# Day 16 — Linux Ownership, sudo, and Groups

## Topic

Linux ownership, group ownership, sudo privileges, `chown`, `chgrp`, and ownership verification using `ls -la` and `stat`.

## Status

Completed

---

## Commands Practiced

```bash
whoami
id
groups
sudo -l
mkdir -p ~/ownership-practice
cd ~/ownership-practice
touch owner-test.txt
ls -la
stat owner-test.txt
sudo chown root:root owner-test.txt
ls -la
stat owner-test.txt
sudo chown kali:kali owner-test.txt
ls -la
stat owner-test.txt
```

---

## Current User

The `whoami` command shows the current logged-in user.

```bash
whoami
```

Output:

```text
kali
```

This means the current user is `kali`.

---

## User ID and Group Membership

The `id` command shows the current user's UID, GID, and group memberships.

```bash
id
```

Important output:

```text
uid=1000(kali)
gid=1000(kali)
groups=1000(kali),27(sudo),119(wireshark)
```

Meaning:

```text
uid = user ID
gid = primary group ID
groups = groups the user belongs to
```

Important groups:

- `sudo` = allows the user to run commands with elevated/root privileges using `sudo`
- `wireshark` = allows packet capture or Wireshark-related permissions
- `adm` = may allow access to some system logs
- `vboxsf` = VirtualBox shared folder access

---

## sudo Privileges

The `sudo -l` command lists what commands the current user is allowed to run with sudo.

```bash
sudo -l
```

Observed output:

```text
User kali may run the following commands on kali-vm1:
    (ALL : ALL) ALL
```

Meaning:

The `kali` user can run all commands as any user and any group using `sudo`.

Simple meaning:

```text
kali can run administrative/root-level commands using sudo.
```

---

## Owner User vs Owner Group

Every Linux file has:

- Owner user
- Owner group
- Others

Example:

```text
-rw-r--r-- 1 kali kali 0 test.txt
```

Meaning:

```text
First kali  = owner user
Second kali = owner group
```

The owner user is the specific user that owns the file.

The owner group is the group assigned to the file. Users who are members of that group can use the group permissions.

---

## Initial File Ownership

I created a test file:

```bash
touch owner-test.txt
```

Then checked it:

```bash
ls -la
```

Output:

```text
-rw-rw-r-- 1 kali kali 0 owner-test.txt
```

Meaning:

```text
Owner user  = kali
Owner group = kali
Permissions = rw-rw-r--
```

Then I checked detailed file metadata:

```bash
stat owner-test.txt
```

Output:

```text
Access: (0664/-rw-rw-r--)
Uid: (1000/kali)
Gid: (1000/kali)
```

Meaning:

```text
UID 1000 = kali user
GID 1000 = kali group
```

---

## Changing Ownership to root

Command:

```bash
sudo chown root:root owner-test.txt
```

This changed both the owner user and owner group to `root`.

Checked with:

```bash
ls -la
```

Output:

```text
-rw-rw-r-- 1 root root 0 owner-test.txt
```

Meaning:

```text
Owner user  = root
Owner group = root
```

Checked with:

```bash
stat owner-test.txt
```

Output:

```text
Uid: (0/root)
Gid: (0/root)
```

Meaning:

```text
UID 0 = root user
GID 0 = root group
```

---

## Changing Ownership Back to kali

Command:

```bash
sudo chown kali:kali owner-test.txt
```

This changed the file ownership back to the `kali` user and `kali` group.

Checked with:

```bash
ls -la
```

Output:

```text
-rw-rw-r-- 1 kali kali 0 owner-test.txt
```

Checked with:

```bash
stat owner-test.txt
```

Output:

```text
Uid: (1000/kali)
Gid: (1000/kali)
```

Meaning:

The file owner and group were restored back to `kali`.

---

## chmod vs chown vs chgrp

### chmod

`chmod` changes file or directory permissions.

Example:

```bash
chmod 644 file.txt
```

It controls:

- Read
- Write
- Execute

### chown

`chown` changes the owner user and/or owner group.

Example:

```bash
sudo chown root:root file.txt
```

Meaning:

```text
Owner user  = root
Owner group = root
```

### chgrp

`chgrp` changes only the group ownership of a file or directory.

Example:

```bash
sudo chgrp sudo file.txt
```

Important correction:

```text
chgrp does not rename a group.
chgrp changes which group owns the file or directory.
```

---

## Permission Denied

A `Permission denied` error happens when the current user does not have the required permission.

Common reasons:

- No read permission
- No write permission
- No execute/traverse permission
- File is owned by another user
- Action requires root privileges
- Directory permissions block access

Example:

```text
A normal user may not be allowed to edit a root-owned system file without sudo.
```

---

## My Folder Organization

I moved practice folders under my cybersecurity project folder.

Current structure:

```text
/home/kali/cyber_project/kali_practise/
├── ownership-practice
├── permissions-practice
└── portfolio-labs
```

This keeps Kali practical work organized in one place.

---

## Key Takeaways

- `whoami` shows the current user.
- `id` shows UID, GID, and group memberships.
- `groups` shows which groups the current user belongs to.
- `sudo -l` shows what commands the current user can run with sudo.
- The `sudo` group allows elevated/root-level command execution.
- Every Linux file has an owner user and owner group.
- `chmod` changes permissions.
- `chown` changes owner user and/or owner group.
- `chgrp` changes only group ownership.
- `stat` shows detailed ownership and permission metadata.
- `root` has UID 0 and GID 0.
- `kali` has UID 1000 and GID 1000 in this VM.

---

## Interview Lines

Linux files have an owner user, owner group, and others.

The first username in `ls -la` output is the owner user, and the second username is the owner group.

`chmod` changes permissions, while `chown` changes ownership.

`chgrp` changes group ownership of a file or directory.

`sudo -l` lists what commands the current user can run with sudo privileges.

If a user is in the `sudo` group, they can usually run administrative commands using `sudo`.

A `Permission denied` error usually means the current user does not have the required read, write, execute, ownership, or sudo privileges.
