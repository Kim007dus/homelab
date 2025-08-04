# Ansible Server Cert

I generate all certificates locally, because on many VMs the directories are not always accessible or readable. This also prevents errors on the VM that could interfere with its own certificate management. Only the steps in cert_deploy are executed on the VM.

👉 Running

Only Proxmox:

```bash
ansible-playbook -i inventories/hosts.ini ssl_certificate_management.yml --limit proxmox
```

Restart Proxmox: `systemctl restart pveproxy`

Only Home Assistant:

- Install SSH add-on
- Adjust configuration.yaml:

```yaml
http:
  ssl_certificate: /config/fullchain.pem
  ssl_key: /config/privkey.pem
```

```bash
# Specific service
ansible-playbook -i inventories/hosts.ini ssl_certificate_management.yml --limit home_assistant
```

Restart Home Assistant via ssh: `ha core restart`
