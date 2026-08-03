# Day 35 – TryHackMe Introduction to SIEM

## Room Details

- **Platform:** TryHackMe
- **Learning path:** Cyber Security 101 → Security Solutions
- **Room:** Introduction to SIEM
- **Day:** 35
- **Module:** Security Solutions

## Learning Objectives

- Explain why isolated logs make security investigations difficult.
- Understand how a SIEM centralizes, parses, normalizes, and correlates logs.
- Identify common security log sources and ingestion methods.
- Understand how correlation rules turn related events into alerts.
- Follow a structured alert-triage and investigation workflow.
- Distinguish evidence from assumptions when documenting an alert.

## What Is a SIEM?

**SIEM** stands for **Security Information and Event Management**.

A SIEM collects security-relevant data from many systems into one searchable location. It helps analysts detect suspicious activity, investigate alerts, build timelines, and document incidents.

A simplified SIEM pipeline is:

```text
Log Sources → Collection → Parsing → Normalization → Correlation → Alert → Triage → Investigation
```

## Why Isolated Logs Are a Problem

Investigating each device separately creates several limitations:

- Logs are distributed across many hosts and applications.
- Products use different formats, field names, and timestamps.
- A single event may appear harmless without related evidence.
- Manual searches are slow during time-sensitive incidents.
- Retention periods and access methods may differ.
- Building a reliable cross-system timeline becomes difficult.

A SIEM reduces these problems by centralizing the evidence and making events from different sources easier to search and compare.

## Core SIEM Functions

| Function | Purpose |
|---|---|
| **Collection** | Receives logs and security telemetry from multiple sources. |
| **Parsing** | Separates raw log text into useful fields. |
| **Normalization** | Maps different vendor formats into consistent field names and values. |
| **Enrichment** | Adds context such as asset value, user identity, geolocation, or threat intelligence. |
| **Correlation** | Connects related events across users, hosts, IP addresses, and time. |
| **Alerting** | Notifies analysts when rule conditions or detection logic are matched. |
| **Search and investigation** | Allows analysts to query events, pivot between entities, and build timelines. |
| **Dashboards and reports** | Summarizes activity, trends, cases, and operational metrics. |
| **Retention** | Preserves searchable evidence for investigations, auditing, and compliance. |

## Common Log Sources

| Source | Useful security evidence |
|---|---|
| **Windows endpoints and servers** | Logons, account changes, process activity, services, and audit events. |
| **Linux systems** | Authentication, privilege use, services, scheduled tasks, and system messages. |
| **Active Directory / identity provider** | Authentication, account changes, group membership, and access decisions. |
| **Firewall** | Allowed or blocked connections, source/destination IPs, ports, and protocols. |
| **IDS/IPS** | Signatures, suspicious traffic, exploit indicators, and prevention actions. |
| **DNS** | Domain queries, responses, suspicious destinations, and beaconing patterns. |
| **Proxy / secure web gateway** | URLs, categories, users, downloads, and web-access decisions. |
| **VPN** | Remote-access logons, source locations, session duration, and assigned addresses. |
| **Web and application servers** | Requests, authentication, errors, status codes, and application actions. |
| **Endpoint security / EDR** | Processes, files, command lines, detections, and response actions. |
| **Cloud services** | Sign-ins, API calls, configuration changes, and administrative activity. |

No single source normally provides the complete story. Analysts correlate identity, endpoint, network, application, and cloud evidence.

## Log Ingestion Methods

Common ways to send data into a SIEM include:

- **Agent:** Software installed on a host collects and forwards selected events.
- **Syslog:** Network devices and Unix-like systems send messages to a central receiver.
- **API or connector:** The SIEM retrieves events from cloud platforms and security products.
- **Log forwarder:** A dedicated service collects, buffers, and forwards logs.
- **File or database ingestion:** The SIEM reads supported log files or stored records.

Before relying on ingested data, an analyst should verify:

```text
Is the correct source sending logs?
Are timestamps and time zones consistent?
Are important fields parsed correctly?
Is the expected event volume arriving?
Are there collection gaps or delays?
```

## Parsing and Normalization

Raw products may describe the same concept differently. For example, one source might use `src_ip`, another `sourceAddress`, and another `client_ip`.

Normalization maps them to a consistent field such as:

```text
source.ip
```

Useful normalized fields include:

- Timestamp
- Username
- Hostname
- Source and destination IP address
- Source and destination port
- Event action and outcome
- Process name and command line
- URL or domain
- Rule name and severity

Correct normalization allows one query or detection rule to work across multiple data sources.

## Correlation and Alerting

A single failed logon may be normal. A sequence of related events can be more significant:

```text
Repeated failed logons
        ↓
Successful logon from the same source
        ↓
Privilege or group-membership change
        ↓
Sensitive system access
```

A correlation rule evaluates defined conditions across events and time. When the conditions match, the SIEM creates an alert for analyst review.

An alert is a lead—not proof of an incident. It may be:

- **True positive:** The rule detected genuine malicious or policy-violating activity.
- **Benign true positive:** The detected activity occurred but had a legitimate explanation.
- **False positive:** The rule triggered even though the suspicious condition was not present.
- **False negative:** Malicious activity occurred but the detection did not alert.

## Alert-Triage Workflow

1. Read the alert title, description, severity, rule logic, and trigger time.
2. Identify the involved user, host, source IP, destination, process, and resource.
3. Check whether the required log sources are present and reliable.
4. Review the events that directly triggered the alert.
5. Expand the time window before and after the trigger.
6. Pivot on related entities such as the username, hostname, IP address, domain, or file hash.
7. Compare the activity with normal behaviour and known administrative work.
8. Decide whether the alert is suspicious, benign, or still inconclusive.
9. Document the supporting evidence and any uncertainty.
10. Escalate or close the alert according to the playbook.

## Questions to Ask During Analysis

```text
What detection rule triggered?
Which event fields satisfied the rule?
Who or what is involved?
When did the activity begin and end?
Where did it originate and what was targeted?
Was the activity successful?
What related events happened before and after it?
Do other log sources support the same conclusion?
What should I check next?
```

## Practical Reporting Model

Every investigation should end with four clear statements:

```text
What I checked:
The alert, time window, entities, fields, and supporting log sources reviewed.

What I found:
The relevant events and their chronological sequence.

What it means:
The evidence-supported interpretation, including uncertainty.

What I would do next:
The next query, data source, containment step, or escalation required.
```

## SOC Relevance

SIEM skills are central to junior SOC work because they support:

- Continuous security monitoring
- Alert validation and prioritization
- Cross-source investigation
- User and host scoping
- Timeline creation
- Evidence-based escalation
- Incident documentation and handoff
- Detection-rule improvement

The analyst's goal is not merely to close alerts quickly. It is to make a defensible decision using reliable evidence and clearly document what remains unknown.

## Mistakes to Avoid

- Treating an alert as automatic proof of compromise
- Investigating only the event that triggered the alert
- Ignoring timestamp, time-zone, or ingestion-delay issues
- Trusting fields without checking whether they were parsed correctly
- Searching only one source when correlation is possible
- Ignoring missing logs or collection gaps
- Closing an alert without documenting evidence
- Exposing lab answers, credentials, target details, flags, or raw sensitive data in public notes

## Retention Checks

- Expand the term SIEM.
- Explain why isolated logs make investigations difficult.
- Describe collection, parsing, normalization, correlation, and alerting.
- Name at least six useful SIEM log sources.
- Explain the difference between parsing and normalization.
- Explain why an alert is not proof of an incident.
- Distinguish a true positive, benign true positive, false positive, and false negative.
- Describe the first five actions you would take when triaging an alert.
- State what you checked, found, concluded, and would do next.

## Evidence Boundary

This note records concepts and methods learned in a guided TryHackMe room. It does not claim production SOC experience. Lab answers, credentials, target details, flags, and raw output are intentionally excluded.

## Status

- Portfolio note: **Prepared**
- Experience boundary: **Guided lab learning only**

