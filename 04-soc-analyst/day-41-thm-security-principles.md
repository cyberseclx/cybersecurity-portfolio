# Day 41 – TryHackMe Security Principles

## Room
- **Path:** Cyber Security 101
- **Module:** Build Your Cyber Security Career
- **Room:** Security Principles
- **Status:** Completed – 100%
- **Estimated room time:** 90 minutes

## Objective
Build a foundation in core cyber security principles, models, and terminology used to reason about protecting systems, data, and services.

## Core Security Idea
Perfect security does not exist.

Security controls should be chosen based on:
- What asset is being protected.
- Who the likely adversary is.
- How capable that adversary may be.
- The potential impact if the asset is compromised.

The room uses this idea to show that different assets and threats require different levels and types of protection.

## Learning Objectives
The room introduced:
- Confidentiality, Integrity, and Availability (CIA).
- Disclosure, Alteration, and Destruction/Denial (DAD).
- Fundamental security models such as Bell-LaPadula.
- Defence-in-Depth.
- Zero Trust.
- Trust but Verify.
- ISO/IEC 19249.
- Vulnerability, Threat, and Risk.

## Room Tasks Covered

### Task 1 – Introduction
Introduced the idea that security must be designed around the asset, adversary, and level of risk.

A key principle is that no system can be made perfectly secure, so the goal is to improve the security posture and make successful attacks more difficult.

### Task 2 – CIA
Covered the security triad:
- **Confidentiality**
- **Integrity**
- **Availability**

These three functions are core goals when protecting information and systems.

### Task 3 – DAD
Introduced the opposite of the CIA triad:
- **Disclosure**
- **Alteration**
- **Destruction / Denial**

This provides another way to think about what happens when security properties are violated.

### Task 4 – Fundamental Concepts of Security Models
Introduced security models, including the **Bell-LaPadula model**.

The detailed model rules and examples used inside the task were not included in the room text supplied for this GitHub note, so they are not expanded here rather than being guessed.

### Task 5 – Defence-in-Depth
Introduced the security principle of using multiple layers of protection instead of relying on a single security control.

### Task 6 – ISO/IEC 19249
Introduced ISO/IEC 19249 and its role in security principles.

The detailed principles listed inside the task were not included in the supplied room text, so they are not reproduced here.

### Task 7 – Zero Trust versus Trust but Verify
Covered two approaches to trust and access:
- **Zero Trust**
- **Trust but Verify**

The room compared these approaches as part of understanding modern security design.

### Task 8 – Threat versus Risk
Covered the distinction between:
- **Vulnerability**
- **Threat**
- **Risk**

These terms are related but not interchangeable.

### Task 9 – Conclusion
Completed the Security Principles room.

## Concepts to Remember

### CIA Triad

**Confidentiality**  
Protect information from unauthorised access or disclosure.

**Integrity**  
Protect information from unauthorised or improper modification.

**Availability**  
Ensure authorised users can access systems and data when needed.

### DAD Triad

**Disclosure**  
Loss of confidentiality.

**Alteration**  
Loss of integrity.

**Destruction / Denial**  
Loss of availability.

## Defence-in-Depth
Defence-in-Depth means using multiple security layers.

The purpose is to avoid depending on a single control. If one layer fails, other layers may still prevent or limit an attack.

## Zero Trust
A core Zero Trust idea is that access should not automatically be trusted simply because a user or system is inside a network.

Authentication, authorisation, and verification remain important.

## Threat, Vulnerability, and Risk
These terms should be kept separate:
- **Vulnerability:** A weakness that may be exploited.
- **Threat:** Something that may exploit a weakness and cause harm.
- **Risk:** The potential for loss or damage when a threat can exploit a vulnerability.

## Practical Security Relevance
These concepts are useful across:
- SOC analysis
- Incident response
- Network security
- System administration
- Security architecture
- Vulnerability management
- Risk assessment
- Security interviews and certifications

## Commands Practiced
This room was primarily concept-focused.

No specific commands were included in the room information supplied for this GitHub note, so no commands are recorded.

## Troubleshooting / Corrections
No specific troubleshooting issue or incorrect command was supplied for this room.

## What I Learned
- Security depends on the value of the asset and the capability of the adversary.
- No security solution is completely perfect.
- CIA represents three major security goals.
- DAD represents the failure or opposite of those security goals.
- Security models provide structured rules for protecting information.
- Defence-in-Depth uses multiple layers of protection.
- Zero Trust reduces reliance on implicit trust.
- Vulnerability, threat, and risk describe different parts of the security problem.

## Areas to Reinforce
- Bell-LaPadula rules and practical scenarios.
- Other security models introduced in the room.
- Detailed ISO/IEC 19249 principles.
- Zero Trust architecture examples.
- Threat vs vulnerability vs risk scenario identification.
- Mapping real incidents to CIA and DAD.

## Final Status
**TryHackMe – Security Principles: 100% completed.**
