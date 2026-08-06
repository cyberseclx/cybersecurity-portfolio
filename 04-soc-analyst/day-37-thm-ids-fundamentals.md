# Day 37 – TryHackMe IDS Fundamentals

## Room Details

- **Platform:** TryHackMe
- **Learning path:** Cyber Security 101 → Security Solutions
- **Room:** IDS Fundamentals
- **Day:** 37
- **Status:** Completed (100%)
- **Estimated room time:** 60 minutes

## Learning Objectives

- Explain the purpose and limitations of an Intrusion Detection System (IDS).
- Distinguish network-based and host-based IDS deployments.
- Compare signature-based and anomaly-based detection.
- Explain the difference between an IDS and an Intrusion Prevention System (IPS).
- Understand the main stages of Snort traffic inspection.
- Read the structure of a Snort rule.
- Validate and use a custom Snort rule safely.
- Interpret IDS alerts from a SOC analyst's perspective.

## What Is an IDS?

An Intrusion Detection System monitors network or host activity for signs of attacks, policy violations, or abnormal behaviour. When it detects matching activity, it generates an alert for investigation.

```text
Traffic or host activity → IDS analysis → Detection → Alert → Analyst investigation
```

An IDS normally detects and reports suspicious activity; it does not automatically block the threat. Prevention requires an inline control such as an IPS, firewall action, endpoint control, or an approved analyst response.

## Why an IDS Is Needed

A firewall allows or denies traffic according to its rules, but permitted traffic can still contain malicious activity. An IDS adds visibility by inspecting activity that has passed other preventive controls.

```text
Firewall: Should this connection be allowed?
IDS:      Does the observed activity appear suspicious or malicious?
```

An IDS is one source of evidence. Its alerts should be correlated with endpoint, authentication, DNS, proxy, firewall, server, and application logs before reaching a conclusion.

## Types of IDS

| Type | Main visibility | Typical placement |
|---|---|---|
| **Network IDS (NIDS)** | Network packets and traffic patterns | A network segment, monitoring port, or traffic tap |
| **Host IDS (HIDS)** | Events on one endpoint, including logs, files, processes, and configuration changes | Installed on or connected to an individual host |

### Network IDS

A NIDS can observe traffic from multiple systems and identify suspicious network behaviour. Its visibility may be limited by encryption, asymmetric routing, packet loss, high traffic volume, or an incorrect monitoring position.

### Host IDS

A HIDS provides detailed visibility into activity occurring on a particular system. It can detect evidence that may not be visible on the network, but it depends on reliable host telemetry and correct configuration.

## Detection Methods

| Method | How it works | Strength | Limitation |
|---|---|---|---|
| **Signature-based detection** | Compares activity with known attack patterns or indicators. | Precise for known threats when signatures are accurate. | May miss new, modified, or obfuscated attacks. |
| **Anomaly-based detection** | Compares activity with an established baseline of normal behaviour. | Can reveal previously unseen or unusual behaviour. | Poor baselines or thresholds may create false positives. |
| **Hybrid detection** | Uses more than one detection method. | Provides broader visibility and context. | Requires tuning, maintenance, and analyst validation. |

### Detection Outcomes

| Outcome | Meaning |
|---|---|
| **True positive** | Malicious activity correctly generates an alert. |
| **False positive** | Benign activity incorrectly generates an alert. |
| **True negative** | Benign activity correctly produces no alert. |
| **False negative** | Malicious activity is not detected. |

The objective is not simply to generate more alerts. Useful detection balances coverage with enough accuracy and context for analysts to act.

## IDS vs IPS

| IDS | IPS |
|---|---|
| Monitors activity and alerts on detections. | Operates inline and can block or prevent matching activity. |
| Usually does not interrupt the connection. | Can drop packets, reset connections, or apply another prevention action. |
| A false positive creates investigation work. | A false positive may also interrupt legitimate traffic. |

An IDS alert is evidence to investigate, not automatic proof that a system was compromised.

## Snort Overview

Snort is an open-source network intrusion detection and prevention system. In IDS mode, it captures network traffic, decodes packets, evaluates them against configured rules, and produces alerts or logs when conditions match.

A simplified workflow is:

```text
Packet capture → Decode and normalize → Rule evaluation → Alert or log output
```

Important operational elements include:

- The monitored network interface.
- Network variables such as the protected network.
- The main configuration file.
- Enabled rule files and rule order.
- Alert mode and output location.
- Packet visibility and capture quality.
- Rule tuning and suppression decisions.

## Snort Rule Structure

A simplified Snort rule contains a header and rule options:

```text
action protocol source_ip source_port direction destination_ip destination_port (options)
```

Generic learning example:

```text
alert icmp any any -> $HOME_NET any (msg:"ICMP echo request observed"; itype:8; sid:1000001; rev:1;)
```

This example is intentionally broad and may be noisy. It is included to explain syntax, not as a production-ready detection rule.

### Rule Header

| Field | Purpose |
|---|---|
| `alert` | Generate an alert when all rule conditions match. |
| `icmp` | Inspect ICMP traffic. |
| `any any` | Match any source IP and source port. |
| `->` | Match traffic moving from source to destination. |
| `$HOME_NET any` | Match the configured protected network on any destination port. |

### Rule Options

| Option | Purpose |
|---|---|
| `msg` | Human-readable description shown with the alert. |
| `itype:8` | Match an ICMP echo-request message. |
| `sid` | Unique Snort rule identifier. Local rules should use a locally managed SID range. |
| `rev` | Revision number of the rule. Increment it when the rule changes. |

Depending on the detection objective, a rule can also use content, flow, flags, thresholds, references, classifications, and other protocol-specific options.

## Default and Custom Rules

### Default or Community Rules

Existing rules provide coverage for known behaviours and threats. They still require review because network roles, approved applications, address ranges, and normal traffic vary between environments.

### Custom Rules

A custom rule should begin with a clear detection objective:

```text
Behaviour to detect:
Required packet or flow evidence:
Protected assets:
Expected legitimate activity:
Alert severity and response:
Possible false positives:
```

A rule that compiles is not automatically a useful rule. It must be tested against matching and non-matching traffic, reviewed for performance impact, and tuned using real environmental context.

## Safe Snort Workflow

1. Identify the interface and network segment being monitored.
2. Confirm that the required traffic is visible to the sensor.
3. Review the configuration, network variables, and enabled rules.
4. Define one specific detection objective.
5. Add or modify the rule through the approved local rule file.
6. Validate the configuration before starting detection.
7. Generate controlled test traffic in an authorized lab.
8. Confirm that matching traffic generates the expected alert.
9. Confirm that unrelated traffic does not generate unnecessary alerts.
10. Review the timestamp, addresses, ports, protocol, message, SID, and supporting packet evidence.
11. Tune the rule and document the change.

Common validation syntax is:

```bash
sudo snort -T -c /etc/snort/snort.conf
```

A common console-alert pattern is:

```bash
sudo snort -q -A console -i <interface> -c /etc/snort/snort.conf
```

Paths and options depend on the installed Snort version and environment. These commands are reference patterns only; this note does not claim that they were executed or that any specific output was obtained.

## Alert Analysis Workflow

When reviewing a Snort or other IDS alert:

1. Confirm the alert timestamp, sensor, time zone, signature, SID, and revision.
2. Identify the source and destination IP addresses, ports, protocol, and direction.
3. Review the packet or flow evidence that caused the rule to match.
4. Identify the affected asset, its role, owner, exposure, and criticality.
5. Determine whether the activity was allowed by the firewall and whether the connection succeeded.
6. Check for repeated attempts, related alerts, or activity across other systems.
7. Pivot to firewall, DNS, proxy, authentication, endpoint, server, and application logs.
8. Classify the alert as a likely true positive, false positive, or requiring more evidence.
9. Escalate or contain only according to the evidence and approved procedure.
10. Document findings, uncertainty, and the next investigative action.

## Practical Reporting Model

Every practical should end with:

```text
What I checked:
The IDS configuration, monitored traffic, rule conditions, alert fields, and related evidence reviewed.

What I found:
The activity that matched the rule and the systems, users, or connections involved.

What it means:
Whether the evidence appears benign, suspicious, or malicious and how confident that assessment is.

What I would do next:
The next log source, packet review, endpoint check, tuning action, escalation, or containment step required.
```

## Mistakes to Avoid

- Assuming an IDS automatically blocks detected activity.
- Treating every alert as proof of compromise.
- Ignoring false negatives because no alert was generated.
- Confusing the alert source with the protected destination.
- Writing overly broad rules that generate excessive noise.
- Changing several rule conditions at once without controlled testing.
- Ignoring the monitored interface, network variables, or sensor placement.
- Investigating an alert without checking supporting host and network logs.
- Publishing lab credentials, target details, room answers, flags, or raw sensitive output.

## Retention Checks

- Explain why an IDS is still useful when a firewall is present.
- State whether an IDS normally prevents a detected threat.
- Distinguish a NIDS from a HIDS.
- Compare signature-based and anomaly-based detection.
- Explain true positives, false positives, true negatives, and false negatives.
- Distinguish an IDS from an IPS.
- Describe the simplified Snort packet-inspection workflow.
- Identify the header and options in a Snort rule.
- Explain the purpose of `msg`, `sid`, and `rev`.
- Describe how to validate and test a custom rule safely.
- State what you checked, found, concluded, and would do next.

## Evidence Boundary

This note records concepts and methods learned in a guided TryHackMe room. It does not claim production IDS, Snort, or SOC experience. Lab answers, credentials, target details, flags, and raw output are intentionally excluded.

## Status

- TryHackMe room: **Completed – 100%**
- Portfolio note: **Prepared**
- Experience boundary: **Guided lab learning only**
