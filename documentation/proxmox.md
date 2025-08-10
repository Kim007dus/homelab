# VM Ubuntu template

Bron: https://austinsnerdythings.com/2021/09/01/how-to-deploy-vms-in-proxmox-with-terraform/

````
wget https://cloud-images.ubuntu.com/focal/current/focal-server-cloudimg-amd64.img
sudo apt update -y && sudo apt install libguestfs-tools -y
sudo virt-customize -a focal-server-cloudimg-amd64.img --install qemu-guest-agent

sudo qm create 9000 --name "ubuntu-clone" --memory 2048 --cores 2 --net0 virtio,bridge=vmbr0
sudo qm importdisk 9000 focal-server-cloudimg-amd64.img local-lvm
sudo qm set 9000 --scsihw virtio-scsi-pci --scsi0 local-lvm:vm-9000-disk-0
sudo qm set 9000 --boot c --bootdisk scsi0
sudo qm set 9000 --ide2 local-lvm:cloudinit
sudo qm set 9000 --serial0 socket --vga serial0
sudo qm set 9000 --agent enabled=1

sudo qm template 9000
````

To do: Terraform clone aanmaken - zodat bij update van proxmox etc dit heel makkelijk kan straks.

Terraform: K8s cluster:
https://austinsnerdythings.com/2021/09/01/how-to-deploy-vms-in-proxmox-with-terraform/
https://www.youtube.com/watch?v=U1VzcjCB_sY&t=564s

