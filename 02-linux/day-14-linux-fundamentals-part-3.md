# Day 14 — Linux Fundamentals Part 3

## Room / Topic

TryHackMe — Linux Fundamentals Part 3

## Status

Completed

## What I Practiced

Today I completed Linux Fundamentals Part 3. This room helped revise more Linux command-line usage and practical concepts useful for Linux administration and cybersecurity.

## Key Concepts

### Terminal Efficiency

Linux work becomes faster when we know how to combine commands, search files, inspect output, and understand system information.

### Processes

A process is a running program on Linux.

Useful commands:

```bash
ps
ps aux
top
```

Real-world use:

* Check running services
* Find suspicious processes
* Troubleshoot high CPU or memory usage

### Services

Services are background programs that run on the system.

Useful commands:

```bash
systemctl status service_name
systemctl start service_name
systemctl stop service_name
systemctl restart service_name
```

Real-world use:

* Manage Apache, SSH, databases, monitoring tools, and other server services.

### Logs

Logs record system and application activity.

Common log locations:

```text
/var/log/
/var/log/auth.log
/var/log/syslog
/var/log/apache2/
```

Useful commands:

```bash
cat file.log
less file.log
tail file.log
tail -f file.log
grep "word" file.log
```

Real-world use:

* Investigate login attempts
* Troubleshoot failed services
* Check web server activity
* Monitor suspicious behavior

### Package Management

Linux systems use package managers to install and update software.

Debian/Ubuntu/Kali examples:

```bash
apt update
apt install package_name
apt remove package_name
```

### Searching and Filtering

Useful commands:

```bash
find / -name filename 2>/dev/null
grep "keyword" file.txt
grep -R "keyword" /path 2>/dev/null
```

`find` searches for files.
`grep` searches inside files.

## Commands Practiced

```bash
ps
top
systemctl
journalctl
cat
less
head
tail
tail -f
grep
find
apt update
apt install
```

## Important Takeaways

* Processes are running programs.
* Services are background programs managed by the system.
* Logs are important for troubleshooting and security investigations.
* `grep` is useful for finding specific text inside files and logs.
* `find` is useful for locating files across the filesystem.
* `tail -f` is useful for watching logs live.
* Package managers help install and maintain software.

## Real-World Use

These concepts are important for:

* Linux support roles
* Junior system administration
* SOC analyst work
* Troubleshooting incidents
* Checking logs
* Managing services
* Cybersecurity labs and privilege escalation practice

## Interview Line

Linux process, service, and log management are important because they help administrators understand what is running, what has failed, and what activity happened on the system. These are core skills for Linux administration, SOC monitoring, and cybersecurity troubleshooting.
