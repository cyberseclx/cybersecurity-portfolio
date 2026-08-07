# Day 40 – TryHackMe FlareVM: Arsenal of Tools

## Room

- **Path:** Cyber Security 101 → Defensive Security Tooling
- **Room:** FlareVM: Arsenal of Tools
- **Status:** Completed – 100%
- **Estimated room time:** 40 minutes

## Objective

Become familiar with FlareVM and the investigative tools it provides for malware analysis, reverse engineering, incident response, forensic investigation, and static analysis.

## What is FlareVM?

FlareVM stands for:

**Forensics, Logic Analysis, and Reverse Engineering**

It is a specialised Windows-based toolkit designed for:

- Reverse engineers
- Malware analysts
- Incident responders
- Forensic investigators
- Penetration testers

The room describes FlareVM as a curated collection of specialised tools used to investigate executables, understand malware behaviour, and analyse suspicious files.

## Learning Objectives

The room focused on:

- Exploring tools available inside FlareVM.
- Learning how tools can be used to analyse potentially malicious processes.
- Becoming familiar with tools used for static analysis of malicious documents and binaries.

## Lab Environment

The provided FlareVM machine was used for the room exercises.

Most of the room files were located in:

```text
C:\Users\Administrator\Desktop\Sample
```

The room explicitly warned that the machine contains malicious sample files and that those files should only be handled inside the isolated FlareVM environment.

## Room Tasks Covered

### Task 1 – Introduction

Introduced FlareVM, its purpose, target users, learning objectives, lab setup, and malware-handling safety precautions.

### Task 2 – Arsenal of Tools

Explored the collection of tools available inside FlareVM.

### Task 3 – Commonly Used Tools for Investigation: Overview

Reviewed commonly used investigative tools available in the environment.

### Task 4 – Analyzing Malicious Files!

Worked through the room's malicious-file analysis section using the provided FlareVM environment.

### Task 5 – Conclusion

Completed the FlareVM: Arsenal of Tools room.

## Important Analysis Concepts

### Static Analysis

Static analysis means examining a suspicious file without relying on normal execution of the file.

In this room, static-analysis tooling was introduced in the context of:

- Malicious documents
- Executables / binaries
- Suspicious processes
- File investigation

### Isolated Analysis Environment

A key operational lesson from the room is that suspicious or malicious samples should be analysed in a controlled environment rather than on a normal workstation.

The provided FlareVM lab:

- Had no internet access.
- Contained malicious samples specifically for the exercises.
- Was intended to keep analysis separated from the analyst's primary system.

## Security Relevance

FlareVM is directly relevant to defensive-security and DFIR workflows because it provides a central Windows environment for investigating suspicious files and processes.

Possible workflow areas introduced by the room include:

- Malware triage
- Static analysis
- Process investigation
- Binary inspection
- Suspicious-document analysis
- Incident-response investigation
- Forensic investigation

## Commands / Tools Practiced

The exact tools, commands, and outputs used in Tasks 2–4 were not included in the completion text supplied for this GitHub note.

They are therefore not recorded here rather than being guessed.

## Troubleshooting / Corrections

No specific troubleshooting issue or incorrect command was supplied for this room.

## What I Learned

- FlareVM is a specialised Windows toolkit for forensic analysis, malware analysis, and reverse engineering.
- It is designed for analysts who need multiple investigative tools in one prepared environment.
- Static analysis is an important part of investigating malicious documents and binaries.
- Suspicious files should be handled only in isolated, controlled environments.
- Malware investigations can involve both files and running processes.
- FlareVM complements other defensive-security environments by focusing heavily on Windows-based investigation and reverse-engineering workflows.

## REMnux vs FlareVM – Current Understanding

From the two completed rooms:

- **REMnux** provides a specialised Linux-based malware-analysis environment.
- **FlareVM** provides a specialised Windows-based malware-analysis and reverse-engineering environment.

Both are useful defensive-security toolkits, but they provide different operating-system environments and tool ecosystems for investigation.

## SOC / DFIR Relevance

This room helps build familiarity with the tooling side of malware triage and incident investigation.

For an entry-level SOC or DFIR workflow, the main takeaway is:

> Suspicious files should be investigated in an isolated environment using appropriate analysis tools instead of being opened or executed on a normal workstation.

## Areas to Reinforce

- Exact purpose of the major FlareVM tools.
- Static vs dynamic analysis.
- Windows process investigation.
- PE / executable analysis fundamentals.
- Malicious-document analysis workflow.
- Indicators that distinguish suspicious and normal processes/files.
- Safe malware-handling practices.

## Final Status

**TryHackMe – FlareVM: Arsenal of Tools: 100% completed.**
