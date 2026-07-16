# Troubleshooting Log
## Issue: Windows Server Installer could not detect the virtual hard disk
### Problem
During the Windows Server 2022 installation, the installer displayed no available disks and prompted to load a storage driver. 

### Root Cause
The VM was configured to use a VirtIO SCSI virtual disk. Windows Server installation media does not include the VirtIO storage drivers, so it could not detect the virtual hard disk. 

### Troubleshooting Process
- Verified that the virtual hard disk existed in Proxmox. 
- Confirmed the Windows Server ISO was attached correctly. 
- Verified the VM booted from the Windows Installation media. 
- Determined that the VirtIO driver ISO was missing. 
- Download the virtio-win.iso.
- Uploaded it to Proxmox and attached it as a second CD/DVD drive. 
- Loaded the appropriate VirtIO storage driver during Windows Setup. 