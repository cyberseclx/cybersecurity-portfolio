# Day 22 - Linux Find Grep Redirection Filtering Repair Practical

## Block

**Clockify:** `D22-B04 | Linux Practical | Find Grep Redirection Filtering Repair`  
**Project:** `CS Sprint | Practical Labs`

## Lab Folder

```bash
/home/kali/cyber_project/kali_practise/Linux/linux-find-grep-repair-day22
```

## Status

Completed.

---

## 1. Files and Folders Created

```text
auth.log
system.log
users.txt
backup/
logs/
reports/
files.txt
errors.txt
```

Subfolders:

```text
backup/users_backup.txt
logs/access.log
logs/error.log
reports/day22.txt
```

---

## 2. find Practice

### Find `.log` files

```bash
find . -type f -name "*.log"
```

Output included:

```text
./auth.log
./system.log
./logs/error.log
./logs/access.log
```

### Find `.txt` files

```bash
find . -type f -name "*.txt"
```

Output included:

```text
./backup/users_backup.txt
./errors.txt
./reports/day22.txt
./files.txt
./users.txt
```

### Find `users.txt`

```bash
find . -type f -name "users.txt"
```

Output:

```text
./users.txt
```

### Find directory named `backup`

```bash
find . -type d -name "backup"
```

Output:

```text
./backup
```

Memory:

```text
find . -type f -name "*.log" = find log files from current directory
find . -type d -name "backup" = find directory named backup
```

---

## 3. grep Practice

### Search failed

```bash
grep "failed" auth.log
```

Found 3 failed lines.

### Ignore case

```bash
grep -i "FAILED" auth.log
```

Still found the failed lines because `-i` ignores uppercase/lowercase.

### Show line numbers

```bash
grep -n "failed" auth.log
```

Output showed:

```text
2:2026-07-11 failed admin 192.168.1.11
3:2026-07-11 failed guest 192.168.1.12
6:2026-07-11 failed admin 192.168.1.15
```

### Count failed lines

```bash
grep -c "failed" auth.log
```

Output:

```text
3
```

### Show lines that are not success

```bash
grep -v "success" auth.log
```

This showed failed and denied lines.

### Search failed OR denied

```bash
grep -E "failed|denied" auth.log
```

This showed both failed and denied entries.

### Search admin inside `.log` files

```bash
grep "admin" *.log
```

Output showed matching lines from `auth.log`.

Memory:

```text
-i = ignore case
-n = line numbers
-c = count
-v = invert match / NOT matching
-E = extended regex, useful for OR
```

---

## 4. Redirection Practice

### Overwrite output

```bash
ls > files.txt
```

### Append output

```bash
pwd >> files.txt
```

### Redirect errors

```bash
ls /wrong/path 2> errors.txt
```

`errors.txt` contained:

```text
ls: cannot access '/wrong/path': No such file or directory
```

Memory:

```text
> = overwrite
>> = append
2> = redirect errors
```

---

## 5. sort / uniq / wc Practice

### Count repeated users

```bash
sort users.txt | uniq -c
```

Output:

```text
3 admin
2 guest
1 root
1 test
1 user1
```

### Count total lines

```bash
wc -l auth.log
```

Output:

```text
7 auth.log
```

### Count failed lines using pipe

```bash
grep "failed" auth.log | wc -l
```

Output:

```text
3
```

### Count failed lines using grep only

```bash
grep -c "failed" auth.log
```

Output:

```text
3
```

Memory:

```text
sort before uniq because uniq works on adjacent duplicate lines.
wc -l has a space.
wc-l is wrong.
```

---

## 6. awk / cut Practice

### Print username field

```bash
awk '{print $3}' auth.log
```

This printed usernames.

### Print usernames only where status is failed

```bash
awk '$2=="failed" {print $3}' auth.log
```

Output:

```text
admin
guest
admin
```

### Print first field using cut

```bash
cut -d " " -f1 auth.log
```

This printed dates.

### Print third field using cut

```bash
cut -d " " -f3 auth.log
```

This printed usernames.

Memory:

```text
cut = simple delimiter and field extraction
awk = more flexible column processing and conditional filtering
```

Example:

```bash
awk '$2=="failed" {print $3}' auth.log
```

Meaning:

```text
If field 2 equals failed, print field 3.
```

---

## 7. which / whereis

### which grep

```bash
which grep
```

Output:

```text
grep: aliased to grep --color=auto
```

This means the shell is using an alias for `grep`.

### whereis grep

```bash
whereis grep
```

Output:

```text
grep: /usr/bin/grep /usr/share/man/man1/grep.1.gz /usr/share/info/grep.info.gz
```

Memory:

```text
which = actual command/alias used by shell
whereis = binary, man page, and related locations
```

---

## 8. Mistakes Fixed

### Command prompt showed `>....`

This usually means the shell thought a quote or multi-line input was not closed properly.

Fix:

```text
Press Ctrl+C to cancel the broken command.
Then retype the command carefully.
```

### Uppercase folder path

Lab path used:

```bash
/home/kali/cyber_project/kali_practise/Linux/linux-find-grep-repair-day22
```

This is okay, but Linux is case-sensitive.

```text
Linux and linux are different folder names.
```

For GitHub, continue using lowercase:

```text
02-linux
```

---

## 9. Key Memory Rules

```text
find = find files/directories by name/type/location
grep = search inside file content
> = overwrite
>> = append
2> = redirect error
| = send output to next command
sort = sort lines
uniq = remove/count adjacent duplicates
wc -l = count lines
cut = simple field extraction
awk = flexible field extraction and filtering
which = command used by shell
whereis = binary/source/manual locations
```

---

## 10. Commands To Memorize

```bash
find . -type f -name "*.log"
find . -type f -name "*.txt"
find . -type f -name "users.txt"
find . -type d -name "backup"

grep "failed" auth.log
grep -i "FAILED" auth.log
grep -n "failed" auth.log
grep -c "failed" auth.log
grep -v "success" auth.log
grep -E "failed|denied" auth.log
grep "admin" *.log

ls > files.txt
pwd >> files.txt
ls /wrong/path 2> errors.txt

sort users.txt | uniq -c
wc -l auth.log
grep "failed" auth.log | wc -l
grep -c "failed" auth.log

awk '{print $3}' auth.log
awk '$2=="failed" {print $3}' auth.log
cut -d " " -f1 auth.log
cut -d " " -f3 auth.log

which grep
whereis grep
```

---

## 11. Weak Areas To Keep Repairing

```text
Exact lowercase command syntax
Correct file names
cut syntax
awk syntax with filename
grep -v for NOT matching
grep -E OR syntax
wc -l spacing
find path before conditions
```

---
