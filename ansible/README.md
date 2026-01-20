# Homelab Automation with Ansible

This repository contains all Ansible automations for my homelab environment. The goal is to enable consistent, repeatable deployments and configurations.

## 🎯 Objectives

- **Automation**: Replace manual configuration with code
- **Consistency**: Uniform setup across all homelab servers
- **Documentation**: Apply Infrastructure as Code principles
- **Scalability**: Easily add new services

## 📋 Current Playbooks

### SSL Certificate Management

Automates the creation and deployment of SSL certificates within the homelab using a self-signed Root CA (Home-CA).

**Benefits:**

- No browser warnings about insecure connections
- Full HTTPS coverage within the local network
- Centralized certificate management
- Automatic deployment to various services

**Supported services:**

- Home Assistant
- Proxmox VE
- *(Extendable for other services)*

**Usage:**

*Home Assistant:*

- Install SSH add-on
- Adjust configuration.yaml:

```yaml
http:
  ssl_certificate: /config/fullchain.pem
  ssl_key: /config/privkey.pem
```

```bash
# Run playbook
ansible-playbook -i inventories/hosts.ini ssl_certificate_management.yml --limit home_assistant
```

Restart Home Assistant via ssh: `ha core restart`

*Proxmox:*

```bash
# Run playbook
ansible-playbook -i inventories/hosts.ini ssl_certificate_management.yml --limit proxmox
```

Restart Proxmox: `systemctl restart pveproxy`

### Argo CD Bootstrap - kubectl apply method

Installs Argo CD on the k3s cluster, applies the Traefik ingress, and bootstraps the GitOps root application defined in [ansible_install_argocd/install_argocd.yml](ansible_install_argocd/install_argocd.yml).

**Highlights:**

- Creates the argocd namespace and applies the upstream Argo CD manifest
- Patches argocd-server for TLS termination at the ingress
- Waits for core pods to become ready before rolling out the root application
- Prints the initial admin password on first install (optional for upgrades)

**Usage:**

```bash
cd ansible_install_argocd
ansible-playbook install_argocd.yml 
```

### Argo CD Bootstrap - HELM

Work in progress

## 📁 Repository Structure

```
ansible/
├── README.md                               # This file
├── ansible-server-certs/
    └──  ssl-certificate-management.yml     # SSL certificate automation playbook
    └── roles/
        └── cert_generator/                 # SSL certificate role
            ├── tasks/
            ├── files/
        └── cert_deploy/
            └──  tasks/
                └── main.yml
                └── home_assistant.yml
                └── proxmox.yml   
    └── inventory/
            └── hosts.ini                   # Homelab hosts
    └── group_vars/
        └── home_assistant.yml              # HA specific variables - not in this repo
        └── proxmox.yml                     # Proxmox specific variables - not in this repo
```


## 🔧 Prerequisites

- Ansible >= 2.9
- SSH access to all target hosts
- Root/sudo privileges on target systems
- Python >= 3.6 on control node

## ⚙️ Setup

1. **Clone repository:**

   ```bash
   git clone <repository-url>
   cd ansible
   ```

2. **Configure inventory:**

   ```bash
   cp inventory/hosts.ini.example inventory/hosts.ini
   # Edit with your own hosts
   ```

3. **Test connectivity:**

   ```bash
   ansible all -m ping
   ```

## 🤝 Contributing

This is my personal homelab project, but suggestions and improvements are always welcome via issues or pull requests.

## 📝 License

MIT License - see [LICENSE](LICENSE) for details.

---

> **Note**: This repository contains configurations specific to my homelab environment. Many variables, such as group_vars & files/certs, are of course not online. Adjust these variables and configurations before using them in your own environment.
