# Project Planning

## Objective

The goal of this project is to build a small enterprise Active Directory environment from the ground up in a homelab. Rather than following a tutorial from start to finish, I want to understand how each service works, why it is configured the way it is, and how the different components work together.

Throughout the project, I will document each phase as it is completed. The finished repository will serve as both a learning resource for myself and a portfolio demonstrating hands-on Windows Server administration and common Help Desk tasks.

---

## Project Overview

This lab simulates the IT infrastructure for a fictional company called **Kinetiq Technologies**. The environment will be expanded over multiple phases to include the core services commonly found in an enterprise Windows environment.

Planned services include:

- Active Directory Domain Services (AD DS)
- DNS
- DHCP
- Group Policy
- File Services
- Print Services
- PowerShell automation
- Windows 11 client management
- Simulated Help Desk scenarios

---

## Company Information

| Setting | Value |
|---------|-------|
| Company | Kinetiq Technologies |
| Industry | Technology Consulting |
| Employees | 40 |
| Departments | IT, Engineering, Accounting, Human Resources, Sales, Management |

---

## Domain Information

| Setting | Value |
|---------|-------|
| Domain Name | ad.kinetiqtech.com |
| NetBIOS Name | KINETIQ |

---

## Planned Network

| Setting | Value |
|---------|-------|
| Network | 10.10.10.0/24 |
| Gateway | 10.10.10.1 |
| Domain Controller | 10.10.10.10 |
| File Server | 10.10.10.20 |
| DHCP Scope | 10.10.10.100 - 10.10.10.199 |

---

## Planned Infrastructure

### Servers

| Server | Purpose | IP Address |
|---------|---------|------------|
| DC01-KTQ | Active Directory, DNS, DHCP | 10.10.10.10 |
| FS01-KTQ | File and Print Services | 10.10.10.20 |
| ADMIN01-KTQ | Administrative Workstation | DHCP |

### Client Workstations

The environment will include Windows 11 client machines representing different departments throughout the company.

- KTQ-ACC-01
- KTQ-ENG-01
- KTQ-HR-01
- KTQ-MGMT-01
- KTQ-SALES-01

---

## Lab Environment

The project is hosted entirely within my homelab.

### Management Workstation

| Component | Value |
|----------|-------|
| Operating System | Linux Mint |

The management workstation is used to:

- Manage the Git repository
- Create project documentation
- Build network diagrams
- Connect to the virtualization host

### Virtualization Host

| Component | Value |
|----------|-------|
| Hardware | Dedicated Laptop |
| Operating System | Ubuntu Server |
| Hypervisor | Proxmox VE |

The virtualization host runs all Windows Server and Windows 11 virtual machines used throughout the project.

---

## Project Scope

By the end of the project, the environment should support:

- A fully functional Active Directory domain
- Centralized user and computer management
- DNS and DHCP services
- Group Policy deployment
- Department file shares with appropriate permissions
- Print services
- Remote administration
- PowerShell automation
- Simulated Help Desk support tasks

Each phase will be documented after it has been completed, including the configuration performed, how it was verified, and any lessons learned before moving on to the next phase.

---

## Lessons Learned

Planning the environment before creating any virtual machines helped establish a clear roadmap for the rest of the project. Defining the network, server roles, naming conventions, and project scope ahead of time should make future phases easier to manage and keep the environment organized as it grows.

---

## Next Steps

The next phase focuses on designing the network architecture for the lab, including the logical network layout, IP addressing scheme, and naming conventions that will be used throughout the environment.