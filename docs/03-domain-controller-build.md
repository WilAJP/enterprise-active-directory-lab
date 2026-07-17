# Domain Controller Deployment

**Server:** DC01-KTQ

**Operating System:** Windows Server 2022 Evaluation

**Hypervisor:** Proxmox VE

**Status:** In Progress

# Objectives
Deploy the first Windows Server virtual machine that will later become the Active Directory Domain Controller for the Enterprise Active Directory Lab. 

# Planning
Before installing Windows Server, the virtual machine was configured with hardware resources appropriate for a domain controller. 

The goal was to provide sufficient performance while preserving host resources for future servers and client workstations. 

# Virtual Hardware Configuration 
| Component | Configuration |
|------------|---------------|
| Hypervisor | Proxmox VE |
| Firmware | UEFI (OVMF) |
| Machine Type | q35 |
| TPM | TPM 2.0 |
| Disk Controller | VirtIO SCSI |
| Disk Size | 60 GB |
| CPU | 2 vCPUs |
| Memory | 4 GB |
| Network Adapter | VirtIO |
| Network Bridge | vmbr0 |

# Design Decisions

## Why UEFI?
Modern Windows Server deployments use UEFI firmware because it provides improved hardware compatibility, Secure Boot support, and aligns with current enterprise hardware standards. 

## Why 4 GB RAM?
A domain controller requires relatively little memory compared to application or database servers. Allocating 4 GB provides sufficient resources while leaving capacity available for additional virtual machines. 

## Why 2 vCPUs?
Authentication, DNS, and DHCP are lightweight workloads in a homelab environment. Two virtual CPUs provide adequate performance without unnecessarily consuming host resources. 

## Why 60 GB?
A 60 GB virtual disk provides enough capacity for Windows Server, Active Directory, DNS, DHCP, logs and future configuration changes while avoiding unnecessary storage allocation. 

## Why vmbr0?
The initial deployment uses the default proxmox bridge to simplify installation, provide internet connectivity, and allow Windows Updates. 

The environment will be migrated to a dedicated isolated virtual network in a future project. 

# Progress
- [X] Created virtual machine
- [X] Installed Windows Server
- [X] Configured static IP
- [X] Renamed Server
- [X] Installed Active Directory
- [] Configured DNS
- [] Configured DHCP
- [] Verified domain functionality
