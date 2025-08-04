# Home Assistant

I run my Home Assistant in a VM. I used a [community script](https://www.derekseaman.com/2023/10/home-assistant-proxmox-ve-8-0-quick-start-guide-2.html) to get started, as this seemed the easiest way to begin.

## Next steps

* Using Ansible, I deployed my SSL certificate so I can access my VM locally via https://.
* Passing through USB devices to the specific VM:

```bash
**@proxmox:~# lsusb
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 0573:1573 Zoran Co. Personal Media Division (Nogatech) USB Audio and HID
Bus 001 Device 002: ID 0bda:c821 Realtek Semiconductor Corp. Bluetooth Radio 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
**@proxmox:~# qm set 100 -usb0 host=0bda:c821
```
