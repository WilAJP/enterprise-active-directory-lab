# Active Directory Installation

## Objective

The goal of this phase was to install the Active Directory Domain Services (AD DS) role on **DC01-KTQ** and promote the server to the first Domain Controller for the Kinetiq Technologies environment.

During the promotion process, a new Active Directory forest was created using the domain **ad.kinetiqtech.com**, and the DNS Server role was installed automatically.

---

## Environment

| Setting | Value |
|---------|-------|
| Server Name | DC01-KTQ |
| Operating System | Windows Server 2022 Standard Evaluation |
| Hypervisor | Proxmox VE |
| Domain Name | ad.kinetiqtech.com |
| NetBIOS Name | KINETIQ |
| Server IP Address | 10.10.10.10 |

---

## Configuration

### Installing Active Directory Domain Services

The Active Directory Domain Services role was installed through the Add Roles and Features Wizard in Server Manager.

Installing the role prepares the server to become a Domain Controller, but the Active Directory environment is not created until the server is promoted.

![Add Roles and Features Wizard](../images/active-directory/01-add-roles-wizard.png)

After confirming the installation settings, Windows Server installed the required Active Directory services.

![Installation Progress](../images/active-directory/02-install-progress.png)

---

### Promoting the Server

Once the installation completed, Server Manager displayed a notification indicating that additional configuration was required.

Selecting Promote this server to a domain controller launched the Active Directory Domain Services Configuration Wizard.

![Post-Deployment Notification](../images/active-directory/03-post-deployment.png)

---

### Creating the Active Directory Forest

Since this is the first Domain Controller in the environment, I created a new Active Directory forest using the domain:

**ad.kinetiqtech.com**

This domain will be used throughout the project to manage users, computers, groups, and security policies.

![Create New Forest](../images/active-directory/04-create-forest.png)

---

### Domain Controller Configuration

During the promotion process, the following options were configured:

- Forest Functional Level: Windows Server 2016
- Domain Functional Level: Windows Server 2016
- DNS Server enabled
- Global Catalog enabled
- Read-Only Domain Controller disabled
- Directory Services Restore Mode (DSRM) password configured

The first Domain Controller in a new forest also functions as the Global Catalog. DNS was installed during the promotion process because Active Directory depends on DNS to locate domain services.

![Domain Controller Options](../images/active-directory/05-domain-options.png)

---

### Prerequisite Validation

Before promoting the server, Windows Server performed a series of prerequisite checks to verify that the required configuration was in place.

The validation completed successfully with only the expected warnings for a new forest deployment.

![Prerequisite Check](../images/active-directory/06-prerequisites-check.png)

---

### Domain Controller Promotion

After the prerequisite checks completed successfully, Windows promoted **DC01-KTQ** to the first Domain Controller in the environment.

During this process Windows:

- Created the Active Directory forest
- Created the **ad.kinetiqtech.com** domain
- Installed and configured DNS
- Created the Active Directory database (NTDS)
- Created the SYSVOL shared folder

The server automatically restarted after the promotion completed.

![Server Restart After Promotion](../images/active-directory/07-domain-controller-reboot.png)

---

## Verification

After the restart, several checks were performed to verify that Active Directory was functioning correctly.

### Active Directory Users and Computers

The **ad.kinetiqtech.com** domain was successfully created, and **DC01-KTQ** appeared in the Domain Controllers organizational unit.

This confirmed that the server had been successfully promoted.

![Active Directory Users and Computers](../images/active-directory/08-active-directory-users-computers.png)

---

### DNS Manager

The DNS Manager console showed that the required forward lookup zones had been created automatically during promotion.

The following zones were present:

- ad.kinetiqtech.com
- _msdcs.ad.kinetiqtech.com

This confirmed that DNS was configured correctly as part of the Active Directory installation.

![DNS Manager](../images/active-directory/09-dns-manager.png)

---

## Lessons Learned

This phase helped me understand that installing the Active Directory Domain Services role and promoting a server to a Domain Controller are two separate steps. Installing the role only prepares the server. The Active Directory environment is created during the promotion process.

I also learned how closely Active Directory and DNS work together. Without DNS, clients would not be able to locate Domain Controllers or authenticate to the domain.

Finally, creating the first Domain Controller also establishes the Active Directory forest, which becomes the foundation for managing users, computers, groups, and security policies throughout the environment.

---

## Next Steps

With the first Domain Controller successfully deployed, the next phase will focus on building the Active Directory structure for Kinetiq Technologies.

This includes:

- Creating Organizational Units (OUs)
- Creating security groups
- Creating user accounts
- Creating computer accounts
- Preparing the environment for future Group Policy deployment