# Day 17 — Windows Fundamentals 3

## Room / Topic

TryHackMe — Windows Fundamentals 3

## Status

Completed

---

## What I Practiced

Today I completed Windows Fundamentals 3.

This room focused on built-in Windows security tools that help protect a Windows system.

Topics covered:

- Windows Updates
- Windows Security
- Virus & threat protection
- Firewall & network protection
- App & browser control
- Device security
- BitLocker
- Volume Shadow Copy Service

This room is useful for:

- IT Support
- SOC Analyst L1
- System Admin Trainee
- Endpoint Security
- Windows Troubleshooting

---

## Windows Updates

Windows Updates keep the operating system updated.

Updates may include:

- Security patches
- Bug fixes
- Driver updates
- Feature updates
- Stability improvements

### Security Importance

Unpatched systems are easier to attack.

Many malware attacks target known vulnerabilities.

Regular updates reduce the attack surface.

### Interview Line

Windows Updates are important because they patch vulnerabilities, improve stability, and reduce the risk of exploitation.

---

## Windows Security

Windows Security is the central security dashboard in Windows.

It includes:

- Virus & threat protection
- Account protection
- Firewall & network protection
- App & browser control
- Device security
- Device performance & health
- Protection history

### Real-World Use

Windows Security helps check:

- Antivirus status
- Firewall status
- Protection history
- Security warnings
- Device health

### Interview Line

Windows Security is the built-in Windows dashboard for managing antivirus, firewall, browser protection, device security, and protection history.

---

## Virus & Threat Protection

Virus & threat protection is used to protect the system from malware and suspicious files.

Important features:

- Microsoft Defender Antivirus
- Quick scan
- Full scan
- Custom scan
- Offline scan
- Real-time protection
- Protection history

### Microsoft Defender

Microsoft Defender is the built-in Windows antivirus and anti-malware solution.

It helps detect:

- Viruses
- Trojans
- Spyware
- Ransomware
- Suspicious files
- Potentially unwanted applications

### Interview Line

Virus & threat protection uses Microsoft Defender to detect and respond to malware, suspicious files, and other threats.

---

## Firewall & Network Protection

Windows Firewall controls network traffic allowed into or out of the system.

Firewall profiles:

- Domain network
- Private network
- Public network

### Domain Network

Used when the system is connected to a workplace domain.

Example:

- Corporate Active Directory network

### Private Network

Used for trusted networks.

Examples:

- Home Wi-Fi
- Trusted office network

### Public Network

Used for untrusted networks.

Examples:

- Cafe Wi-Fi
- Airport Wi-Fi
- Public hotspot

The public profile is usually the strictest.

### Interview Line

Windows Firewall protects the system by controlling inbound and outbound network traffic using domain, private, and public profiles.

---

## App & Browser Control

App & browser control helps protect users from unsafe apps, files, websites, and downloads.

Important features:

- Reputation-based protection
- Microsoft Defender SmartScreen
- Exploit protection

### SmartScreen

SmartScreen helps protect users from:

- Malicious websites
- Suspicious downloads
- Unknown applications
- Phishing pages

### Interview Line

App & browser control helps protect users from malicious websites, suspicious downloads, and unsafe applications using SmartScreen and reputation-based protection.

---

## Device Security

Device security shows hardware-based security features available on the system.

Common areas:

- Core isolation
- Memory integrity
- TPM
- Secure Boot

### TPM

TPM stands for Trusted Platform Module.

TPM is used for:

- BitLocker key protection
- Secure credential storage
- Device identity
- Hardware-backed security

### Secure Boot

Secure Boot helps ensure that only trusted boot software runs during startup.

### Interview Line

Device security shows hardware-backed protections such as TPM, Secure Boot, core isolation, and memory integrity.

---

## BitLocker

BitLocker is Microsoft’s full-disk encryption feature.

It protects data at rest by encrypting the drive.

Main purpose:

- Protect data if a laptop or drive is lost or stolen.

BitLocker can use:

- TPM
- Recovery key
- PIN
- Password

### Interview Line

BitLocker provides full-disk encryption to protect data at rest, especially if a device is lost or stolen.

---

## Volume Shadow Copy Service

Volume Shadow Copy Service is also called VSS.

VSS allows Windows to create snapshots of files or volumes.

Uses:

- Restore previous versions of files
- Backup support
- System restore support
- Recovery after accidental deletion or modification

### Security Relevance

Ransomware may try to delete shadow copies to prevent recovery.

Example ransomware behavior:

- Encrypt files
- Delete shadow copies
- Prevent victim from restoring previous versions

### Interview Line

Volume Shadow Copy Service creates snapshots that can help restore previous versions of files, but attackers may delete shadow copies during ransomware attacks.

---

## Important Windows Security Tools Learned

| Tool / Feature | Purpose |
|---|---|
| Windows Updates | Installs patches, security fixes, drivers, and feature updates |
| Windows Security | Central dashboard for Windows security features |
| Microsoft Defender | Built-in antivirus and anti-malware protection |
| Virus & threat protection | Scans and detects malware |
| Firewall & network protection | Controls network traffic |
| App & browser control | Protects against unsafe apps, downloads, and websites |
| SmartScreen | Warns about suspicious websites, apps, and downloads |
| Device security | Shows hardware-backed security features |
| TPM | Hardware security module used for features like BitLocker |
| Secure Boot | Helps prevent untrusted boot software |
| BitLocker | Full-disk encryption |
| Volume Shadow Copy Service | Backup and restore snapshots |

---

## Real-World IT Support Use

This room is useful for IT support because these tools help troubleshoot and secure Windows endpoints.

Examples:

- Check Windows Update status
- Run Microsoft Defender scan
- Review protection history
- Check firewall profile
- Allow or block apps through firewall
- Check SmartScreen protection
- Verify BitLocker status
- Recover files using previous versions

---

## SOC Analyst Relevance

This room is useful for SOC basics because Windows endpoints are common targets.

SOC use cases:

- Review Defender alerts
- Check malware detections
- Investigate suspicious downloads
- Check firewall status
- Look for security warnings
- Check if ransomware deleted shadow copies
- Verify whether security tools are enabled

---

## Key Takeaways

- Windows Updates patch vulnerabilities.
- Windows Security is the central dashboard for built-in protection.
- Microsoft Defender provides antivirus and threat protection.
- Firewall profiles change based on network trust level.
- Public network profile is usually stricter than private or domain.
- App & browser control helps protect against malicious apps and websites.
- SmartScreen warns users about suspicious websites and files.
- Device security includes TPM, Secure Boot, core isolation, and memory integrity.
- BitLocker protects data at rest.
- Volume Shadow Copy Service helps restore previous file versions.
- Ransomware may delete shadow copies to prevent recovery.

---

## Interview Lines

Windows Updates patch vulnerabilities and reduce the attack surface.

Windows Security is the built-in dashboard for antivirus, firewall, browser protection, device security, and protection history.

Microsoft Defender is the built-in Windows antivirus and anti-malware solution.

Windows Firewall controls inbound and outbound network traffic using domain, private, and public profiles.

BitLocker provides full-disk encryption to protect data at rest.

Volume Shadow Copy Service creates snapshots that can help restore previous versions of files.

Ransomware may delete shadow copies to prevent recovery.
