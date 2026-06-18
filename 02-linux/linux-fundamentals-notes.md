# Linux Fundamentals Notes

## Overview

These notes document the Linux fundamentals I practiced through Hack The Box Linux Fundamentals, TryHackMe learning, and my local Kali Linux virtual machine.

## Commands Practiced

| Command  | Purpose                                                                 |
| -------- | ----------------------------------------------------------------------- |
| `pwd`    | Shows the current working directory                                     |
| `ls`     | Lists files and directories                                             |
| `ls -la` | Shows detailed file information, including hidden files and permissions |
| `cd`     | Changes the current directory                                           |
| `mkdir`  | Creates a directory                                                     |
| `touch`  | Creates an empty file                                                   |
| `cp`     | Copies files or directories                                             |
| `mv`     | Moves or renames files and directories                                  |
| `rm`     | Removes files or directories                                            |
| `cat`    | Reads and displays file content                                         |
| `whoami` | Shows the current logged-in user                                        |
| `id`     | Shows user ID, group ID and group membership                            |
| `chmod`  | Changes file permissions                                                |
| `chown`  | Changes file ownership                                                  |

## Linux Concepts I Understand

### Root User

The `root` user is the most privileged user in Linux. Root can read, modify, install, remove and change almost anything on the system.

Because root has extensive permissions, using it carelessly can damage the operating system, expose sensitive files or create security risks. A normal user should only use elevated privileges when required.

### Users and Groups

Linux uses users and groups to control who can access files, directories and system resources.

A user can belong to one or more groups. Permissions are often assigned based on the file owner, the file group and all other users.

### File Permissions

Linux permissions are usually shown as:

```text
-rw-r-----
```

This can be divided into:

```text
Owner | Group | Others
rw-   | r--   | ---
```

* `r` means read
* `w` means write
* `x` means execute
* `-` means that permission is not granted

For example:

```bash
chmod 640 test.txt
```

This means:

* Owner: read and write
* Group: read only
* Others: no permissions

## Commands Tested in My Local Kali Linux VM

```bash
mkdir -p ~/portfolio-labs/linux-practice
cd ~/portfolio-labs/linux-practice

pwd
whoami
id

mkdir files
touch files/test.txt
ls -la files

chmod 640 files/test.txt
ls -l files/test.txt

cat /etc/passwd | head
```

## What I Learned

* Linux file permissions are a core security control because they restrict who can read, change or execute files.
* Root access is powerful and should follow the principle of least privilege.
* `ls -l` is useful for checking ownership and permissions before troubleshooting access issues.
* Users, groups and file permissions are important concepts for Linux administration, SOC investigations and privilege-escalation analysis.
* I need more practice with ownership, services, processes, logs and Bash scripting.

## Next Linux Topics

* File ownership with `chown` and `chgrp`
* Processes with `ps`, `top` and `htop`
* Services with `systemctl`
* Log files in `/var/log`
* Network commands such as `ip a`, `ss`, `ping`, `curl` and `wget`
* Bash scripting basics
