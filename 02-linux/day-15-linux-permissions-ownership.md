# Day 15 — Linux Permissions and Ownership

## Topic

Linux file permissions, directory permissions, ownership, groups, and `chmod`.

## Status

Completed

## Commands Practiced

```bash
whoami
id
groups
mkdir -p ~/permissions-practice
cd ~/permissions-practice
touch test.txt
ls -la
stat test.txt
chmod 600 test.txt
ls -la
chmod 644 test.txt
ls -la
chmod 755 test.txt
ls -la
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

This means I was logged in as the `kali` user.

---

## User ID and Groups

The `id` command shows the user ID, group ID, and group memberships.

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
groups = all groups the user belongs to
```

Important groups:

```text
sudo      = user can run administrative commands using sudo
wireshark = user can capture/analyze packets with Wireshark permissions
adm       = user may read some system logs
vboxsf    = VirtualBox shared folder access
```

The `groups` command also shows group memberships.

```bash
groups
```

---

## File Permission Format

Example:

```text
-rw-r--r--
```

Breakdown:

```text
-     = regular file
rw-   = owner permissions
r--   = group permissions
r--   = others permissions
```

Linux permissions are divided into three parts:

```text
Owner
Group
Others
```

Permission symbols:

```text
r = read
w = write
x = execute
```

---

## File Permissions

For a file:

```text
r = read file contents
w = modify file contents
x = execute the file as a program or script
```

Example:

```text
-rwxr-xr--
```

Meaning:

```text
Owner  = read, write, execute
Group  = read, execute
Others = read only
```

---

## Directory Permissions

Directory permissions behave differently from file permissions.

For a directory:

```text
r = list directory contents
w = create, delete, or rename files inside the directory
x = enter/traverse/access the directory
```

Important note:

```text
For directories, x does not mean execute like a file.
For directories, x means the ability to enter or traverse the directory.
```

Example:

```bash
cd directory-name
```

This requires execute permission on the directory.

Also, write permission on a directory is usually useful only when execute permission is also available.

---

## Practical Lab Setup

I created a practice directory:

```bash
mkdir -p ~/permissions-practice
cd ~/permissions-practice
```

Then I created a test file:

```bash
touch test.txt
```

I checked the file permissions:

```bash
ls -la
```

Initial output:

```text
-rw-rw-r-- 1 kali kali 0 Jul 4 20:08 test.txt
```

Meaning:

```text
Owner  = kali
Group  = kali
Others = everyone else

Owner permissions  = read + write
Group permissions  = read + write
Others permissions = read only
```

---

## stat Command

The `stat` command shows detailed file information.

```bash
stat test.txt
```

Output showed:

```text
Access: (0664/-rw-rw-r--)
Uid: (1000/kali)
Gid: (1000/kali)
```

Meaning:

```text
0664        = numeric permission format
-rw-rw-r--  = symbolic permission format
Uid         = owner user
Gid         = owner group
```

---

## chmod 600

Command:

```bash
chmod 600 test.txt
ls -la
```

Output:

```text
-rw-------
```

Meaning:

```text
Owner  = read + write
Group  = no permission
Others = no permission
```

Use case:

```text
Private files
SSH keys
Sensitive files
Files that only the owner should access
```

Example:

```text
600 = rw-------
```

---

## chmod 644

Command:

```bash
chmod 644 test.txt
ls -la
```

Output:

```text
-rw-r--r--
```

Meaning:

```text
Owner  = read + write
Group  = read only
Others = read only
```

Use case:

```text
Normal text files
Configuration files
Files that others can read but not modify
```

Example:

```text
644 = rw-r--r--
```

---

## chmod 755

Command:

```bash
chmod 755 test.txt
ls -la
```

Output:

```text
-rwxr-xr-x
```

Meaning:

```text
Owner  = read + write + execute
Group  = read + execute
Others = read + execute
```

Use case:

```text
Scripts
Programs
Directories that need to be accessed
```

Important:

```text
755 is common for scripts and directories.
It is usually not needed for a normal empty text file.
```

Example:

```text
755 = rwxr-xr-x
```

---

## Numeric Permission Values

Linux permissions can be represented using numbers.

```text
r = 4
w = 2
x = 1
```

Combinations:

```text
7 = 4 + 2 + 1 = rwx
6 = 4 + 2     = rw-
5 = 4 + 1     = r-x
4 = 4         = r--
0 = 0         = ---
```

Common examples:

```text
600 = rw-------
644 = rw-r--r--
755 = rwxr-xr-x
```

---

## Ownership

A file has:

```text
Owner user
Owner group
Others
```

Example:

```text
-rw-r--r-- 1 kali kali 0 Jul 4 20:08 test.txt
```

Meaning:

```text
Owner user  = kali
Owner group = kali
File name   = test.txt
```

The first `kali` is the owner user.

The second `kali` is the owner group.

---

## Important Commands

### Check current user

```bash
whoami
```

### Check user ID and groups

```bash
id
```

### Check group memberships

```bash
groups
```

### List permissions

```bash
ls -la
```

### Show detailed file information

```bash
stat test.txt
```

### Change permissions

```bash
chmod 600 test.txt
chmod 644 test.txt
chmod 755 test.txt
```

---

## Key Takeaways

- Linux permissions control who can read, write, or execute files.
- Permissions are divided into owner, group, and others.
- File permissions and directory permissions behave differently.
- For files, execute means running the file as a script or program.
- For directories, execute means entering or traversing the directory.
- `chmod` changes file or directory permissions.
- `600`, `644`, and `755` are common permission modes.
- `id` and `groups` show the current user’s privileges and group memberships.
- Being in the `sudo` group allows administrative actions using `sudo`.

---

## Interview Lines

Linux permissions are divided into owner, group, and others.

For files, read means viewing contents, write means modifying contents, and execute means running the file.

For directories, execute means entering or traversing the directory.

`chmod 600` is used for private files, `chmod 644` is common for normal readable files, and `chmod 755` is common for scripts or directories.

The `id` command shows user ID, group ID, and group memberships, which helps understand a user’s privileges on a Linux system.
