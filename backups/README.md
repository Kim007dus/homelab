# 💾 Backup Strategy

Welcome to the Backup section of my homelab!
Here you'll find the configuration for securing my virtual machines and containers using offsite backups.

---

## 📚 Contents

- [Purpose & Goals](#-purpose--goals)
- [Architecture & Choices](#️-architecture--choices)
- [Implementation Guide](#️-implementation-guide)
  - [1. Remote Storage Setup](#1-remote-storage-setup-rclone)
  - [2. Persistent Mount](#2-persistent-mount-systemd)
  - [3. Proxmox Configuration](#3-proxmox-configuration)
- [License](#license)

---

## 🎯 Purpose & Goals

**Why this setup?**

- To ensure **Disaster Recovery** capability for my Proxmox environment.
- To implement the **3-2-1 backup rule** (3 copies, 2 media types, 1 offsite).
- To leverage **Snapshot** technology for zero-downtime backups.

**Learning goals:**

- Integrating Cloud Storage via **WebDAV** protocols.
- Managing persistent mounts with **Systemd**.
- Configuring centralized storage in Proxmox VE.

---

## 🏗️ Architecture & Choices

To keep my data safe and accessible, I made the following choices:

- **Proxmox VE:**
  The hypervisor handles the orchestration of backups, creating snapshots of disk states (including running databases and filesystems).

- **Rclone:**
  The "Swiss army knife" of cloud storage. It allows me to mount a remote cloud storage provider as if it were a local disk, making it seamless for Proxmox to write to it.

- **Private European Cloud (TransIP Stack):**
  I use a WebDAV-based storage provider hosted in Europe to ensure data sovereignty and GDPR compliance.

- **Systemd Automount:**
  Instead of manual mounts, a systemd service ensures the backup drive is eagerly mounted at boot and automatically recovered if the connection drops.

---

## 🛠️ Implementation Guide

### 1. Remote Storage Setup (Rclone)

First, we establish the connection to the cloud provider.

```shell
# Install rclone
apt install rclone

# Configure (follow interactive setup)
rclone config
# 💡 Suggestion: Name the remote 'transip-stack'
# Choose 'WebDAV' generic, and enter your credentials
```

### 2. Persistent Mount (Systemd)

We create a mount point and a service to keep it connected.

```shell
# Create local mount point
mkdir -p /mnt/proxmox-backup

# Create systemd service file
nano /etc/systemd/system/rclone-transip.service
```

**Configuration File:**

```ini
[Unit]
Description=RClone mount for Proxmox Backup (TransIP Stack)
After=network-online.target
Wants=network-online.target

[Service]
Type=notify
# Syntax: rclone mount <remote_name>:<remote_path> <local_mount_point>
# Update 'transip-stack' to match your rclone config name (e.g., proxmox-backup)
ExecStart=/usr/bin/rclone mount transip-stack: /mnt/proxmox-backup \
  --vfs-cache-mode writes \
  --vfs-cache-max-age 24h \
  --cache-dir /var/cache/rclone \
  --allow-other \
  --dir-cache-time 5m
ExecStop=/bin/fusermount -u /mnt/proxmox-backup
Restart=on-failure
RestartSec=10

[Install]
WantedBy=multi-user.target
```

**Enable & Verify:**

```shell
# Enable and start the service
systemctl daemon-reload
systemctl enable --now rclone-transip.service
systemctl status rclone-transip.service

# 🔎 Verify mount
ls -la /mnt/proxmox-backup
```

### 3. Proxmox Configuration

Finally, we tell Proxmox to use this new directory.

**Add Storage:**

1. Go to **Datacenter** → **Storage** → **Add** → **Directory**
2. Fill in the details:
    - **ID**: `proxmox-backup`
    - **Directory**: `/mnt/proxmox-backup`
    - **Content**: Select `VZDump backup file`
    - **Enable**: ✅
    - **Shared**: ⬜ (Unchecked)
3. Click **Add**

**Schedule Automated Backups:**

1. Go to **Datacenter** → **Backup** → **Add**
2. Configure the job:
    - **Node**: All (or specific node)
    - **Storage**: `proxmox-backup`
    - **Schedule**: `Daily` at `02:00` 🕑
    - **Mode**: `Snapshot` (Recommended for running VMs)
    - **Compression**: `ZSTD` (Best balance)
    - **Retention**: `Keep Last: 7`
3. Click **Create**

---

## License

MIT License - see [LICENSE](../LICENSE) for details.

---

> Part of my [🏠 Homelab project](../README.md)
