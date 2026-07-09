# Day 20 — TryHackMe Windows PowerShell

## GitHub Path

`04-command-line/day-20-windows-powershell.md`

## Room

```text
TryHackMe Cyber Security 101
Module: Command Line
Room: Windows PowerShell
```

## Clockify Block

```text
D20-B02 | THM Windows PowerShell | Guided Room
```

## Room Goal

The goal of this room was to understand the basics of Windows PowerShell, how it differs from Command Prompt, and how it can be used for system administration, investigation, automation, and cybersecurity tasks.

## What is PowerShell?

PowerShell is a Windows command-line shell and scripting language.

It is used for:

```text
Windows administration
System information gathering
File and folder management
Process and service management
Network troubleshooting
Automation
Security investigation
Active Directory administration
```

## PowerShell vs CMD

```text
CMD = mostly text-based command line
PowerShell = object-based shell and scripting language
```

PowerShell commands return objects, not just plain text. This makes it powerful for filtering, sorting, selecting, and automation.

## Cmdlet Structure

PowerShell commands are called cmdlets.

Most cmdlets follow a Verb-Noun format:

```powershell
Get-Process
Get-Service
Get-ChildItem
Set-Location
Get-Content
Select-String
Sort-Object
Where-Object
```

Example:

```powershell
Get-Process
```

Meaning:

```text
Get the list of running processes.
```

## Important Discovery Commands

### Get-Command

```powershell
Get-Command
Get-Command *Process*
```

Used to discover available commands.

### Get-Help

```powershell
Get-Help Get-Process
Get-Help Get-Process -Examples
```

Used to read help for a cmdlet.

### Get-Alias

```powershell
Get-Alias
```

Used to see aliases.

Examples:

```text
ls  = Get-ChildItem
cd  = Set-Location
cat = Get-Content
pwd = Get-Location
```

## Navigation Commands

```powershell
Get-Location
Set-Location C:\Users
Get-ChildItem
```

Aliases:

```powershell
pwd
cd
ls
dir
```

## File and Folder Management

```powershell
New-Item -ItemType Directory -Name test
New-Item -ItemType File -Name notes.txt
Get-Content notes.txt
Copy-Item notes.txt backup.txt
Move-Item backup.txt .\test\
Remove-Item notes.txt
```

## Searching Content

```powershell
Select-String -Path file.txt -Pattern "error"
```

Meaning:

```text
Search for the word error inside file.txt.
```

This is similar to grep in Linux.

## Piping in PowerShell

The pipe `|` sends output from one command into another command.

```powershell
Get-Process | Sort-Object CPU -Descending
```

Meaning:

```text
Get all processes and sort them by CPU usage.
```

## Filtering with Where-Object

```powershell
Get-Process | Where-Object {$_.CPU -gt 100}
```

Meaning:

```text
Show processes where CPU usage is greater than 100.
```

Important:

```text
$_ represents the current object in the pipeline.
-gt means greater than.
```

Common comparison operators:

```text
-eq = equal
-ne = not equal
-gt = greater than
-lt = less than
-ge = greater than or equal
-le = less than or equal
-like = wildcard match
-match = regex match
```

## Sorting with Sort-Object

```powershell
Get-Process | Sort-Object CPU -Descending
```

## Selecting Output with Select-Object

```powershell
Get-Process | Select-Object Name, Id, CPU
```

## Process Commands

```powershell
Get-Process
Get-Process | Where-Object {$_.ProcessName -like "*chrome*"}
Stop-Process -Name notepad
Stop-Process -Id <PID>
```

## Service Commands

```powershell
Get-Service
Get-Service | Where-Object {$_.Status -eq "Running"}
Get-Service | Where-Object {$_.Status -eq "Stopped"}
```

## System Information

```powershell
Get-ComputerInfo
Get-Process
Get-Service
Get-Date
Get-Location
```

## Network Information

```powershell
Get-NetIPConfiguration
Get-NetIPAddress
Get-NetTCPConnection
Test-Connection google.com
```

`Test-Connection` is similar to `ping`.

## Security and SOC Use Cases

PowerShell is useful in cybersecurity because it can help investigate:

```text
Running processes
Suspicious services
Network connections
System configuration
File contents
Event logs
User activity
Automation scripts
```

Examples:

```powershell
Get-Process
Get-Service
Get-NetTCPConnection
Select-String -Path .\log.txt -Pattern "failed"
```

## Basic Scripting Concepts

PowerShell scripts usually use the `.ps1` extension.

```powershell
Write-Output "Hello PowerShell"
```

Variables use `$`:

```powershell
$name = "Rohit"
Write-Output $name
```

## Important Commands Learned

```powershell
Get-Command
Get-Help
Get-Alias
Get-Location
Set-Location
Get-ChildItem
New-Item
Copy-Item
Move-Item
Remove-Item
Get-Content
Select-String
Where-Object
Sort-Object
Select-Object
Get-Process
Stop-Process
Get-Service
Get-NetIPConfiguration
Get-NetIPAddress
Get-NetTCPConnection
Test-Connection
```

## Common Aliases

```text
pwd  = Get-Location
cd   = Set-Location
ls   = Get-ChildItem
dir  = Get-ChildItem
cat  = Get-Content
cls  = Clear-Host
```

## Mistakes / Things to Remember

```text
PowerShell commands are usually Verb-Noun.
PowerShell output is object-based, not only text.
Use Get-Help when stuck.
Use Get-Command to discover commands.
Use Get-Alias to understand Linux/CMD-like shortcuts.
Use Where-Object for filtering.
Use Sort-Object for sorting.
Use Select-Object to choose columns/properties.
Select-String is similar to grep.
Test-Connection is similar to ping.
```

## Weak Areas to Revise

```text
Where-Object syntax
PowerShell comparison operators
PowerShell pipeline
Difference between object output and text output
Get-NetTCPConnection output
Basic scripting syntax
```

## Final Summary

```text
Completed TryHackMe Windows PowerShell room.
Understood PowerShell basics, cmdlet structure, aliases, navigation, file handling, piping, filtering, sorting, process/service commands, network commands, and scripting basics.
This room supports Windows administration, SOC analysis, and future Active Directory work.
```
