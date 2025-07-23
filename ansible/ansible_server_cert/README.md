# Ansible Server Cert

Alle certficaten genereer ik lokaal, dit is omdat vaak op verschillende vm's de mappen niet of moeilijk leesbaar zijn. Ook voorkom je zo fouten op de VM die het eigen certficaat management in de war brengen. Alleen de stappen in cert_deploy gaan richting de VM. ti


👉 Runnnen

Alleen Proxmox:
```bash
ansible-playbook ssl_certificate_management.yml --limit proxmox
```
Proxmox herstarten `systemctl restart pveproxy`

Alleen Home-Assistant:
Home-Assistant: 
- SSH add-on installeren
- configuration.yaml aanpassen:
```yaml
http:
  ssl_certificate: /config/fullchain.pem
  ssl_key: /config/privkey.pem
```
```bash
# Specifieke service
ansible-playbook ssl-certificate-management.yml --limit home_assistant
```
Home-assistant herstarten via ssh `ha core restart`
