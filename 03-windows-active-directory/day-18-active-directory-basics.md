# Day 18 — Active Directory Basics

## Room / Topic

TryHackMe — Active Directory Basics

## Status

Completed

## Time Taken

Approximately 5 hours

---

## What I Practiced

Today I completed the Active Directory Basics room.

This room focused on how companies manage users, computers, permissions, authentication, and policies inside a Windows domain environment.

Topics covered:

- Windows Domains
- Active Directory
- Domain Controllers
- Users and Groups
- Organizational Units
- Managing AD Users
- Managing AD Computers
- Delegating permissions
- Group Policy Objects
- Authentication methods
- Kerberos
- NTLM
- Trees, Forests, and Trusts

This room is important for:

- SOC Analyst L1
- System Admin Trainee
- IT Support
- Windows Admin
- Network Support
- Cybersecurity fundamentals

---

## Windows Domain

A Windows domain is a centralized network environment where users, computers, and resources are managed together.

Instead of managing each computer separately, companies use a domain to manage everything centrally.

Examples of things managed in a domain:

- User accounts
- Computer accounts
- Password policies
- Group memberships
- Access permissions
- Security policies
- Login authentication
- Software and configuration policies

---

## Why Companies Use Domains

Companies use domains because they make administration easier.

Without a domain:

- Each computer has its own local users.
- Passwords must be managed separately.
- Policies must be configured manually.
- Access control becomes difficult.

With a domain:

- Users can log in from domain-joined computers.
- Admins can manage accounts centrally.
- Password resets are easier.
- Security policies can be pushed using Group Policy.
- Access to resources can be controlled using groups.

---

## Domain Controller

A Domain Controller is a server that manages the Active Directory domain.

It handles:

- User authentication
- Computer authentication
- Active Directory database
- Login requests
- Group Policy distribution
- Security and access control

Simple flow:

```text
User logs in
        ↓
Computer contacts Domain Controller
        ↓
Domain Controller verifies credentials
        ↓
User gets access based on permissions
```

Interview line:

```text
A Domain Controller is a server that authenticates users and computers and manages the Active Directory domain.
```

---

## Active Directory

Active Directory is Microsoft’s directory service used to manage users, computers, groups, and other resources in a Windows domain.

It stores information about objects in the domain.

Common Active Directory objects:

- Users
- Groups
- Computers
- Organizational Units
- Printers
- Shared resources
- Service accounts

Interview line:

```text
Active Directory is a centralized directory service used to manage users, computers, groups, and policies in a Windows domain.
```

---

## Active Directory Objects

An object is an item stored inside Active Directory.

Examples:

```text
User object       = represents a person/account
Computer object   = represents a domain-joined machine
Group object      = collection of users/computers
OU object         = container used for organization and policy application
```

---

## Organizational Units

OU stands for Organizational Unit.

OUs are containers inside Active Directory used to organize users, computers, and groups.

Examples:

- IT
- Sales
- Marketing
- Management
- Workstations
- Servers

OUs are useful because admins can apply policies and delegate permissions to specific parts of the organization.

Example:

```text
THM
├── IT
├── Sales
├── Marketing
├── Management
├── Servers
└── Workstations
```

Important:

```text
OUs help organize Active Directory objects and apply Group Policy to specific users or computers.
```

---

## Users in Active Directory

User accounts represent people who need access to the domain.

A user account can be used to:

- Log in to domain computers
- Access shared folders
- Access applications
- Receive permissions through groups
- Be managed by administrators

Common user management tasks:

- Create user
- Disable user
- Reset password
- Unlock account
- Move user to another OU
- Add user to groups
- Remove user from groups

---

## Groups in Active Directory

Groups are used to manage permissions more easily.

Instead of assigning permissions to users one by one, admins add users to groups and assign permissions to the group.

Example:

```text
Sales Users group → access to Sales shared folder
IT Admins group → admin access to IT systems
HR Users group → access to HR resources
```

Why groups are useful:

- Easier permission management
- Better organization
- Easier auditing
- Scalable access control

Interview line:

```text
Groups are used in Active Directory to manage permissions efficiently by assigning access to groups instead of individual users.
```

---

## Computers in Active Directory

When a Windows computer joins a domain, a computer object is created in Active Directory.

Computer objects allow administrators to:

- Manage domain-joined machines
- Apply computer-based policies
- Organize machines by department or type
- Control workstation and server settings

Examples:

```text
Workstations OU
Servers OU
Domain Controllers OU
```

---

## Managing Users in AD

In the room, I practiced user management concepts such as:

- Creating users
- Organizing users inside OUs
- Managing department-based users
- Resetting passwords
- Delegating password reset permissions

Important user management actions:

```text
Create user
Disable user
Reset password
Unlock account
Move user to OU
Add user to group
Remove user from group
```

---

## Delegation in Active Directory

Delegation means giving a user limited administrative permissions.

This allows a normal user to perform specific admin tasks without becoming a full domain admin.

Example from the room:

```text
Phillip was delegated permission to reset passwords for users in the Sales OU.
```

This means Phillip is not a full admin, but he can perform one specific task for one specific OU.

Why delegation is useful:

- Reduces workload for domain admins
- Allows helpdesk users to perform limited tasks
- Follows least privilege principle
- Reduces security risk

Interview line:

```text
Delegation in Active Directory allows administrators to give limited permissions to specific users, such as allowing helpdesk staff to reset passwords for users in a specific OU.
```

---

## Password Reset Practical

In the room, I used Phillip’s account to reset Sophie’s password after delegation was configured.

Phillip login:

```text
Username: THM\phillip
Password: Claire2008
```

PowerShell command used:

```powershell
Set-ADAccountPassword sophie -Reset -NewPassword (Read-Host -AsSecureString -Prompt 'New Password') -Verbose
```

This command resets Sophie’s password.

Important learning:

```text
Set-ADAccountPassword works in PowerShell, not normal Command Prompt.
```

I first accidentally ran the command in Command Prompt and got an error.

Correct shell:

```text
PowerShell
```

Wrong shell:

```text
Command Prompt
```

---

## PowerShell Prompt Mistake

When copying commands, I must not copy the PowerShell prompt.

Wrong:

```powershell
PS C:\Users\phillip> Set-ADUser -Identity sophie -ChangePasswordAtLogon $true -Verbose
```

Correct:

```powershell
Set-ADUser -Identity sophie -ChangePasswordAtLogon $true -Verbose
```

Important:

```text
PS C:\Users\phillip> is only the prompt.
It should not be copied as part of the command.
```

---

## Set-ADUser Command

The `Set-ADUser` command is used to modify Active Directory user properties.

Example:

```powershell
Set-ADUser -Identity sophie -ChangePasswordAtLogon $true -Verbose
```

This forces the user to change password at next login.

Another example:

```powershell
Set-ADUser -Identity sophie -ChangePasswordAtLogon $false -Verbose
```

This removes the forced password change requirement.

---

## RDP Login Practical

I used RDP from AttackBox to connect to the Windows target machine.

Example command:

```bash
xfreerdp /u:THM\\phillip /p:Claire2008 /v:MACHINE_IP /cert:ignore
```

Important:

In Linux terminal, the domain username is written with double backslash:

```text
THM\\phillip
```

But in Windows login screen, it is written as:

```text
THM\phillip
```

Example Sophie login:

```bash
xfreerdp /u:THM\\sophie /p:'P@ssw0rd123!' /v:MACHINE_IP /cert:ignore
```

---

## Group Policy

Group Policy is used to centrally manage user and computer settings in a Windows domain.

Group Policy can control:

- Password policies
- Desktop settings
- Control Panel access
- Software settings
- Security settings
- Firewall settings
- Drive mappings
- Script execution
- Computer restrictions

Group Policy is applied using Group Policy Objects.

---

## Group Policy Object

GPO stands for Group Policy Object.

A GPO is a container that stores policy settings.

A GPO has two major parts:

```text
Computer Configuration
User Configuration
```

Computer Configuration applies to computers.

User Configuration applies to users.

Important concept:

```text
Creating a GPO decides the rule book name.
Editing the GPO decides what the rule actually does.
Linking the GPO decides where it applies.
```

---

## GPO Name vs GPO Setting vs GPO Link

This was an important practical lesson.

```text
GPO name    = Rule book name
GPO setting = Actual rule inside the book
GPO link    = Which users or computers receive that rule
```

Example from the room:

```text
GPO name:
Restrict Control Panel Access

Actual setting:
Prohibit access to Control Panel and PC settings

Linked to:
Management, Marketing, Sales OUs
```

---

## Restrict Control Panel Access Practical

The room required creating a GPO to block Control Panel access for non-IT users.

GPO name:

```text
Restrict Control Panel Access
```

Policy path:

```text
User Configuration
→ Policies
→ Administrative Templates
→ Control Panel
→ Prohibit access to Control Panel and PC settings
```

Setting:

```text
Enabled
```

Linked OUs:

```text
Management
Marketing
Sales
```

IT OU was not linked because IT users should still have access to Control Panel.

---

## What I Learned About GPO Linking

Creating a GPO alone does nothing until it is linked.

Editing a GPO alone only defines the setting.

A GPO must be linked to an OU, domain, or site to apply.

Example:

```text
Restrict Control Panel Access GPO
        ↓
Linked to Sales OU
        ↓
Users inside Sales receive the restriction
```

Important:

```text
Because the Control Panel restriction was under User Configuration, it needed to be linked to OUs containing users.
```

---

## Group Policy Practical Mistake

I first edited the wrong GPO.

I enabled the setting inside:

```text
Default Domain Policy
```

But the room wanted a new GPO named:

```text
Restrict Control Panel Access
```

Correct approach:

```text
Create new GPO
Edit the new GPO
Enable the Control Panel restriction
Link the GPO to required OUs
```

Important lesson:

```text
Always confirm the Group Policy Management Editor title before editing.
```

Correct title should show the intended GPO name.

---

## Authentication Methods

Authentication is the process of verifying a user or computer identity.

In Active Directory, common authentication methods include:

- Kerberos
- NTLM

---

## Kerberos

Kerberos is the default authentication protocol in modern Windows domain environments.

It uses tickets for authentication.

Basic idea:

```text
User logs in
        ↓
Domain Controller verifies identity
        ↓
User receives ticket
        ↓
Ticket is used to access services
```

Kerberos is important because it allows secure authentication without repeatedly sending the password.

Interview line:

```text
Kerberos is the default authentication protocol in Active Directory and uses tickets to authenticate users and access services.
```

---

## NTLM

NTLM is an older Microsoft authentication protocol.

It is still supported for compatibility but is weaker than Kerberos.

NTLM may be used when Kerberos is not available or cannot be used.

Interview line:

```text
NTLM is an older Windows authentication protocol, while Kerberos is the default and preferred authentication method in modern Active Directory environments.
```

---

## Trees, Forests, and Trusts

Active Directory can be structured using domains, trees, forests, and trusts.

---

## Domain

A domain is a logical group of users, computers, and resources managed together.

Example:

```text
thm.local
```

---

## Tree

A tree is a group of domains that share a continuous namespace.

Example:

```text
company.local
sales.company.local
it.company.local
```

---

## Forest

A forest is the top-level Active Directory structure.

It can contain one or more domain trees.

A forest is the largest security boundary in Active Directory.

Interview line:

```text
A forest is the highest-level Active Directory container and can contain multiple domain trees.
```

---

## Trust

A trust relationship allows users in one domain to access resources in another domain.

Trusts are useful when different domains or forests need to share access.

Example:

```text
Domain A trusts Domain B
Users from Domain B may access resources in Domain A depending on permissions
```

---

## Important Commands Practiced

### Check current user

```cmd
whoami
```

Example output:

```text
thm\phillip
```

### Start PowerShell from Command Prompt

```cmd
powershell
```

### Reset AD user password

```powershell
Set-ADAccountPassword sophie -Reset -NewPassword (Read-Host -AsSecureString -Prompt 'New Password') -Verbose
```

### Force password change at next logon

```powershell
Set-ADUser -Identity sophie -ChangePasswordAtLogon $true -Verbose
```

### Remove password change requirement

```powershell
Set-ADUser -Identity sophie -ChangePasswordAtLogon $false -Verbose
```

### RDP as Phillip

```bash
xfreerdp /u:THM\\phillip /p:Claire2008 /v:MACHINE_IP /cert:ignore
```

### RDP as Sophie

```bash
xfreerdp /u:THM\\sophie /p:'PASSWORD' /v:MACHINE_IP /cert:ignore
```

---

## Common Errors Faced

### Error 1 — Command not recognized

Reason:

```text
Set-ADAccountPassword was run inside Command Prompt instead of PowerShell.
```

Fix:

```cmd
powershell
```

Then run the command again.

---

### Error 2 — Access is denied

Reason:

```text
Phillip did not have proper delegated permission on the correct OU.
```

Fix:

```text
Delegate password reset permission to Phillip on the Sales OU.
```

---

### Error 3 — Copied PowerShell prompt

Wrong:

```powershell
PS C:\Users\phillip> Set-ADUser ...
```

Correct:

```powershell
Set-ADUser ...
```

Reason:

```text
The prompt is not part of the command.
```

---

### Error 4 — GPO existed but did nothing

Reason:

```text
The GPO was created and linked, but the actual setting inside the GPO was not configured.
```

Fix:

```text
Edit the correct GPO and enable the required policy setting.
```

---

### Error 5 — Edited wrong GPO

Reason:

```text
The setting was enabled inside Default Domain Policy instead of the new GPO.
```

Fix:

```text
Create and edit the correct GPO named Restrict Control Panel Access.
```

---

## Practical Lessons Learned

- Active Directory manages users, computers, groups, OUs, and policies.
- Domain Controllers authenticate users and computers.
- OUs help organize AD objects and apply policies.
- Delegation gives limited admin permissions.
- PowerShell is needed for AD management commands.
- A GPO must have settings configured inside it.
- A GPO must be linked to an OU/domain/site to apply.
- User Configuration settings apply to users.
- Computer Configuration settings apply to computers.
- Kerberos is the default AD authentication protocol.
- NTLM is older and less preferred than Kerberos.
- Forests, trees, and trusts are used to structure larger AD environments.

---

## Real-World IT Support Relevance

This room is useful for IT support because helpdesk teams commonly deal with:

- User password resets
- Account unlocks
- Group membership changes
- Login issues
- Domain account problems
- RDP access issues
- Policy restrictions
- Control Panel restrictions
- User permissions
- Department-based access

---

## Real-World SOC Relevance

This room is useful for SOC because Active Directory is a major target in real attacks.

SOC analysts should understand:

- Domain users
- Domain controllers
- Authentication logs
- Failed logins
- Password reset events
- Privileged accounts
- Delegated permissions
- Group Policy abuse
- Kerberos and NTLM authentication
- Domain trust relationships

---

## Interview Lines

Active Directory is a centralized directory service used to manage users, computers, groups, and policies in a Windows domain.

A Domain Controller authenticates users and computers and manages the Active Directory domain.

An OU is a container used to organize Active Directory objects and apply policies or delegation.

Delegation allows administrators to assign limited administrative tasks to specific users, such as password reset rights for a specific OU.

A GPO is a Group Policy Object used to centrally manage user and computer settings.

Creating a GPO defines the policy container, editing it defines what it does, and linking it defines where it applies.

Kerberos is the default authentication protocol in Active Directory and uses tickets.

NTLM is an older Microsoft authentication protocol used mainly for compatibility.

A forest is the highest-level Active Directory structure and can contain multiple domain trees.

A trust allows users from one domain or forest to access resources in another, depending on permissions.

---

## Final Takeaway

Active Directory is the backbone of most Windows corporate environments.

This room helped me understand how companies centrally manage users, computers, authentication, permissions, and policies.

The most important practical lessons were:

```text
Users and computers are managed centrally in AD.
OUs organize users and computers.
Delegation gives limited admin permissions.
PowerShell is used for AD user management.
GPOs must be edited and linked to work.
Kerberos and NTLM are important authentication methods.
```
