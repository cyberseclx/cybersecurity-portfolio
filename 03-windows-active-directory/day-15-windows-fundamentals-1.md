# Day 15 — Windows Fundamentals 1

## Room / Topic

TryHackMe — Windows Fundamentals 1

## Status

Completed

## What I Practiced

Today I completed Windows Fundamentals 1. This room introduced the Windows desktop environment, Windows editions, NTFS file system, System32, user accounts, permissions, User Account Control, Settings, Control Panel, and Task Manager.

This was my first Windows-focused room in the Windows and Active Directory module.

## Key Concepts

### Windows Editions

Windows comes in different editions such as Home, Pro, Enterprise, and Server editions.

For IT support and cybersecurity, editions matter because some security and management features are available only in higher editions.

Example:

```text
Windows Home = basic home-user edition
Windows Pro = business/professional edition with extra features
Windows Server = server operating system used in organizations
```

### BitLocker

BitLocker is a disk encryption feature available in Windows Pro and higher editions.

It helps protect data if a laptop or disk is lost or stolen.

Interview line:

```text
BitLocker provides full-disk encryption to protect data at rest.
```

---

## Desktop GUI

The Windows desktop is the graphical interface used to interact with the operating system.

Important parts:

```text
Desktop = main screen
Start Menu = access apps, settings, power options
Taskbar = pinned apps and running programs
Notification Area = clock, network, volume, background apps
File Explorer = browse files and folders
```

Real-world use:

```text
IT support often guides users through the desktop, Start Menu, taskbar, and File Explorer during troubleshooting.
```

---

## Windows File System

### NTFS

NTFS stands for New Technology File System.

It is the main file system used by modern Windows systems.

Important NTFS features:

```text
File and folder permissions
Encryption support
Compression
Large file support
Journaling
Alternate Data Streams
```

### FAT32

FAT32 is an older file system.

Limitations:

```text
No advanced permissions like NTFS
Maximum individual file size is 4 GB
Commonly used on USB drives and older devices
```

### Why NTFS matters for cybersecurity

NTFS permissions control who can access files and folders.

Misconfigured permissions can allow unauthorized access to sensitive files.

---

## Windows\System32 Folder

The `C:\Windows\System32` folder contains important Windows system files, executables, libraries, and tools.

Examples of important tools inside System32:

```text
cmd.exe
taskmgr.exe
notepad.exe
control.exe
services.msc
eventvwr.msc
```

Important note:

```text
System32 is critical for Windows. Deleting or modifying files here can break the operating system.
```

Real-world use:

```text
Many administrative tools and system utilities are located in System32.
```

---

## User Accounts, Profiles, and Permissions

### User Account

A user account allows a person to log in and use the system.

Types:

```text
Standard user
Administrator user
```

### Standard User

A standard user can perform normal daily tasks but cannot make major system-wide changes without administrator approval.

### Administrator

An administrator can install software, change system settings, manage users, and perform privileged actions.

### User Profile

A user profile stores user-specific files and settings.

Example path:

```text
C:\Users\Username
```

Common profile folders:

```text
Desktop
Documents
Downloads
Pictures
AppData
```

### Permissions

Permissions define what a user or group can do with files and folders.

Examples:

```text
Read
Write
Modify
Full Control
```

Security importance:

```text
Incorrect permissions can expose sensitive data or allow unauthorized changes.
```

---

## User Account Control

User Account Control, or UAC, is a Windows security feature that asks for confirmation before allowing privileged actions.

Example:

```text
Installing software
Changing system settings
Running an app as administrator
```

Why UAC exists:

```text
It helps prevent unauthorized or accidental system-level changes.
```

Cybersecurity relevance:

```text
UAC prompts can indicate privilege elevation attempts.
```

---

## Settings and Control Panel

Windows has both Settings and Control Panel.

### Settings

Modern interface for managing Windows options.

Used for:

```text
Accounts
Network
Updates
Privacy
Apps
System settings
```

### Control Panel

Older administrative interface still used for many advanced settings.

Used for:

```text
Programs and Features
Network and Sharing Center
User Accounts
System tools
Administrative settings
```

Real-world use:

```text
IT support engineers often use both Settings and Control Panel depending on the issue.
```

---

## Task Manager

Task Manager is used to view and manage running processes, performance, startup apps, users, and services.

Useful tabs:

```text
Processes
Performance
App history
Startup
Users
Details
Services
```

Common use cases:

```text
Check high CPU usage
Check high memory usage
End unresponsive programs
Review startup applications
Identify suspicious processes
Check running services
```

Cybersecurity relevance:

```text
Task Manager can help identify unusual processes, suspicious resource usage, or unknown applications running on a system.
```

---

## Commands / Tools Mentioned

```text
System Information
File Explorer
Control Panel
Settings
Task Manager
System32
UAC prompt
```

Useful Windows tools:

```text
taskmgr.exe
control.exe
cmd.exe
services.msc
eventvwr.msc
msinfo32.exe
```

---

## Important Takeaways

* Windows is widely used in corporate environments, so attackers often target it.
* Windows Pro includes features like BitLocker that are not available in Home edition.
* NTFS is important because it supports permissions and security features.
* System32 contains critical Windows system files and tools.
* User accounts and permissions are key to Windows security.
* UAC helps protect the system from unauthorized privilege changes.
* Task Manager is useful for troubleshooting and basic security investigation.
* Settings and Control Panel are both important for system administration.

---

## Real-World Use

This room is useful for:

```text
IT support
Windows troubleshooting
SOC analyst basics
Endpoint security
User permission issues
System administration
Active Directory preparation
```

Examples:

```text
Use Task Manager to check suspicious processes.
Use NTFS permissions to control file access.
Use UAC to prevent unauthorized admin actions.
Use BitLocker to protect data on lost/stolen devices.
Use Control Panel or Settings to troubleshoot user issues.
```

---

## Interview Lines

### Windows Editions

Windows editions matter because business editions like Pro and Enterprise include advanced security and management features such as BitLocker, domain join, and enterprise controls.

### NTFS

NTFS is the modern Windows file system that supports permissions, encryption, compression, large files, and other security features.

### UAC

UAC helps prevent unauthorized system changes by requiring approval before privileged actions are performed.

### Task Manager

Task Manager is used to monitor processes, performance, startup programs, users, and services, making it useful for troubleshooting and basic security checks.

---

## Confidence Level

Comfortable with basic Windows GUI, editions, NTFS, System32, users, UAC, Settings, Control Panel, and Task Manager.
