# Microsoft Active Directory & PowerShell Automation Lab

## Overview

This project simulates a real-world enterprise Active Directory environment using Windows Server, Active Directory Domain Services (AD DS), DNS, Organizational Units (OUs), security groups, and PowerShell automation.

The lab demonstrates how IT administrators automate onboarding, manage user accounts, apply Role-Based Access Control (RBAC), and troubleshoot Active Directory issues in an enterprise environment.

---

# Technologies Used

- Windows Server
- Active Directory Domain Services (AD DS)
- DNS
- PowerShell
- VMware Fusion
- Organizational Units (OUs)
- Security Groups
- RBAC Principles

---

# Skills Demonstrated

- Installing Active Directory Domain Services
- Promoting a server to Domain Controller
- Configuring DNS
- Creating Organizational Units
- Creating users manually and with PowerShell
- Bulk onboarding using CSV files
- Creating and managing security groups
- Disabling user accounts
- Moving disabled users to separate OUs
- Troubleshooting AD object path errors
- Verifying group memberships
- PowerShell automation

---

# Lab Environment

| Component | Details |
|---|---|
| Hypervisor | VMware Fusion |
| Server OS | Windows Server |
| Domain | corp.local |
| Roles Installed | AD DS, DNS |
| Automation Tool | PowerShell |

---

# Organizational Unit Structure

```text
corp.local
│
├── HR
├── IT
├── Finance
│   └── Sales
├── Disabled Users
├── Workstations
└── Servers


Project Walkthrough
1. Installed Active Directory Domain Services
Configured the Windows Server environment and installed AD DS.
2. Promoted Server to Domain Controller
Configured a new forest:
corp.local
Installed DNS during promotion.
3. Configured DNS
Configured DNS during Active Directory deployment to support domain services and internal name resolution.
4. Created Organizational Units
Created OUs to simulate enterprise departments and administrative structure.
Organizational Units Created
HR
IT
Finance
Sales
Disabled Users
Workstations
Servers
5. User Lifecycle Management
Performed common IT administration tasks:
Created users
Disabled accounts
Moved users to Disabled Users OU
Reset passwords
Example: Disabling a User Account
Example: Disabled User OU
Security Groups & RBAC
Created security groups to simulate Role-Based Access Control (RBAC).
Groups Created
IT_team
Finance_team
Sales_team
HR_files_access
Tasks Performed
Added users to department groups
Verified group membership
Applied least privilege principles
PowerShell Automation
Automated user onboarding using PowerShell.
Bulk User Creation Script
Import-Csv C:\bulk-users.csv | ForEach-Object {

    $FullName = "$($_.FirstName) $($_.LastName)"

    New-ADUser `
        -Name $FullName `
        -GivenName $_.FirstName `
        -Surname $_.LastName `
        -SamAccountName $_.Username `
        -UserPrincipalName "$($_.Username)@corp.local" `
        -Path "OU=Sales,DC=corp,DC=local" `
        -AccountPassword (ConvertTo-SecureString "P@ssw0rd123!" -AsPlainText -Force) `
        -Enabled $true `
        -ChangePasswordAtLogon $true
}
Troubleshooting
During the lab, several real-world Active Directory issues were encountered and resolved.
Issues Resolved
Directory object not found
Invalid OU paths
Missing security groups
Incorrect distinguished names
Group membership assignment errors
Verification Commands Used
Get-ADOrganizationalUnit -Filter * | Select Name, DistinguishedName
Get-ADGroupMember -Identity "Sales_team"
Get-ADUser tuser
PowerShell Group Automation
Created security groups and assigned members using PowerShell.
Example
New-ADGroup `
-Name "Sales_team" `
-GroupScope Global `
-GroupCategory Security `
-Path "OU=Sales,DC=corp,DC=local"

Add-ADGroupMember `
-Identity "Sales_team" `
-Members jwalker, sturner, dharris, omartin, eclark
Screenshots Included
This project includes screenshots demonstrating:
AD DS installation
Domain Controller promotion
DNS setup
OU creation
User account management
Disabled account management
Security groups
PowerShell automation
Error troubleshooting
Group verification<img width="1680" height="1050" alt="Screenshot 2026-05-06 at 9 42 11 PM" src="https://github.com/user-attachments/assets/4b5f4fdf-75e7-490b-954b-572dd9911801" />
<img width="1680" height="1050" alt="Screenshot 2026-05-06 at 9 41 15 PM" src="https://github.com/user-attachments/assets/20fa4ca0-6f74-4479-9ae7-933da167a749" />
<img width="1680" height="1050" alt="Screenshot 2026-05-06 at 9 37 46 PM" src="https://github.com/user-attachments/assets/7b8e387e-b2f0-4b5f-819e-16655e196da5" />
<img width="1680" height="1050" alt="Screenshot 2026-05-06 at 9 28 03 PM" src="https://github.com/user-attachments/assets/9c766e03-9671-4d6c-8726-87b76f7d2648" />
<img width="1680" height="1050" alt="Screenshot 2026-05-06 at 9 27 58 PM" src="https://github.com/user-attachments/assets/963e1198-9399-40b6-890c-5cb6a0803ab2" />
<img width="1680" height="1050" alt="Screenshot 2026-05-06 at 9 12 35 PM" src="https://github.com/user-attachments/assets/b4440e59-d358-4f6c-ae7b-cdbec07936fd" />
<img width="1680" height="1050" alt="Screenshot 2026-05-06 at 9 04 14 PM" src="https://github.com/user-attachments/assets/6698d48c-d2b7-4e78-9892-dd09dbd151ac" />
<img width="1680" height="1050" alt="Screenshot 2026-05-06 at 8 29 32 PM" src="https://github.com/user-attachments/assets/7e8c0eab-215a-42d5-b652-46b87c8f46dd" />
<img width="1680" height="1050" alt="Screenshot 2026-05-06 at 7 14 38 PM" src="https://github.com/user-attachments/assets/b1816060-1850-4ad3-8cf1-2f3ccd281e16" />
<img width="1680" height="1050" alt="Screenshot 2026-05-06 at 7 07 44 PM" src="https://github.com/user-attachments/assets/8e6d2667-17f1-4b03-8e3a-6084ee7fe3a9" />
<img width="1680" height="1050" alt="Screenshot 2026-05-06 at 7 02 37 PM" src="https://github.com/user-attachments/assets/95fa0803-4da5-4a14-a7ec-426283516b5b" />
<img width="1680" height="1050" alt="Screenshot 2026-05-06 at 7 02 30 PM" src="https://github.com/user-attachments/assets/6b7c27e0-bf42-4f69-a919-bc5e320aceb4" />
<img width="1680" height="1050" alt="Screenshot 2026-05-06 at 7 02 25 PM" src="https://github.com/user-attachments/assets/f4c07be2-529a-49e0-86e6-1af6585be0d1" />
<img width="1680" height="1050" alt="Screenshot 2026-05-06 at 6 59 20 PM" src="https://github.com/user-attachments/assets/490b138e-4b0b-4fa5-a975-c399c5721b85" />
<img width="1680" height="1050" alt="Screenshot 2026-05-06 at 6 44 58 PM" src="https://github.com/user-attachments/assets/936a3eec-efcb-42ad-afe5-69fd70b5416b" />
<img width="1680" height="1050" alt="Screenshot 2026-05-06 at 5 48 42 PM" src="https://github.com/user-attachments/assets/994dca6e-a1ac-42a9-93d2-1cb172197e9e" />
<img width="1680" height="1050" alt="Screenshot 2026-05-06 at 5 45 37 PM" src="https://github.com/user-attachments/assets/4514cacc-4260-496e-bd9a-445ea4254d6d" />
<img width="1680" height="1050" alt="Screenshot 2026-05-06 at 5 44 56 PM" src="https://github.com/user-attachments/assets/2d09c8c9-50ab-4a9a-959b-d29918614cd8" />
<img width="1680" height="1050" alt="Screenshot 2026-05-06 at 5 41 29 PM" src="https://github.com/user-attachments/assets/dd3308a1-0c98-40ae-8ae1-9d13c98f1038" />
<img width="1680" height="1050" alt="Screenshot 2026-05-06 at 5 32 40 PM" src="https://github.com/user-attachments/assets/b07efdef-fb69-4c25-8a15-429f923671aa" />
