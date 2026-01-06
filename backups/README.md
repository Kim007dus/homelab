# Backup Strategy

Proxmox VE Host → Creates VM backup → Stores to mounted rclone → TransIP Stack

```shell
# Install rclone
apt install rclone

# Configure (follow interactive setup)
rclone config
# Choose WebDAV, enter your TransIP Stack details

# Create mount point
mkdir -p /mnt/proxmox-backup

# Create systemd service for persistent mount
vim /etc/systemd/system/rclone-transip.service
```

Paste the following configuration:

```ini
[Unit]
Description=RClone mount for Proxmox Backup (TransIP Stack)
After=network-online.target
Wants=network-online.target

[Service]
Type=notify
# Syntax: rclone mount <remote_name>:<remote_path> <local_mount_point>
ExecStart=/usr/bin/rclone mount proxmoc-backup:backupProxmox /mnt/proxmox-backup \
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

Enable and verify the service:

```shell
# Enable and start
systemctl daemon-reload
systemctl enable --now rclone-transip.service
systemctl status rclone-transip.service

# Verify mount
ls -la /mnt/proxmox-backup
```

## Add Storage in Proxmox GUI

1. Go to **Datacenter** → **Storage** → **Add** → **Directory**
2. Fill in:
   * **ID**: `proxmox-backup` (or your preferred name)
   * **Directory**: `/mnt/proxmox-backup`
   * **Content**: Choose backup
   * **Enable**: ✓ (checked)
   * **Shared**: Leave unchecked (unless you have a cluster)
3. Click **Add**

## Set up Automated Backup

1. Go to **Datacenter** → **Backup** → **Add**
2. Configure:
   * **Node**: Your Proxmox node
   * **Storage**: `proxmox-backup` (the storage you just added)
   * **Schedule**: Daily at 02:00 (or your preferred time)
   * **Selection mode**: Select your VM(s)
   * **Compression**: ZSTD (good balance of speed/size)
   * **Mode**: Snapshot (recommended)
   * **Retention**:
       * **Keep Last**: 3 (keeps last 3 backups)
3. Click **Create**
