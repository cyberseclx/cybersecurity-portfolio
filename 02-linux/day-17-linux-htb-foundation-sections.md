# Day 17 — Linux Foundation Sections

## Status

Completed

---

## Topics Revised

Today I revised the foundation sections of Linux.

Topics covered:

- Linux structure
- Linux distributions
- Linux kernel
- Shell
- Bash
- Linux prompt
- Getting help
- System information
- Navigation
- Files and directories

---

## Linux

Linux is an open-source operating system kernel.

Many operating systems are built using the Linux kernel.

These operating systems are called Linux distributions.

Examples:

- Debian
- Ubuntu
- Kali Linux
- Fedora
- Arch
- CentOS

---

## Linux Kernel

The kernel is the core part of the operating system.

It manages:

- Hardware
- Memory
- Processes
- Devices
- System resources

Simple flow:

User → Shell → Kernel → Hardware

---

## Shell

The shell is a command-line interface.

It allows users to interact with the operating system by running commands.

---

## Bash

Bash is a type of Linux shell.

Bash stands for:

Bourne Again Shell

---

## Linux Distribution

A Linux distribution is an operating system built using:

- Linux kernel
- System tools
- Package manager
- Default software
- Desktop environment or command-line tools

Kali Linux is a Debian-based Linux distribution focused on penetration testing, security auditing, and digital forensics.

---

## Important Linux Directories

| Directory | Purpose |
|---|---|
| / | Root directory. Everything starts from here |
| /home | User home directories |
| /etc | System-wide configuration files |
| /var | Variable data that changes frequently |
| /var/log | System and application log files |
| /tmp | Temporary files |
| /bin | Essential user command binaries |
| /sbin | System administration binaries |
| /usr | Installed programs, libraries, documentation, and shared resources |

---

## Important Notes

`/home` is used for user personal files.

`/usr` is not the user home directory.

`/usr` stores installed applications and shared resources.

`/etc` is important because it stores configuration files.

`/var/log` is important for troubleshooting and SOC investigation.

---

## Linux Prompt

The Linux prompt usually shows:

- Username
- Hostname
- Current directory
- Privilege symbol

Example:

```text
kali@kali-vm:~$
