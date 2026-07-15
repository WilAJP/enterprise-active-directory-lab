# Enterprise Active Directory Lab

## Project Goal
Build a simulated enterprise windows environment to get hands on experience with Active Directory, DNS, DHCP, Group Policy, file services, print services, PowerShell automation, and common help desk tasks. 

I will provide full documentation for each step I take to demonstrate practical IT administration skills. 

## Company Information
Company Name: Kinetiq Technologies

Industry: Technology Consulting

Employees: 40

Departments:
- Information Technology
- Engineering
- Accounting
- Human Resources
- Sales
- Management

## Domain Information
Domain Name: 
ad.kinetiqtech.com

NetBIOS name:
KINETIQ

## Network Information
Network: 
10.10.10.0/24

Gateway:
10.10.10.1

DNS Server:
10.10.10.10

DHCP Scope:
10.10.10.100 - 10.10.10.199

## Planned Servers
| Server      | Purpose                       | IP          |
| ----------- | ----------------------------- | ----------- |
| DC01-KTQ    | Active Directory / DNS / DHCP | 10.10.10.10 |
| FS01-KTQ    | File & Print Server           | 10.10.10.20 |
| ADMIN01-KTQ | Administrator Workstation     | DHCP        |

## Planned Clients
KTQ-ACC-01
KTQ-ENG-01
KTQ-HR-01
KTQ-MGMT-01
KTQ-SALES-01

## Planned Services
- Active Directory Domain Services
- DNS
- DHCP
- Group Policy
- File Services
- PowerShell
- Remote Administration

## Success Criteria
The project will be considered complete when:
- Windows Server is deployed
- Active Directory is operational
- Clients can join the domain
- DNS resolves correctly
- DHCP leases addresses
- Users authenticate successfully
- Group Policy deploys settings
- Department file shares function correctly
- Help desk tickets have been documented