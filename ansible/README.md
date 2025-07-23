# Homelab Automation with Ansible

Deze repository bevat alle Ansible automatiseringen voor mijn homelab omgeving. Het doel is om consistente, herhaalbare deployments en configuraties mogelijk te maken.

## 🎯 Doelstellingen

- **Automatisering**: Handmatige configuratie vervangen door code
- **Consistentie**: Uniforme setup binnen alle homelab servers
- **Documentatie**: Infrastructure as Code principes toepassen
- **Schaalbaarheid**: Eenvoudig nieuwe services toevoegen

## 📋 Huidige Playbooks

### SSL Certificate Management
Automatiseert het aanmaken en deployen van SSL certificaten binnen het homelab met behulp van een self-signed Root CA (Home-CA).

**Voordelen:**
- Geen browser waarschuwingen over onveilige verbindingen
- Volledige HTTPS coverage binnen het lokale netwerk
- Gecentraliseerd certificaatbeheer
- Automatische deployment naar verschillende services

**Ondersteunde services:**
- Home Assistant
- Proxmox VE
- *(Uitbreidbaar voor andere services)*

**Usage:**

*Home-Assistant:*
- SSH add-on installeren
- configuration.yaml aanpassen:
```yaml
http:
  ssl_certificate: /config/fullchain.pem
  ssl_key: /config/privkey.pem
```
```bash
#Run playbook
ansible-playbook -i inventories/hosts.ini ssl_certificate_management.yml --limit home_assistant
```
Home-assistant herstarten via ssh `ha core restart`

*Proxmox:*
```bash
#Run playbook
ansible-playbook -i inventories/hosts.ini ssl_certificate_management.yml --limit proxmox
```
Proxmox herstarten `systemctl restart pveproxy`



## 📁 Repository Structuur

```
ansible/
├── README.md                               # Dit bestand
├── ansible-server-certs/
    └──  ssl-certificate-management.yml     # SSL certificaat automation playbook
    └── roles/
        └── cert_generator/                 # SSL certificaat role
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
        └── home_assistant.yml              # HA specifieke variabelen - niet in deze repo
        └── proxmox.yml                     # Proxmox specifieke variabelen - niet in deze repo
```

## 🚀 Geplande Uitbreidingen

- [ ] **ArgoCD Deployment op mijn cluster**: GitOps voor Kubernetes workloads

## 🔧 Prerequisites

- Ansible >= 2.9
- SSH toegang tot alle target hosts
- Root/sudo privileges op target systems
- Python >= 3.6 op control node

## ⚙️ Setup

1. **Clone repository:**
   ```bash
   git clone <repository-url>
   cd ansible
   ```

2. **Configureer inventory:**
   ```bash
   cp inventory/hosts.ini.example inventory/hosts.ini
   # Edit met je eigen hosts
   ```

3. **Test connectiviteit:**
   ```bash
   ansible all -m ping
   ```

## 🤝 Bijdragen

Dit is mijn persoonlijke homelab project, maar suggesties en verbeteringen zijn altijd welkom via issues of pull requests.

## 📝 License

MIT License - zie [LICENSE](LICENSE) bestand voor details.

---

> **Note**: Dit repository bevat configuraties specifiek voor mijn homelab omgeving, veel variabelen, zoals group_vars & files/certs staan natuurlijk niet online. Pas deze variabelen en configuraties aan voordat je ze in je eigen omgeving gebruikt.
