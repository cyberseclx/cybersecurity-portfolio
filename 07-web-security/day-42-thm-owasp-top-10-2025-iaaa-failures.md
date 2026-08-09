# Day 42 – TryHackMe OWASP Top 10 2025: IAAA Failures

## Room

- **Path:** Cyber Security 101
- **Module:** OWASP Top 10 (2025)
- **Room:** OWASP Top 10 2025: IAAA Failures
- **Status:** Completed – 100%
- **Estimated room time:** 30 minutes

## Objective

Understand OWASP Top 10 2025 categories related to failures in the implementation of:

- Identity
- Authentication
- Authorisation
- Accountability

These four areas form the **IAAA model**.

## OWASP Categories Covered

The room covered three OWASP Top 10 2025 categories:

1. **A01: Broken Access Control**
2. **A07: Authentication Failures**
3. **A09: Logging & Alerting Failures**

## Task 1 – Introduction

The room introduced IAAA failures and explained that weaknesses in Identity, Authentication, Authorisation, and Accountability can lead to serious application-security problems.

The room combines theory with supporting practical challenges.

## Task 2 – What is IAAA?

The room introduced the four IAAA components:

### Identity

Identity is concerned with who a user, account, or entity claims to be.

### Authentication

Authentication is concerned with verifying that claimed identity.

### Authorisation

Authorisation determines what an authenticated user or entity is permitted to access or perform.

### Accountability

Accountability is concerned with being able to trace actions and events back to users, systems, or processes.

## Task 3 – A01: Broken Access Control

This task covered:

**A01: Broken Access Control**

Broken access control occurs when an application fails to correctly enforce restrictions on what users are allowed to access or do.

The detailed challenge steps and answers were not included in the supplied room information, so they are not recorded here.

## Task 4 – A07: Authentication Failures

This task covered:

**A07: Authentication Failures**

Authentication failures relate to weaknesses in how applications verify users or protect authentication mechanisms.

The specific examples, challenge steps, and answers were not included in the supplied room information, so no additional details are invented.

## Task 5 – A09: Logging & Alerting Failures

This task covered:

**A09: Logging & Alerting Failures**

This category relates to failures in recording important security events and alerting when suspicious or malicious activity occurs.

The specific logging examples and challenge answers were not included in the supplied room information.

## Task 6 – Conclusion

Completed the OWASP Top 10 2025: IAAA Failures room.

## Key Distinctions

The most important conceptual distinction from this room is:

```text
Identity != Authentication
Authentication != Authorisation
Authorisation != Accountability
```

A simple way to remember the flow:

```text
Identity       -> Who are you claiming to be?
Authentication -> Can you prove it?
Authorisation  -> What are you allowed to do?
Accountability -> Can your actions be traced and reviewed?
```

## Security Failure Mapping

### Broken Access Control

Main area:

```text
Authorisation
```

The application fails to correctly enforce what a user should be allowed to access or perform.

### Authentication Failures

Main area:

```text
Authentication
```

The application fails to correctly verify or protect user authentication.

### Logging & Alerting Failures

Main area:

```text
Accountability
```

Security-relevant activity may not be properly recorded, monitored, or alerted on.

## Practical Security Relevance

These concepts are directly useful for:

- Web application security
- SOC investigations
- Authentication monitoring
- Access-control reviews
- Incident detection
- Penetration testing
- Security testing
- Application-security assessments

## Questions to Ask During Testing

For an application, think about:

```text
Who is the user?
How is the user's identity verified?
What resources/actions should the user be allowed to access?
Is access control enforced on every request?
Are important actions logged?
Would suspicious activity trigger an alert?
```

## Challenges

The room included supporting practical challenges.

Exact commands, payloads, URLs, answers, and flags were not supplied for this GitHub note and are therefore not recorded rather than being guessed.

## Troubleshooting / Corrections

No specific troubleshooting issue was supplied for this room.

## What I Learned

- IAAA stands for Identity, Authentication, Authorisation, and Accountability.
- Authentication and authorisation are different security functions.
- Broken Access Control is closely connected to failures in authorisation.
- Authentication Failures involve weaknesses in verifying or protecting user identities.
- Logging & Alerting Failures reduce accountability and make attacks harder to detect.
- Application security depends not only on preventing attacks but also on recording and detecting suspicious activity.

## Areas to Reinforce

- Broken Access Control scenarios.
- Horizontal vs vertical access-control issues.
- Authentication attack patterns.
- Secure session and credential handling.
- Security logging requirements.
- Alerting and monitoring logic.
- Mapping OWASP findings back to IAAA.

## Final Status

**TryHackMe – OWASP Top 10 2025: IAAA Failures: 100% completed.**
