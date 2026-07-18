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

### Resolution 
The VirtIO storage driver was successfully loaded from the attacted VirtIO driver ISO. 

Windows Setup immediately detected the virtual disk, allowing the installation to continue normally. 

After Windows installation completed, the VirtIO network driver wa also installed through Device Manager, enabling the Red Hat VirtIO Ethernet Adapter. 

### Lessons Learned
Windows Server Installation media does not include all VirtIO drivers by default. 

When deploying Windows virtual machines on Proxmox using VirtIO devices, the VirtIO driver ISO should be attached before beginning the installation. 

## Issue: Member Server Could Not Resolve the Active Directory Domain
### Problem
After installing Windows Server on FILE01-KTQ, the server could communicate with the Domain Controller by IP address but was unable to properly resolve the Active Directory domain during initial testing. 

DNS lookups returned inconsistent results, preventing verification that the server was communicating with the Active Directory integrated DNS server. 

### Root Cause
The member server initially received DNS information from the network through IPv6 while also using manually configured IPv4 settings. 

As a result, DNS queries were being set to the home network's public DNS servers instead of the Domain Controller, preventing the server from resolving internal Active Directory records.

Additionally, an IP address conflict was encountered after assigning the initial static IP address, requiring a different address to be selected. 

### Troubleshooting Process

- Verified basic network connectivity by successfully pinging the Domain Controller's IP address.
- Verified the Active Directory DNS zones existed on DC01-KTQ.
- Confirmed the Domain Controller's DNS service was running correctly.
- Used `ipconfig /all` to inspect the network configuration.
- Discovered that the server was still using public IPv6 DNS servers.
- Disabled IPv6 on the member server to simplify DNS resolution within the lab environment.
- Assigned a new static IPv4 address after detecting an IP address conflict.
- Verified the member server was using the Domain Controller (`10.0.0.250`) as its DNS server.
- Confirmed DNS resolution directly against the Domain Controller using PowerShell.
- Successfully joined FILE01-KTQ to the Active Directory domain.

### Resolution
After correcting the network configuration and ensuring the member server used the Domain Controller as its only DNS server, FILE01-KTQ successfully joined the `ad.kinetiqtech.com` domain.

The computer account was then moved into the Kinetiq Technologies -> Computers -> Servers Organizational Unit. 

### Lessons Learned
Active Directory environments rely heavily on DNS.

Domain-joined Windows systems should use the Domain Controller as their primary DNS server rather than public DNS servers.

Systematic troubleshooting using tools such as `ipconfig`, `Resolve-DnsName`, `nslookup`, and DNS Manager made it possible to isolate the issue and verify each layer of the network configuration before attempting to join the domain.