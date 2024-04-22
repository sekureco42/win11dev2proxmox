# win11dev2proxmox
## Purpose
This script is intended to deploy Windows 11 Development VM to your proxmox instance. It will download an actual VMWare image to your Proxmox host, extracts it, imports it into Proxmox; adjusts hardware settings, starts the system and waits until you install the Virtio drivers to enable QEMU agent which then will be used to add an additional user to the system as local administrator and installs OpenSSH server for connection from an Ansible host.

For more details see my blog on https://www.sekureco42.ch/posts/deploy-windows-11-dev-vm-to-proxmox/, `Deploy Windows 11 Dev VM to Proxmox`

## Usage
* Modify first section with your settings:

```bash
# --- Start Config Section
USERNAME= # if defined a user will be added as local administrator
PASSWORD= # Password for the new user
VMNAME= # If defined it will be used as name in Proxmox
VMDOWNLOAD_PATH="/mnt/pve/ISOimages" # Where to download the Windows 11 Developer Image
VMSTORAGE="FastDisk" # Where should the VM saved on Proxmox
VMNET="virtio,bridge=vmbr0,firewall=0,tag=401" # Your network definition for VM
VIRTIO_ISO="ISOimages:iso/virtio-win.iso" # Location of virtio driver ISO
# --- End Config Section
```

* Define dedicated username and password which should be created during deployment
* Adjust network setup (in the example VLAN `401` with `vmbr0` will be used to deploy the VM)
* Run the script by invoking the script on your Proxmox Host - depending on your download and disk speed it takes 30 to 60 minutes.

## Feedback
For feedback write an email to rOger_at_sekureco42.ch

## Thanks
Thanks go to following projects:
- https://www.proxmox.com/en/proxmox-virtual-environment/overview
- https://github.com/AlexNabokikh/windows-playbook
- https://developer.microsoft.com/en-us/windows/downloads/virtual-machines/