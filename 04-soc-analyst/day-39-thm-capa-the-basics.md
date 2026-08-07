# Day 39 – TryHackMe CAPA: The Basics

## Room Details

- **Platform:** TryHackMe
- **Learning path:** Cyber Security 101 → Defensive Security Tooling
- **Room:** CAPA: The Basics
- **Day:** 39
- **Block:** D39-B02
- **Status:** Completed (100%)
- **Estimated room time:** 60 minutes

## Learning Objectives

- Explain what CAPA is and why defenders use it.
- Distinguish static analysis from dynamic analysis.
- Understand how CAPA rules identify potential program capabilities.
- Read the main sections of a CAPA report.
- Interpret MITRE ATT&CK, MAEC, and Malware Behavior Catalog mappings.
- Use namespaces to organize related capabilities.
- Compare standard, verbose, very verbose, and JSON output.
- Treat CAPA results as leads that require analyst validation.

## What Is CAPA?

CAPA, short for **Common Analysis Platform for Artifacts**, is an open-source tool used to identify capabilities in executable files and supported analysis artifacts.

It can help an analyst quickly recognize potential behaviours such as:

- Network communication.
- File and Registry interaction.
- Process creation or injection.
- Persistence mechanisms.
- Data collection or encryption.
- Anti-analysis and obfuscation techniques.
- Runtime code loading.

CAPA automates part of the reverse-engineering triage process by comparing features found in an artifact with a collection of behavioural rules.

```text
Artifact → Feature extraction → CAPA rules → Matched capabilities → Analyst validation
```

A matched capability means that CAPA found features satisfying a rule. It does **not** automatically prove that the behaviour executed, that the sample is malicious, or that every match is relevant.

## Static and Dynamic Analysis

| Analysis type | What it examines | Main advantage | Main limitation |
|---|---|---|---|
| **Static analysis** | A file without executing it | Reduces the risk of triggering the sample and supports repeatable inspection | Packing or obfuscation may hide behaviour |
| **Dynamic analysis** | Behaviour produced while a sample runs in an isolated environment | Reveals actions that occur during execution | Only the executed path and observed conditions are visible |

This room focused mainly on using CAPA for **static analysis**. Suspicious programs should not be executed on a normal personal or production system.

## How CAPA Works

At a high level, CAPA:

1. Receives a supported artifact for analysis.
2. Identifies relevant file and code features.
3. Compares those features against its rule collection.
4. Determines which rule conditions matched.
5. Reports the corresponding capabilities and metadata.
6. Lets the analyst inspect the evidence behind important matches.

Rule features may include:

- API calls.
- Strings.
- Numeric constants.
- Instruction or code characteristics.
- Imported functions.
- References to other CAPA rule matches.

Rules convert low-level evidence into higher-level descriptions that are easier to investigate.

## CAPA Rule Structure

A CAPA rule normally contains two important parts:

| Part | Purpose |
|---|---|
| **Metadata** | Describes the rule name, namespace, authors, scope, examples, and optional ATT&CK or MBC mappings. |
| **Features** | Defines the technical conditions that must match in the artifact. |

Conceptual example:

```yaml
rule:
  meta:
    name: example network capability
    namespace: communication/example
  features:
    - and:
      - api: example_connect_function
      - string: example_network_marker
```

This is an illustrative structure, not evidence from the room sample.

## Understanding CAPA Output

CAPA reports combine basic artifact information with behavioural rule matches.

### General information

Depending on the artifact and output format, useful context may include:

- File name or source.
- File format.
- Architecture.
- Operating system.
- Hash values.
- Analysis backend.
- CAPA and rule-set information.

This context helps confirm that the correct artifact was analyzed and supports correlation with other tools.

### Capability

A capability is a human-readable description of something the analyzed program may be able to do. Examples include creating a process, communicating over HTTP, manipulating files, or modifying the Registry.

The analyst should ask:

```text
What capability matched?
Which evidence caused the match?
Where in the artifact was it found?
Does it fit the other observed evidence?
What should be validated next?
```

### Namespace

Namespaces organize related rules into hierarchical categories. Examples from the standard CAPA rules collection include:

| Namespace | Typical focus |
|---|---|
| **anti-analysis** | Packing, obfuscation, debugger checks, and other evasion behaviour |
| **collection** | Information or data gathered for possible later use or exfiltration |
| **communication** | HTTP, TCP, command-and-control, and related network activity |
| **data-manipulation** | Encoding, encryption, compression, and hashing |
| **host-interaction** | Files, processes, services, Registry, and other system resources |
| **load-code** | Loading or executing embedded code, libraries, or shellcode |
| **persistence** | Methods used to maintain access across restarts or sessions |
| **impact** | Actions connected to an operation's final effect |

A namespace groups capabilities; it is not itself proof of malicious intent.

## Behavioural Mappings

CAPA rules may include mappings that make results easier to relate to established security frameworks.

### MITRE ATT&CK

MITRE ATT&CK organizes adversary behaviour into tactics and techniques. A CAPA mapping can help an analyst connect a detected capability with a recognized adversary technique.

The mapping should be treated as analytical context, not automatic attribution to a threat actor or confirmation that an attack occurred.

### MAEC

**Malware Attribute Enumeration and Characterization (MAEC)** provides a standardized way to describe malware-related attributes and behaviour. It supports consistent communication and structured analysis.

### Malware Behavior Catalog

The **Malware Behavior Catalog (MBC)** organizes malware objectives and behaviours. CAPA can use MBC mappings to describe a capability in malware-analysis language.

The three views serve different purposes:

| Framework | Main use in analysis |
|---|---|
| **MITRE ATT&CK** | Relate a capability to adversary tactics and techniques |
| **MAEC** | Represent malware attributes and behaviour in a standardized form |
| **MBC** | Categorize malware objectives and behaviours |

## Output Formats and Detail Levels

CAPA can present findings at different levels of detail:

| Mode | Purpose |
|---|---|
| **Default text** | Shows concise, top-level capability matches |
| **Verbose (`-v`)** | Includes all rule matches, including nested matches |
| **Very verbose (`-vv`)** | Shows detailed evidence explaining how rules matched |
| **JSON (`-j`)** | Produces structured, machine-readable output for tooling or deeper review |

Generic command patterns:

```bash
capa <authorized-sample>
capa -v <authorized-sample>
capa -vv <authorized-sample>
capa -j <authorized-sample>
```

These commands are examples of the analysis workflow. This note does not claim that they were executed outside the guided room.

## Reading the Provided Report Types

The room demonstrated three useful report forms:

```text
Standard text report   → Quick overview of important top-level capabilities
Very verbose report    → Detailed rule matches and supporting evidence
JSON report            → Structured results for searching, filtering, or automation
```

A practical approach is:

1. Begin with the standard report to identify high-value findings.
2. Prioritize capabilities related to execution, persistence, communication, collection, credential access, defence evasion, or impact.
3. Open the very verbose report to understand why a selected rule matched.
4. Use the JSON report when structured filtering or programmatic processing is useful.
5. Correlate the result with file metadata, logs, network activity, endpoint evidence, and threat intelligence.

## Analyst Interpretation Workflow

```text
Confirm artifact → Review general information → Identify capabilities
→ Prioritize suspicious matches → Inspect detailed evidence
→ Correlate with other sources → Record conclusion and next action
```

For each important match, record:

```text
Capability:
Namespace:
Framework mapping:
Evidence shown by CAPA:
Why it matters:
Supporting evidence:
Confidence and limitations:
Recommended next step:
```

## Defensive Security Use Cases

CAPA can support:

- Initial malware triage.
- Incident-response investigation.
- Threat hunting.
- Prioritization of suspicious files.
- Identification of potential persistence or communication behaviour.
- Mapping program features to ATT&CK techniques.
- Selecting areas for deeper manual reverse engineering.
- Comparing capabilities across related samples.

CAPA reduces the time required to understand a file's potential functionality, but it does not replace reverse engineering, sandboxing, or evidence-based incident analysis.

## Safe Analysis Practices

1. Analyze only artifacts and systems you are authorized to inspect.
2. Work in an isolated lab or approved malware-analysis environment.
3. Preserve the original file and calculate hashes before analysis.
4. Do not double-click or execute a suspicious sample on a normal system.
5. Keep tools and rules from trusted sources up to date.
6. Start with static triage and use dynamic analysis only in an appropriately isolated sandbox.
7. Validate high-impact matches using supporting evidence.
8. Treat extracted domains, URLs, commands, and file paths as potentially dangerous.
9. Do not upload confidential samples to public services without authorization.
10. Document uncertainty instead of overstating a conclusion.

## Common Mistakes to Avoid

- Treating every CAPA match as proof of malware.
- Assuming a detected capability definitely executed.
- Ignoring benign software that may use the same APIs or behaviours.
- Reporting an ATT&CK mapping as threat-actor attribution.
- Reading only the capability name without examining supporting evidence.
- Ignoring packing or obfuscation that may limit static analysis.
- Running an unknown sample directly to confirm a static finding.
- Publishing malicious samples, credentials, flags, or room answers.
- Claiming professional malware-analysis experience from a guided lab.

## Practical Reporting Model

Every analysis summary should answer:

```text
What I checked:
The artifact identity, CAPA report type, and prioritized capability matches.

What I found:
The relevant capabilities, namespaces, mappings, and supporting rule evidence.

What it means:
A cautious interpretation of what the program may be capable of doing.

What I would do next:
Hash verification, deeper static review, isolated dynamic analysis, IOC correlation,
endpoint or network-log review, threat-intelligence enrichment, or escalation.
```

## Retention Checks

- Explain CAPA in one sentence.
- Distinguish static analysis from dynamic analysis.
- Explain how CAPA rules turn low-level features into capabilities.
- State why a capability match does not prove that behaviour executed.
- Identify the purpose of general information, namespaces, and capabilities.
- Explain the roles of MITRE ATT&CK, MAEC, and MBC.
- Compare default, verbose, very verbose, and JSON output.
- Describe when the detailed report should be inspected.
- State two limitations of automated static analysis.
- Describe the evidence that should be correlated with CAPA findings.
- Explain how suspicious samples should be handled safely.

## References

- [Official CAPA usage documentation](https://github.com/mandiant/capa/blob/master/doc/usage.md)
- [Official CAPA rules collection](https://github.com/mandiant/capa-rules)

## Evidence Boundary

This note records concepts and methods learned in a guided TryHackMe room. It does not claim production malware-analysis, reverse-engineering, threat-hunting, or SOC experience. Exercise answers, credentials, target details, sample-specific findings, flags, and raw output are intentionally excluded.

## Status

- TryHackMe room: **Completed – 100%**
- Portfolio note: **Prepared**
