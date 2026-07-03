# Day 14 — Linux Fundamentals Part 1

## Room / Topic

TryHackMe — Linux Fundamentals Part 1

## Status

Completed

## What I Practiced

Today I refreshed basic Linux command-line usage through the THM Linux Fundamentals Part 1 room. Most commands were already familiar from my previous HTB Linux practice, but this was useful revision for navigation, file handling, searching, and shell operators.

## Key Concepts

### Terminal

The terminal allows us to interact with the Linux operating system using commands.

### Current Directory

The current directory is the location where we are working inside the filesystem.

### Filesystem

Linux stores files and directories in a structured hierarchy. We move around this structure using commands like `cd`, `pwd`, and `ls`.

### Standard Output Redirection

Shell operators like `>` and `>>` allow us to send command output into files.

## Commands Practiced

### Print text

```bash
echo "Hello"
```

Used to print text to the terminal.

### Check current user

```bash
whoami
```

Shows which user is currently logged in.

### Show current directory

```bash
pwd
```

Shows the present working directory.

### List files and folders

```bash
ls
ls -la
```

`ls` lists files and folders.
`ls -la` shows hidden files, permissions, ownership, size, and timestamps.

### Change directory

```bash
cd directory_name
cd ..
cd ~
```

Used to move between directories.

### Read file content

```bash
cat file.txt
```

Displays the contents of a file.

### Search for files

```bash
find /home -name file.txt 2>/dev/null
```

Used to search for files by name.
`2>/dev/null` hides permission errors.

### Search inside files

```bash
grep "word" file.txt
```

Used to search for specific text inside a file.

## Shell Operators

### `>`

```bash
echo "hello" > note.txt
```

Writes output to a file and overwrites existing content.

### `>>`

```bash
echo "world" >> note.txt
```

Appends output to the end of a file.

### `&&`

```bash
mkdir test && cd test
```

Runs the second command only if the first command succeeds.

### `&`

```bash
command &
```

Runs a command in the background.

## Important Takeaways

* `pwd` tells where I am.
* `ls` shows what is inside a directory.
* `cd` moves between directories.
* `cat` reads file contents.
* `find` searches for files.
* `grep` searches inside files.
* `>` overwrites file content.
* `>>` appends to file content.
* `&&` chains commands safely.

## Real-World Use

These commands are used daily in Linux administration, SOC work, troubleshooting, log analysis, scripting, and cybersecurity labs.

Examples:

* Use `ls -la` to inspect permissions.
* Use `cat` or `less` to read configuration files.
* Use `find` to locate files.
* Use `grep` to search logs.
* Use shell operators to save command output into evidence files.

## Interview Line

Linux fundamentals are important because most servers, security tools, logs, and automation workflows depend on command-line usage. Being comfortable with navigation, file handling, searching, and shell operators is the foundation for Linux administration and cybersecurity work.

## Confidence Level

Comfortable. This was mostly revision, but useful for reinforcing command-line basics.
