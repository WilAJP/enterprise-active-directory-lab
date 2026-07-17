# Active Directory Structure Design
## Objective
The objective of this phase was to design the Active Directory structure for Kinetiq Technologies before creating users, computers, groups, or Group Policy Objects. 

Planning the structure first helped establish where Active Directory Objects will be stored and how they will be managed as the environment grows. 

The design needed to support:
- Department-based organization
- Separate management of users and computers
- Group Policy targeting
- Security group management 
- Administrative and service accounts
- Future servers and workstations
- Disabled users and computer accounts

## Environment 
The Active Directory environment currently consists of:
| Component | Configuration |
|---|---|
| Domain Controller | **DC01-KTQ** |
| Operating System | **Windows Server 2022 Standard Evaluation** |
| Active Directory Domain | **ad.kinetiqtech.com** |
| NetBIOS Domain Name | **KINETIQ** |
| Forest Functional Level | **Windows Server 2016** |
| Domain Functional Level | **Windows Server 2016** |
| DNS Server | **DC01-KTQ** |
| Domain Controller IP Address | `10.0.0.250` |

The environment currently contains one domain controller. Additional servers, workstations, users, groups, and policies will be added during later phases. 

## Configuration 
No Active Directory Objects were created during this phase. This phase focused on designing the structure that will be implemented next. 

### Organizational Unit Design
A top level OU named `Kinetiq Technologies` will be created under the **ad.kinetiqtech.com** domain. 

The planned structure is: 
```text
Kinetiq Technologies
├── Users
│   ├── Engineering
│   ├── Accounting
│   ├── Sales
│   ├── HR
│   ├── Management
│   └── IT
│
├── Computers
│   ├── Workstations
│   │   ├── Engineering
│   │   ├── Accounting
│   │   ├── Sales
│   │   ├── HR
│   │   ├── Management
│   │   └── IT
│   └── Servers
│
├── Groups
│   ├── Security
│   └── Distribution
│
├── Administrative Accounts
│
├── Service Accounts
│
└── Disabled Objects
    ├── Users
    └── Computers
```

This design separates Active Directory Objects by object type before dividing them by departments. 

Users and computers are separated because they are managed differently and receive different types of Group Policy settings. User policies can control setting such as drive mappings and desktop restrictions, while computer policies can control firewall rules, Windows update, software deployment, and other device settings. 

### Department Structure
The following departments were included in the design:
- Engineering
- Accounting
- Sales
- Human Resources
- Management
- Information Technology

Each department will have its own user OU and workstation OU. 

This will allow policies to be applied to a specific department without affecting the entire domain. 

For example, a policy linked to the Accounting user OU could map an Accounting shared drive. A separate policy linked to the Accounting workstation OU could apply security settings to Accounting computers. 

### Workstation and Server Separation
Workstations and servers will be stored in separate OUs. 

Employee workstations will be placed under: 
```text
Kinetiq Technologies/Computers/Workstations
```

Future member servers will be placed under: 
```text
Kinetiq Technologies/Computers/Servers
```

This separation is important because servers should not receive the same Group Policy settings as Windows 11 workstations. 

The existing domain controller, **DC01-KTQ**, will remain in the build in Domain Controllers OU. It will not be moved in the Kinetiq Technologies Servers OU because domain controllers require their own policies an d administrative controls. 

### Security Group Design
Security groups will be used to assign access to resources instead of assigning permissions directly to individual users. 

Planned department groups include: 
```text
GG_Engineering_Users
GG_Accounting_Users
GG_Sales_Users
GG_HR_Users
GG_Management_Users
GG_IT_Users
```

The `GG` prefix identifies these as global groups. 

Users will be added to the group associated with their department. The groups can later be granted access to shared folders, printers, applications, or other resources. 

This will make access easier to manage when employees join, leave, or move between departments. 

The Groups OU will contain separate child OUs for security groups and distribution groups. 

Security groups will be used for permissions. Distribution groups may be user later for email related organization, but they are not currently required for the lab. 

### Administrative Accounts
Administrative accounts will be stored separately from standard user accounts. 

A future administrator may have both a standard account and a privileged account, such as: 
```text
wilfred.jimenez
adm-wilfred.jimenez
```

The standard account would be used for normal daily activity. The administrative account would only be used when elevated permissions are required. 

Separating privileged accounts reduces the amount of time administrative credentials are used during normal activity. 

### Service accounts
A separate OU will be created for service accounts. 

Service accounts are used by applications, scheduled tasks, or Window services rather than by a person for normal sign in activity. 

Planned naming will use the `svc-` prefix, such as: 
```text
svc-backup
svc-monitoring
```

No service accounts are currently required, but including the OU now provides a clear location for them as the environment grouws. 

### Disabled Objects
Separate OUs will be created for disabled user and computer accounts. 

When an employee leaves the company, the account can be disabled and moved into:
```text
Kinetiq Technologies/Disabled Objects/Users
```

Retired or replaced computer accounts can be moved it: 
```text
Kinetiq Technologies/Disabled Objects/Computers
```

Retired or replaced computer accounts are permanently removed. 

It also keeps inactive objects separate from active users and computers. 

### Group Policy Considerations 
The OU structure was designed with future Group Policy use in mind. 

Policies can be linked to different levels of the structure depending on how broadly they should apply. 

A general workstation security policy could be linked to:
```text
Kinetiq Technologies/Computers/Workstations
```

A department specific policy could be linked to an OU such as: 
```text
Kinetiq Technologies/Users/Engineering
```

The structure provides enough separation to target policies without creating an excessive number of OUs. 

## Lessons Learned
I learned that Organizational Units are not only used to make Active Directory look organized. Their structure affects how administrators apply Group Policy and delegate management. 

I also gained a better understand of the difference between OUs and security groups. OUs organize and manage Active Directory objects, while security groups are used to assign permissions to resources. 

Separating users, workstations, servers, administrative accounts, and service accounts will make the environment easier to manage as more systems are added. 

Planning the structure before creating objects should also reduce the need to reorganize Active Directory later. 

## Next Steps
The next phase will implement the planned structure in Active Directory Users and Computers. 

After the OUs are created, the structure will be verified and documented with screenshots before users, computers, and security groups are added. 

