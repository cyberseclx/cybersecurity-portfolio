# Day 14 — Linux Fundamentals Part 2

## Room / Topic

TryHackMe — Linux Fundamentals Part 2

## Status

Completed

## What I Practiced

Today I completed Linux Fundamentals Part 2. This room refreshed SSH access, Linux command flags/switches, deeper filesystem interaction, file permissions, and common Linux directories.

## Key Concepts

### SSH

SSH is used to securely access a remote Linux machine from another system.

```bash
ssh username@target_ip
```

Real-world use:

* Remote server administration
* SOC/NOC troubleshooting
* Accessing cloud/Linux servers
* Managing systems securely

### Flags and Switches

Linux commands often support flags to change command behavior.

Examples:

```bash
ls -l
ls -a
ls -la
```

* `-l` shows long listing format.
* `-a` shows hidden files.
* `-la` combines both.

### Filesystem Interaction

Important commands:

```bash
touch file.txt
mkdir folder
cp file.txt backup.txt
mv old.txt new.txt
rm file.txt
file filename
```

### Permissions

Linux permissions decide who can read, write, or execute a file.

Permission types:

```text
r = read
w = write
x = execute
```

Permission groups:

```text
user
group
others
```

Example:

```text
-rwxr-xr--
```

Breakdown:

```text
user:   rwx
group:  r-x
others: r--
```

### Common Directories

```text
/home  = user home directories
/root  = root user home directory
/tmp   = temporary files
/etc   = configuration files
/var   = variable data like logs
/bin   = essential binaries
/usr   = user programs and system resources
```

## Commands Practiced

```bash
ssh username@IP
ls -la
touch file.txt
mkdir folder
cp file1 file2
mv oldname newname
rm file.txt
file filename
chmod
chown
head
tail
cat
```

## Important Learning Moment

While checking Apache logs, I saw that `/var/log/apache2/access.log` had restricted permissions:

```text
-rw-r----- 1 root adm
```

This means:

* `root` can read/write
* `adm` group can read
* others cannot read

Since I was logged in as a normal user, I could not read that file directly. This helped me understand Linux file permissions practically.

## Key Takeaways

* SSH is used for secure remote login.
* Flags modify command behavior.
* `ls -la` is useful for checking hidden files and permissions.
* Linux permissions are based on user, group, and others.
* Logs are often protected and readable only by root or admin groups.
* Common directories like `/etc`, `/var`, `/tmp`, and `/home` are important for Linux admin and cybersecurity work.

## Real-World Use

These skills are useful for:

* Linux administration
* Troubleshooting servers
* Reading logs
* Understanding permission errors
* Remote access using SSH
* SOC/NOC investigations

## Interview Line

Linux permissions are important because they control who can read, modify, or execute files. Understanding permissions helps troubleshoot access issues, protect sensitive files, and manage users securely.
