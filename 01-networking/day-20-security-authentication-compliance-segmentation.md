# Day 20 — Network+ Security, Authentication, Compliance and Segmentation

## GitHub Path

`01-networking/day-20-security-authentication-compliance-segmentation.md`

## Clockify Block

`D20-B03 | Network+ Practical | Security Auth Compliance Segmentation`

## Lab Directory

```bash
/home/kali/cyber_project/kali_practise/networking/network-security-auth-segmentation
```

## Lab Files Created

```text
auth_events.log
security_alerts.log
segmentation_rules.txt
compliance_checklist.txt
```

## Topics Covered

```text
Security concepts
Authentication and MFA
IDS / IPS / WAF / EDR / DLP / SIEM / NAC
Regulatory compliance
Network segmentation
DMZ
Firewall-style allow/deny rules
Important service ports
```

# 1. Authentication Log Analysis

## Command

```bash
grep "status=failed" auth_events.log
```

## Output

```text
2026-07-09 09:02:11 user=admin action=login status=failed mfa=no src_ip=203.0.113.44
2026-07-09 09:02:31 user=admin action=login status=failed mfa=no src_ip=203.0.113.44
2026-07-09 09:03:12 user=admin action=login status=failed mfa=no src_ip=203.0.113.44
2026-07-09 09:05:42 user=guest action=login status=failed mfa=no src_ip=192.168.50.10
```

## Interpretation

```text
There were four failed login attempts.
Three failed logins were for the admin user from the same source IP: 203.0.113.44.
This may indicate brute force or credential guessing.
```

# 2. MFA Check

## Command

```bash
grep "mfa=no" auth_events.log
```

## Interpretation

```text
All failed login attempts had MFA disabled.
This shows why MFA is important for reducing account takeover risk.
```

# 3. Count Failed Login Source IPs

## Command

```bash
grep "status=failed" auth_events.log | awk '{print $7}' | sort | uniq -c
```

## Output

```text
1 src_ip=192.168.50.10
3 src_ip=203.0.113.44
```

## Interpretation

```text
203.0.113.44 had three failed login attempts.
192.168.50.10 had one failed login attempt.
Repeated failed logins from the same IP can indicate brute force, password spraying, or suspicious authentication activity.
```

# 4. High and Critical Security Alerts

## Command

```bash
grep -E "severity=high|severity=critical" security_alerts.log
```

## Output

```text
alert_id=1002 technology=IPS severity=high action=blocked src=198.51.100.23 dst=192.168.30.20 reason=malware_connection
alert_id=1003 technology=WAF severity=high action=blocked src=203.0.113.88 dst=DMZ_WEB reason=sql_injection_attempt
alert_id=1004 technology=EDR severity=critical action=quarantined host=WIN-CLIENT-01 reason=suspicious_powershell
alert_id=1005 technology=DLP severity=high action=blocked user=guest reason=upload_customer_data_to_personal_email
alert_id=1006 technology=SIEM severity=high action=correlated reason=failed_logins_plus_admin_success
```

## Interpretation

```text
IPS blocked a malware connection.
WAF blocked a SQL injection attempt against the DMZ web server.
EDR quarantined suspicious PowerShell activity on an endpoint.
DLP blocked possible customer data exfiltration.
SIEM correlated failed logins with admin success.
```

# 5. Security Technology Meanings

```text
IDS = detects suspicious activity and alerts.
IPS = detects and blocks suspicious traffic.
WAF = protects web applications from web attacks like SQL injection and XSS.
EDR = monitors and responds to endpoint threats.
DLP = prevents sensitive data from leaving the organization.
SIEM = collects and correlates logs to generate security alerts.
NAC = controls which users/devices can connect to the network.
```

# 6. Segmentation Rules

## Command

```bash
grep "DENY" segmentation_rules.txt
```

## Output

```text
DENY Guest_VLAN Internal_DB ANY
DENY IoT_VLAN Internal_LAN ANY
DENY Internet Internal_LAN ANY
DENY Users_VLAN Network_Devices SSH_22
```

## Interpretation

```text
Guest VLAN is blocked from internal database.
IoT VLAN is blocked from internal LAN.
Internet is blocked from internal LAN.
Users VLAN is blocked from SSH access to network devices.
These rules reduce lateral movement and protect sensitive systems.
```

# 7. DMZ Rules

## Command

```bash
grep "DMZ_WEB" segmentation_rules.txt
```

## Output

```text
ALLOW Users_VLAN DMZ_WEB TCP_443
ALLOW DMZ_WEB Internal_DB TCP_3306
```

## Interpretation

```text
Users can access the DMZ web server using HTTPS on TCP 443.
The DMZ web server can access the internal database on TCP 3306.
DMZ systems should have only the minimum required access to internal systems.
```

# 8. Compliance Checks

## PCI DSS

```text
PCI_DSS: payment_card_data must be encrypted
PCI_DSS: access_logs must be retained
```

Meaning:

```text
PCI DSS is related to payment card data security.
Common controls include encryption, access logs, segmentation and access control.
```

## GDPR

```text
GDPR: personal_data must support deletion request
```

Meaning:

```text
GDPR is related to personal data protection and privacy for people in the European Union.
```

Other compliance memory:

```text
HIPAA = healthcare and patient data
SOX = financial reporting controls
```

# 9. Kali Network Checks

## Command

```bash
ip -br a
```

## Output

```text
lo               UNKNOWN        127.0.0.1/8 ::1/128
eth0             UP             10.0.2.15/24 fd17:625c:f037:2:4e17:4901:4904:93cb/64 fd17:625c:f037:2:a00:27ff:fe08:b07e/64 fe80::a00:27ff:fe08:b07e/64
```

## Interpretation

```text
lo is the loopback interface.
eth0 is up.
IPv4 address is 10.0.2.15/24.
IPv6 addresses are also present.
fe80:: indicates a link-local IPv6 address.
```

# 10. Listening Services Check

## Command

```bash
ss -tuln
```

## Output

```text
No listening services displayed.
```

## Interpretation

```text
No obvious TCP/UDP services are listening on the Kali VM.
This reduces unnecessary exposure.
```

# 11. Important Ports Observed in /etc/services

## Command

```bash
grep -E "ssh|domain|kerberos|ldap|radius|tacacs|https|http|rdp" /etc/services | head -n 30
```

## Important Ports

```text
SSH = TCP 22
TACACS = TCP/UDP 49
DNS/domain = TCP/UDP 53
HTTP = TCP 80
Kerberos = TCP/UDP 88
LDAP = TCP/UDP 389
HTTPS = TCP/UDP 443
LDAPS = TCP/UDP 636
RADIUS = TCP/UDP 1812
RADIUS Accounting = TCP/UDP 1813
HTTP alternate = TCP 8080
```

Network+ memory:

```text
RADIUS = VPN, Wi-Fi and 802.1X authentication
TACACS+ = network device administration
Kerberos = Windows domain authentication
LDAP = directory access
DNS = name resolution
SSH = secure remote shell
HTTPS = encrypted web traffic
```

# 12. Key Learning from Lab

```text
Repeated failed logins from the same IP may indicate brute force.
MFA reduces account takeover risk.
IDS alerts, IPS blocks.
WAF protects web applications.
EDR protects endpoints.
DLP prevents sensitive data leakage.
SIEM correlates logs and generates alerts.
NAC blocks untrusted devices from joining the network.
Segmentation limits attacker movement.
DMZ protects internal networks from direct internet exposure.
Compliance requirements often require logging, encryption and access control.
```

# 13. Weak Areas to Revise

```text
EDR vs SIEM
NAC vs Firewall
DLP vs Encryption
802.1X components
RADIUS vs TACACS+
DMZ design
Firewall segmentation
ACLs
HIPAA
SOX
East-west vs north-south traffic
```

# Final Status

```text
Network+ Security Practical Completed.
Lab practiced authentication log analysis, failed login counting, MFA review, high severity alert filtering, segmentation rules, compliance checks, interface review, listening service checks and important service ports.
```
