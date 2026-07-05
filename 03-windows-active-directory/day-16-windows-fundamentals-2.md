# Day 16 — Windows Fundamentals 2

## Room / Topic

TryHackMe — Windows Fundamentals 2

## Status

Completed

## What I Practiced

Today I completed Windows Fundamentals 2.

This room focused on important Windows administrative tools and system utilities used for troubleshooting, monitoring, configuration, and basic security investigation.

Topics covered:

- System Configuration
- UAC Settings
- Computer Management
- System Information
- Resource Monitor
- Command Prompt
- Registry Editor

---

## System Configuration

System Configuration is a Windows tool used to manage startup behavior, boot settings, services, and troubleshooting options.

Tool name:

```text
msconfig
```

How to open:

```text
Run → msconfig
```

Common use cases:

- Troubleshoot startup issues
- Enable or disable startup services
- Change boot options
- Perform diagnostic startup
- Check system services

Important tabs:

- General
- Boot
- Services
- Startup
- Tools

### Security / IT Support Relevance

System Configuration is useful when troubleshooting slow startup, unwanted services, or suspicious programs that may start with Windows.

---

## UAC Settings

UAC stands for User Account Control.

UAC helps prevent unauthorized system-level changes by asking for confirmation before allowing privileged actions.

Examples of actions that may trigger UAC:

- Installing software
- Changing system settings
- Running a program as administrator
- Modifying protected areas of Windows

### Interview Line

UAC is a Windows security feature that prompts for approval before allowing privileged actions.

---

## Computer Management

Computer Management is a Windows administrative console that contains multiple system management tools in one place.

Tool name:

```text
compmgmt.msc
```

Important sections:

- Task Scheduler
- Event Viewer
- Shared Folders
- Local Users and Groups
- Performance
- Device Manager
- Disk Management
- Services and Applications

---

## Local Users and Groups

Local Users and Groups allows administrators to manage user accounts and groups on a local Windows machine.

Useful for:

- Creating users
- Disabling users
- Managing group membership
- Checking administrator accounts
- Reviewing local user permissions

Security relevance:

- Unexpected administrator users can be a security risk.
- User group membership should be reviewed during investigations.

---

## Event Viewer

Event Viewer stores Windows logs.

Tool name:

```text
eventvwr.msc
```

Common log categories:

- Application
- Security
- Setup
- System
- Forwarded Events

Security relevance:

- Login activity
- Failed login attempts
- Service failures
- Application errors
- System crashes
- Suspicious activity

Event Viewer is important for IT support, SOC analysis, and troubleshooting.

---

## Device Manager

Device Manager shows hardware devices and drivers installed on the system.

Tool name:

```text
devmgmt.msc
```

Useful for:

- Checking driver issues
- Disabling or enabling devices
- Troubleshooting hardware problems
- Viewing unknown devices

Example issues:

- Network adapter not working
- Audio driver missing
- USB device not detected
- Display driver issue

---

## Disk Management

Disk Management is used to manage disks, partitions, and volumes.

Tool name:

```text
diskmgmt.msc
```

Useful for:

- Creating partitions
- Formatting drives
- Changing drive letters
- Checking disk layout
- Managing attached storage

Security / support relevance:

Disk Management is useful when checking connected drives, storage issues, or suspicious mounted volumes.

---

## Services

Services are background programs that run on Windows.

Tool name:

```text
services.msc
```

Services can be:

- Running
- Stopped
- Disabled
- Automatic
- Manual

Use cases:

- Restart a failed service
- Disable unnecessary services
- Check suspicious services
- Troubleshoot application issues

Security relevance:

Malware can create or abuse Windows services for persistence.

---

## System Information

System Information shows detailed information about the Windows system.

Tool name:

```text
msinfo32
```

Information shown:

- OS name
- OS version
- System manufacturer
- System model
- Processor
- BIOS version
- Installed RAM
- Boot device
- Network adapter information
- Running environment details

IT support use:

System Information is useful when checking system specifications, OS version, hardware details, and troubleshooting compatibility issues.

---

## Resource Monitor

Resource Monitor provides detailed information about system resource usage.

Tool name:

```text
resmon
```

Main tabs:

- CPU
- Memory
- Disk
- Network

Use cases:

- Check high CPU usage
- Check high memory usage
- Check disk activity
- Check network connections
- Identify processes consuming resources

Security relevance:

Resource Monitor can help identify suspicious processes using high CPU, disk, memory, or network activity.

---

## Command Prompt

Command Prompt is a Windows command-line tool.

Tool name:

```text
cmd.exe
```

Common commands:

```cmd
whoami
hostname
ipconfig
ping
net user
net localgroup
systeminfo
tasklist
taskkill
dir
cd
cls
```

Examples:

```cmd
whoami
```

Shows the current user.

```cmd
hostname
```

Shows the computer name.

```cmd
ipconfig
```

Shows IP configuration.

```cmd
systeminfo
```

Shows system details.

```cmd
tasklist
```

Shows running processes.

### Security / SOC Relevance

Command Prompt is useful for quick investigation, checking users, network settings, running processes, and system information.

---

## Registry Editor

The Windows Registry is a database that stores Windows and application configuration settings.

Tool name:

```text
regedit
```

Main registry hives:

- HKEY_CLASSES_ROOT
- HKEY_CURRENT_USER
- HKEY_LOCAL_MACHINE
- HKEY_USERS
- HKEY_CURRENT_CONFIG

Important warning:

Incorrect registry changes can break Windows or installed applications.

Security relevance:

Attackers may use registry keys for persistence. Startup entries and autorun locations are important during malware investigation.

Examples of registry use:

- System configuration
- User settings
- Application settings
- Startup persistence
- Security settings

---

## Important Windows Tools Learned

| Tool | Purpose |
|---|---|
| `msconfig` | System Configuration |
| `compmgmt.msc` | Computer Management |
| `eventvwr.msc` | Event Viewer |
| `devmgmt.msc` | Device Manager |
| `diskmgmt.msc` | Disk Management |
| `services.msc` | Services |
| `msinfo32` | System Information |
| `resmon` | Resource Monitor |
| `cmd.exe` | Command Prompt |
| `regedit` | Registry Editor |

---

## Real-World Use

This room is useful for:

- IT support
- Windows troubleshooting
- SOC analyst basics
- Endpoint investigation
- System administration
- Active Directory preparation
- Malware investigation basics

Examples:

- Use Event Viewer to check failed logins or system errors.
- Use Services to check suspicious background services.
- Use Resource Monitor to check unusual CPU, memory, disk, or network usage.
- Use System Information to check OS and hardware details.
- Use Registry Editor carefully when investigating persistence or configuration issues.
- Use Command Prompt for quick system and network checks.

---

## Key Takeaways

- Windows includes many built-in tools for administration and troubleshooting.
- `msconfig` helps troubleshoot startup and service issues.
- Computer Management combines multiple admin tools in one console.
- Event Viewer is important for logs and investigations.
- Services are important for system functionality and can also be abused by attackers.
- Resource Monitor helps identify resource usage and network activity.
- Command Prompt is useful for quick checks and troubleshooting.
- Registry Editor is powerful but risky; incorrect changes can damage the system.

---

## Interview Lines

System Configuration is used to manage startup behavior, boot options, and services for troubleshooting.

Computer Management is a Windows console that provides access to tools like Event Viewer, Local Users and Groups, Device Manager, Disk Management, and Services.

Event Viewer is used to review Windows logs such as application, system, and security events.

Resource Monitor helps analyze CPU, memory, disk, and network usage by processes.

The Windows Registry stores system and application configuration settings, and attackers may abuse registry keys for persistence.

Command Prompt is useful for checking system information, users, processes, and network configuration.
