# Day 19 — Windows Command Line

## Room / Topic

TryHackMe — Windows Command Line

## Status

Completed

---

## What I Practiced

Today I completed the Windows Command Line room.

This room focused on using `cmd.exe`, the default Windows command-line interpreter, for basic system information, network troubleshooting, file and disk management, and process management.

Topics covered:

- Command Prompt basics
- Basic system information
- Network troubleshooting
- File and folder management
- Disk management basics
- Task and process management
- Reading file contents
- Using wildcards
- Understanding paths

This room is useful for:

- IT Support
- SOC Analyst L1
- Windows Admin
- System Admin Trainee
- Troubleshooting
- Incident investigation

---

## Why Command Line Is Useful

Command-line tools are useful because they are fast, lightweight, and scriptable.

CLI advantages:

- Lower resource usage
- Faster troubleshooting
- Automation through scripts
- Remote management
- Works well on servers and low-resource systems
- Useful when GUI access is unavailable

Interview line:

The command line is useful because it allows faster troubleshooting, automation, and remote administration with fewer system resources than a GUI.

---

## Default Windows Command Line Interpreter

The default command-line interpreter in Windows is:

```text
cmd.exe
```

`cmd.exe` is also called Command Prompt.

---

## Basic System Information Commands

### hostname

Shows the computer name.

```cmd
hostname
```

Use case:

- Identify the current system
- Confirm which machine you are connected to

---

### whoami

Shows the currently logged-in user.

```cmd
whoami
```

Example output:

```text
thm\user
```

Use case:

- Confirm current user context
- Check whether the user is local or domain-based
- Useful during troubleshooting and privilege checks

---

### ver

Shows the Windows version.

```cmd
ver
```

Use case:

- Quickly check OS version from Command Prompt

---

### systeminfo

Shows detailed system information.

```cmd
systeminfo
```

It can show:

- OS name
- OS version
- System manufacturer
- System model
- BIOS version
- Boot time
- Installed hotfixes
- Network card information
- Domain/workgroup information

Use case:

- Inventory
- Troubleshooting
- Patch checking
- System investigation

---

## Network Troubleshooting Commands

### ipconfig

Shows basic IP configuration.

```cmd
ipconfig
```

It can show:

- IPv4 address
- Subnet mask
- Default gateway

Use case:

- Check whether a system has an IP address
- Check gateway information
- Troubleshoot network connectivity

---

### ipconfig /all

Shows detailed network adapter information.

```cmd
ipconfig /all
```

It can show:

- MAC address
- DHCP status
- DNS servers
- Lease information
- Adapter details
- Default gateway
- IPv4 and IPv6 information

Use case:

- Troubleshoot DHCP
- Check DNS settings
- Check MAC address
- Verify adapter configuration

---

### ping

Tests basic reachability using ICMP.

```cmd
ping 8.8.8.8
```

Example:

```cmd
ping google.com
```

Use case:

- Test if a host is reachable
- Check packet loss
- Check basic latency

Important:

If IP ping works but domain name ping fails, DNS may be the problem.

---

### tracert

Shows the route/path packets take to a destination.

```cmd
tracert google.com
```

Use case:

- Identify where traffic may be failing
- Troubleshoot routing path issues
- Check hops between source and destination

---

### nslookup

Queries DNS records.

```cmd
nslookup google.com
```

Use case:

- Check if DNS resolution is working
- Find IP address for a domain name
- Troubleshoot name resolution issues

---

### netstat

Shows network connections and listening ports.

```cmd
netstat
```

Useful option:

```cmd
netstat -ano
```

`netstat -ano` can show:

- Active connections
- Listening ports
- Protocol
- Local address
- Foreign address
- Connection state
- PID

Use case:

- Check active network connections
- Identify listening ports
- Map network connections to processes

---

## File and Folder Management

### dir

Lists files and folders in the current directory or specified path.

```cmd
dir
```

Example:

```cmd
dir C:\Treasure\Hunt
```

Important:

`dir` shows what files exist inside a folder. It does not show file contents.

Use case:

- List files and folders
- Check file names
- Check file size and timestamps

---

### cd

Changes directory.

```cmd
cd C:\Users
```

Move to root of current drive:

```cmd
cd \
```

Move one directory up:

```cmd
cd ..
```

Use case:

- Navigate folders from Command Prompt

---

### mkdir

Creates a new directory.

```cmd
mkdir test-folder
```

Use case:

- Create folders from CLI

---

### copy

Copies files.

```cmd
copy source.txt destination.txt
```

Example:

```cmd
copy file.txt C:\Backup
```

Use case:

- Copy files from one location to another

---

### move

Moves or renames files.

```cmd
move old.txt new.txt
```

Example:

```cmd
move file.txt C:\Backup
```

Use case:

- Move files
- Rename files

---

### del

Deletes files.

```cmd
del file.txt
```

Use case:

- Remove files from CLI

Important:

Use carefully because deleted files may not always go to Recycle Bin when deleted from command line.

---

### type

Shows the content of a text file.

```cmd
type file.txt
```

Example:

```cmd
type C:\Treasure\Hunt\file.txt
```

Important:

`dir` shows the file name.

`type` shows what is written inside the file.

Memory line:

```text
dir = show files in folder
type = show file contents
```

---

## Understanding File Paths

### Drive Letter

Windows uses drive letters such as:

```text
C:
D:
E:
```

Example:

```text
C:\
```

means the root of the C drive.

---

### Folder Path

Example:

```text
C:\Treasure\Hunt
```

This means:

```text
C:\
└── Treasure
    └── Hunt
```

`C:\Treasure\Hunt` is a folder path.

The actual file is inside that folder.

Example full file path:

```text
C:\Treasure\Hunt\secret.txt
```

---

### How To Find and Read a File

Step 1: List the folder.

```cmd
dir C:\Treasure\Hunt
```

Step 2: Read the file shown by `dir`.

```cmd
type C:\Treasure\Hunt\filename.txt
```

---

## Wildcards

Wildcards allow matching multiple files.

### Asterisk Wildcard

`*` means match anything.

Example:

```cmd
copy *.md C:\Markdown
```

This copies all files ending in `.md` to `C:\Markdown`.

Other examples:

```cmd
dir *.txt
dir test*
```

Use case:

- Match multiple files
- Copy files by extension
- Search/list files by pattern

---

## Disk Management Commands

### chkdsk

Checks the file system and disk for errors.

```cmd
chkdsk
```

Use case:

- Disk troubleshooting
- File system checks

---

### tree

Shows folder structure in a tree format.

```cmd
tree
```

Example:

```cmd
tree C:\Users
```

Use case:

- Understand folder hierarchy
- Visualize directory structure

---

## Task and Process Management

### tasklist

Shows running processes.

```cmd
tasklist
```

Use case:

- Check running applications/processes
- Identify process names and PIDs

---

### taskkill

Terminates a running process.

```cmd
taskkill /PID 1234
```

Force kill:

```cmd
taskkill /PID 1234 /F
```

Kill by image name:

```cmd
taskkill /IM notepad.exe /F
```

Use case:

- Stop hung applications
- Kill suspicious or unwanted processes
- Troubleshoot process issues

---

## Important Command Meanings

| Command | Purpose |
|---|---|
| cmd.exe | Default Windows command-line interpreter |
| hostname | Shows computer name |
| whoami | Shows current logged-in user |
| ver | Shows Windows version |
| systeminfo | Shows detailed system information |
| ipconfig | Shows IP configuration |
| ipconfig /all | Shows detailed adapter configuration |
| ping | Tests reachability |
| tracert | Shows route/path to destination |
| nslookup | Tests DNS resolution |
| netstat | Shows network connections and listening ports |
| dir | Lists files and folders |
| cd | Changes directory |
| mkdir | Creates directory |
| copy | Copies files |
| move | Moves or renames files |
| del | Deletes files |
| type | Shows text file contents |
| tree | Shows directory tree |
| chkdsk | Checks disk/file system |
| tasklist | Lists running processes |
| taskkill | Kills running processes |

---

## Troubleshooting Thinking

### User Has No Internet

Check:

```cmd
ipconfig
ping default-gateway
ping 1.1.1.1
nslookup google.com
tracert google.com
```

Possible issues:

- No IP address
- DHCP issue
- Gateway issue
- DNS issue
- Routing issue
- Firewall or ISP issue

---

### Website Name Does Not Work But IP Works

If this works:

```cmd
ping 1.1.1.1
```

But this fails:

```cmd
ping google.com
```

Then DNS may be failing.

Use:

```cmd
nslookup google.com
```

---

### Need To Check Running Processes

Use:

```cmd
tasklist
```

Then kill a process if needed:

```cmd
taskkill /PID process_id /F
```

---

### Need To Read a File

Use:

```cmd
dir folder_path
type full_file_path
```

Example:

```cmd
dir C:\Treasure\Hunt
type C:\Treasure\Hunt\filename.txt
```

---

## Mistake I Clarified

I first wanted to know where the Treasure file was.

Important understanding:

```text
C:\Treasure\Hunt is a folder path.
The file is inside that folder.
```

To find the file name:

```cmd
dir C:\Treasure\Hunt
```

To read it:

```cmd
type C:\Treasure\Hunt\filename.txt
```

---

## Real-World IT Support Relevance

This room is useful for IT support because common support tasks often require command-line troubleshooting.

Examples:

- Check current user
- Check hostname
- Check IP configuration
- Troubleshoot DNS
- Test connectivity
- View running processes
- Kill stuck applications
- Navigate folders
- Read log/text files
- Copy/move/delete files

---

## Real-World SOC Relevance

This room is useful for SOC because analysts often inspect Windows systems using command-line tools.

SOC use cases:

- Check current user context
- Identify host information
- Review network connections
- Check running processes
- Investigate suspicious ports
- Read files from known paths
- Collect quick system information
- Troubleshoot compromised endpoints

---

## Weak Areas To Revise

- Difference between folder path and file path
- `dir` vs `type`
- Wildcards
- `netstat -ano`
- `tasklist`
- `taskkill`
- `tracert`
- `nslookup`

---

## Interview Lines

`cmd.exe` is the default command-line interpreter in Windows.

`ipconfig` shows IP address, subnet mask, and default gateway.

`ipconfig /all` shows detailed adapter information including MAC address, DNS, and DHCP details.

`ping` tests basic reachability.

`tracert` shows the route packets take to a destination.

`nslookup` is used to troubleshoot DNS resolution.

`netstat -ano` shows active connections, listening ports, and process IDs.

`dir` lists files and folders.

`type` displays the contents of a text file.

`tasklist` shows running processes.

`taskkill` terminates a process by PID or image name.

A folder path points to a directory, while a file path points to a specific file.

---

## Final Takeaway

The Windows command line is important for fast troubleshooting and system investigation.

This room helped me practice commands for:

- System information
- Network troubleshooting
- File management
- Disk checks
- Process management

The most important practical lesson was:

```text
Use dir to find files.
Use type to read file contents.
Use ipconfig, ping, tracert, nslookup, and netstat for network troubleshooting.
Use tasklist and taskkill for process management.
```
