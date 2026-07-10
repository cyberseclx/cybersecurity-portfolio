# Day 21 - Linux Shells

## Room

TryHackMe Cyber Security 101 - Linux Shells

## Status

Completed

## Category

Command Line / Linux Shell Scripting

---

## What I Learned

### 1. What is a Shell?

A shell is the interface between the user and the operating system.

It takes commands from the user, interprets them, and passes them to the operating system for execution.

Flow:

```text
User -> Shell -> OS/Kernel -> System Result
```

Using the shell gives more control than using only a graphical user interface because commands can be executed directly and tasks can be automated.

---

### 2. Terminal vs Shell vs CLI

| Term | Meaning |
|---|---|
| Terminal | The application/window where commands are typed |
| Shell | The program that interprets and runs commands |
| CLI | Command Line Interface; a way to interact with a system using text commands |

Examples of Linux shells:

- `sh`
- `bash`
- `zsh`
- `fish`

Command to check the current shell:

```bash
echo $SHELL
```

---

### 3. Basic Shell Commands Practiced

```bash
echo
read
nano
chmod
chmod +x
./script.sh
```

Meanings:

- `echo` prints text/output.
- `read` takes input from the user.
- `nano` is a terminal text editor.
- `chmod` changes file permissions.
- `chmod +x` gives execute permission to a script.
- `./script.sh` runs a script from the current directory.

---

### 4. Shell Script Basics

A shell script is a file that contains multiple commands written together so they can be executed as a program.

Example script file:

```bash
script.sh
```

To edit a script:

```bash
nano script.sh
```

To make a script executable:

```bash
chmod +x script.sh
```

To run the script:

```bash
./script.sh
```

---

### 5. Shebang

Example:

```bash
#!/bin/bash
```

This is called a shebang.

It tells Linux which interpreter should run the script.

In this case, the script will run using Bash.

---

### 6. Variables

A variable is used to store a value.

Example:

```bash
name="Rohit"
echo $name
```

The `$` symbol is used to read or call the value stored inside the variable.

Important points:

- No spaces around `=` while assigning a variable.
- Use `$variable_name` to access the value.
- Variables are useful for storing user input, file names, paths, and repeated values.

Correct:

```bash
name="Rohit"
```

Wrong:

```bash
name = "Rohit"
```

---

### 7. Taking User Input

The `read` command is used to take input from the user.

Example:

```bash
echo "Enter your name:"
read name
echo "Hello $name"
```

Meaning:

- The user enters a value.
- The value is stored inside the variable `name`.
- The script can use that value later.

---

### 8. Conditional Statements

A conditional statement allows a script to make decisions.

Example:

```bash
#!/bin/bash

echo "Please enter your name:"
read name

if [ "$name" = "Stewart" ]; then
    echo "Access granted"
else
    echo "Access denied"
fi
```

Meaning:

- `if` starts the condition.
- `[ "$name" = "Stewart" ]` compares the user input with the expected value.
- `then` runs the command if the condition is true.
- `else` runs the command if the condition is false.
- `fi` ends the condition.

---

### 9. Important Conditional Syntax Rule

Wrong syntax I used:

```bash
if ["$name"="Stewart"];
```

This caused an error similar to:

```bash
command not found
```

Reason:

In Bash, spaces are very important.

The `[` is treated like a command, so it needs spaces around it.

Correct syntax:

```bash
if [ "$name" = "Stewart" ]; then
```

Important spacing rules:

- Space after `[`
- Space before `]`
- Space around `=`
- Use `then` after the condition

---

### 10. Spelling Mistake I Fixed

I typed:

```bash
Steward
```

But the expected value was:

```bash
Stewart
```

Lesson:

Linux scripts are strict. Small spelling mistakes can change the output or break the expected result.

---

### 11. Loops

Loops are used to repeat commands.

They are useful when the same task needs to run multiple times.

Example `for` loop:

```bash
#!/bin/bash

for i in 1 2 3 4 5
do
    echo "Number: $i"
done
```

Meaning:

- `for` starts the loop.
- `i` stores each value one by one.
- `do` starts the commands that will repeat.
- `done` ends the loop.

Output:

```text
Number: 1
Number: 2
Number: 3
Number: 4
Number: 5
```

---

### 12. Why Loops Are Useful

Loops are useful for automation.

Examples:

- Checking multiple files
- Reading multiple usernames
- Running the same command many times
- Checking logs
- Creating repeated output
- Automating Linux support tasks

Example:

```bash
for file in *.log
do
    echo "Checking $file"
done
```

This checks every `.log` file in the current directory.

---

### 13. Conditional + Loop Concept

Conditionals and loops can be combined.

Example:

```bash
#!/bin/bash

for user in admin guest rohit
do
    if [ "$user" = "admin" ]; then
        echo "$user has privileged access"
    else
        echo "$user has normal access"
    fi
done
```

Meaning:

- The loop checks each username.
- The condition checks whether the user is `admin`.
- Different output is shown based on the condition.

This is useful for checking users, files, logs, or system conditions.

---

## Scripts Practiced

### Conditional Script

Purpose:

To take user input and check whether the input matches the allowed value.

Main concepts used:

- `echo`
- `read`
- variable
- `if`
- `else`
- `fi`
- string comparison

---

### Loop Script

Purpose:

To repeat commands using a loop.

Main concepts used:

- `for`
- variable
- `do`
- `done`
- repeated output

---

## Commands Used

```bash
nano conditional_script.sh
nano loop_script.sh
chmod +x conditional_script.sh
chmod +x loop_script.sh
./conditional_script.sh
./loop_script.sh
echo
read
```

---

## Mistakes and Fixes

| Mistake | Fix | Lesson |
|---|---|---|
| Missed spaces in `if` condition | Used `if [ "$name" = "Stewart" ]; then` | Bash condition syntax needs proper spacing |
| Typed wrong spelling | Corrected the expected value | Scripts are strict with exact values |
| Script needs execute permission | Used `chmod +x script.sh` | A script must be executable before running with `./script.sh` |

---

## Key Takeaways

- A shell helps the user interact with the operating system.
- Terminal, shell, and CLI are related but not the same.
- Shell scripts help automate command-line tasks.
- The shebang tells Linux which interpreter should run the script.
- Variables store values.
- `read` takes user input.
- Conditional statements allow scripts to make decisions.
- Loops repeat commands.
- Bash syntax is strict, especially with spaces.
- Small mistakes in spelling or spacing can break a script.

---

## Practical Value

This room helped me understand basic Linux shell usage and beginner shell scripting.

This is useful for:

- command-line confidence
- Linux support tasks
- SOC/NOC troubleshooting
- simple automation
- checking logs
- running repeated commands
- future OSCP preparation

---

## Personal Learning Note

Today I got stuck in a Bash conditional script because of spacing and spelling mistakes.

The error helped me understand that Bash syntax is strict and that small mistakes can completely change how a script runs.

This was useful practical debugging experience.
