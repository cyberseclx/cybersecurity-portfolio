# Day 19 — Disaster Recovery, Redundancy, IPv6, DNS, Time Protocols and Remote Access

## Status

Completed

---

## Topics Revised

Today I revised the following Network+ topics:

- Disaster Recovery
- Network Redundancy
- IPv6 and SLAAC
- An Overview of DNS
- DNS Records
- Time Protocols
- Remote Access

---

## Disaster Recovery

Disaster recovery is the process of restoring systems, data, networks, and services after a failure, outage, cyberattack, or disaster.

Disaster recovery focuses on getting IT systems back online.

---

## Business Continuity

Business continuity is the plan that allows a business to continue operating during or after a disruption.

Difference:

- Business continuity = keeping the business running
- Disaster recovery = restoring IT systems after failure

Examples of business continuity planning:

- Alternate work locations
- Backup communication methods
- Manual processes
- Disaster recovery plan
- Backup internet links
- Backup power

---

## RTO

RTO stands for Recovery Time Objective.

RTO defines how quickly a system or service must be restored after a failure.

Memory line:

```text
RTO = maximum acceptable downtime
```

Example:

```text
RTO = 2 hours
Service must be restored within 2 hours.
```

---

## RPO

RPO stands for Recovery Point Objective.

RPO defines how much data loss is acceptable, measured in time.

Memory line:

```text
RPO = maximum acceptable data loss
```

Example:

```text
RPO = 15 minutes
Business can tolerate losing only the last 15 minutes of data.
```

---

## RTO vs RPO

| Term | Meaning |
|---|---|
| RTO | Maximum acceptable downtime |
| RPO | Maximum acceptable data loss |

Memory:

```text
RTO = time to recover
RPO = data loss window
```

---

## Backup Types

### Full Backup

A full backup backs up all selected data every time the backup runs.

Example:

```text
Sunday full backup = backs up everything selected.
```

### Incremental Backup

An incremental backup backs up only the data changed since the last backup of any type.

Example:

```text
Sunday = full backup
Monday = changes since Sunday
Tuesday = changes since Monday
Wednesday = changes since Tuesday
```

Advantage:

- Faster backup
- Uses less storage

Disadvantage:

- Restore may take longer because the full backup and every incremental backup after it may be needed

### Differential Backup

A differential backup backs up all data changed since the last full backup.

Example:

```text
Sunday = full backup
Monday = changes since Sunday
Tuesday = changes since Sunday
Wednesday = changes since Sunday
```

Advantage:

- Restore is easier than incremental because only the full backup and latest differential backup are needed

Memory:

```text
Incremental = since last backup
Differential = since last full backup
```

---

## Backup Testing

Backups should be tested to confirm that data can actually be restored during a real failure.

Important line:

```text
A backup that cannot be restored is useless.
```

---

## Failover

Failover is the process of automatically or manually switching from a failed primary system to a backup system.

Example:

```text
Primary firewall fails → backup firewall takes over
```

---

## Network Redundancy

Redundancy means having backup devices, links, paths, power, or systems so service can continue if the primary component fails.

Examples:

- Redundant switches
- Redundant routers
- Redundant firewalls
- Multiple DNS servers
- Multiple DHCP servers
- Dual ISP links
- Dual power supplies
- UPS
- Generator
- Redundant uplinks
- Load balancers
- Clustered servers

---

## Single Point of Failure

A single point of failure is one component whose failure can bring down the whole service or network.

Examples:

- Only one internet connection
- Only one firewall
- Only one core switch
- Only one power supply
- Only one DNS server

---

## High Availability

High availability means designing systems to stay operational with minimal downtime.

High availability often uses:

- Redundancy
- Failover
- Load balancing
- Monitoring
- Backup links

---

## Active-Active

Active-active means two or more systems are active at the same time and share traffic or load.

If one fails, the remaining active system continues handling traffic.

---

## Active-Passive

Active-passive means one system is active and another system is on standby.

The passive device waits for the active device to fail.

When the active device fails, the passive device takes over.

---

## Cost and Complexity of Redundancy

Redundancy improves uptime but increases cost and complexity.

Reasons:

- More devices
- More licenses
- More configuration
- More rack space
- More power
- More monitoring
- More troubleshooting complexity

---

## IPv6

IPv6 is a newer IP addressing system designed to replace IPv4.

Important facts:

- IPv6 = 128 bits
- IPv4 = 32 bits
- IPv6 uses hexadecimal
- IPv6 does not use broadcast
- IPv6 uses unicast, multicast, and anycast

---

## Important IPv6 Addresses

| IPv6 Address | Meaning |
|---|---|
| fe80::/10 | Link-local address range |
| ::1 | Loopback address |
| :: | Unspecified address |

### fe80::

`fe80::` usually indicates a link-local IPv6 address.

Link-local addresses are used on the local network segment.

### ::1

`::1` is the IPv6 loopback address.

IPv4 equivalent:

```text
127.0.0.1
```

### ::

`::` is the IPv6 unspecified address.

It means no address or unspecified address.

---

## SLAAC

SLAAC stands for Stateless Address Autoconfiguration.

SLAAC allows an IPv6 device to automatically configure its own IPv6 address without needing a DHCP server.

Simple SLAAC flow:

```text
Device creates link-local address
Device sends Router Solicitation
Router sends Router Advertisement
Device learns prefix
Device creates IPv6 address
```

SLAAC uses Neighbor Discovery Protocol.

---

## Router Advertisement

A Router Advertisement is an IPv6 NDP message sent by a router.

It can advertise:

- Network prefix
- Default gateway information
- SLAAC information

Router Advertisements can be sent periodically or in response to Router Solicitations.

---

## DNS

DNS stands for Domain Name System.

DNS resolves human-readable domain names into IP addresses.

Example:

```text
google.com → IP address
```

DNS is important because users remember names more easily than IP addresses.

---

## DNS Resolver

A DNS resolver receives DNS queries from clients and finds the answer.

It may:

- Check local cache
- Query root servers
- Query TLD servers
- Query authoritative DNS servers

---

## DNS Lookup Flow

Simple DNS lookup flow:

```text
Client asks resolver
Resolver checks cache
Resolver asks root server
Root points to TLD server
TLD points to authoritative server
Authoritative server gives final answer
```

---

## Root DNS Server

Root DNS servers do not store all domain records.

They point DNS resolvers to the correct TLD servers.

Example:

```text
For google.com, root server points toward .com TLD servers.
```

---

## TLD Server

A TLD server manages top-level domains such as:

- .com
- .org
- .net
- .in

A TLD server points the resolver to the authoritative DNS server for the domain.

---

## Authoritative DNS Server

An authoritative DNS server holds the final DNS records for a domain.

Example:

```text
The authoritative server for example.com knows the A, AAAA, MX, TXT, and other records for example.com.
```

---

## DNS Cache and TTL

DNS cache stores previous DNS answers temporarily so future lookups are faster.

TTL stands for Time To Live.

TTL defines how long a DNS record can be cached.

---

## Forward Lookup vs Reverse Lookup

Forward lookup resolves a domain name to an IP address.

Reverse lookup resolves an IP address to a domain name.

| Lookup Type | Meaning |
|---|---|
| Forward lookup | Name to IP |
| Reverse lookup | IP to name |

---

## DNS Records

| Record | Purpose |
|---|---|
| A | Hostname/domain to IPv4 address |
| AAAA | Hostname/domain to IPv6 address |
| CNAME | Alias to another canonical name |
| MX | Mail server for a domain |
| TXT | Text information such as SPF, DKIM, DMARC, verification |
| NS | Authoritative name servers for a domain |
| PTR | Reverse DNS, IP address to hostname |
| SOA | Zone authority information |
| SRV | Service location |

---

## MX Record

MX stands for Mail Exchanger.

MX records identify mail servers for a domain.

---

## TXT Record

TXT records store text information for a domain.

Common uses:

- SPF
- DKIM
- DMARC
- Domain verification
- Security validation

---

## PTR Record

PTR records map an IP address to a hostname.

PTR records are used for reverse DNS lookup.

Example:

```text
1.1.1.1 → one.one.one.one
```

---

## SRV Record

SRV records identify the location of a service.

They can include:

- Service
- Protocol
- Port
- Target host
- Priority
- Weight

SRV records are used by services such as Active Directory, SIP, and XMPP.

---

## NTP

NTP stands for Network Time Protocol.

NTP synchronizes time across devices.

NTP is important for:

- Logs
- Authentication
- Kerberos
- Certificates
- Scheduled tasks
- Troubleshooting
- SOC investigations

---

## NTP and Logs

NTP is important for logs because accurate time helps correlate events across multiple systems.

Example:

```text
Firewall log
Windows log
VPN log
EDR log
```

All need matching time for proper investigation.

---

## NTP and Kerberos

Kerberos is time-sensitive.

If the client and domain controller times are too far apart, authentication can fail.

---

## Remote Access

Remote access allows administrators or users to connect to systems remotely.

Common remote access technologies:

- SSH
- RDP
- VPN
- VNC
- Telnet
- Jump box

---

## Remote Access Ports

| Protocol | Port | Notes |
|---|---|---|
| SSH | TCP 22 | Secure remote command line |
| Telnet | TCP 23 | Insecure cleartext remote command line |
| RDP | TCP 3389 | Windows Remote Desktop |

---

## SSH vs Telnet

SSH provides encrypted remote command-line access.

Telnet provides remote command-line access in cleartext and is insecure.

Memory:

```text
SSH = encrypted
Telnet = cleartext
```

---

## VPN

VPN stands for Virtual Private Network.

A VPN creates an encrypted tunnel between a user/device and a private network.

Use case:

```text
Remote worker securely connects to company network.
```

---

## RDP Security

RDP should not be exposed directly to the internet.

Reasons:

- Brute force attacks
- Credential theft
- Exploitation
- Ransomware access
- Unauthorized remote login attempts

Better approach:

- Use VPN
- Use MFA
- Restrict source IPs
- Use a jump box
- Monitor logs
- Disable unused RDP

---

## Jump Box

A jump box is a hardened intermediate server used to access internal systems securely.

Flow:

```text
Admin → VPN / MFA → Jump Box → Internal Server
```

Purpose:

- Centralized access control
- Logging
- Reduced exposure of internal servers
- Better monitoring

---

## Securing Remote Access

Ways to secure remote access:

- Use VPN
- Use MFA
- Use SSH instead of Telnet
- Restrict access by IP address
- Use strong passwords or SSH keys
- Disable unused remote access services
- Do not expose RDP directly to the internet
- Use a jump box
- Monitor login logs
- Apply least privilege
- Patch remote access services
- Use account lockout policies

---

## Kali Practical

I practiced DNS, IPv6, NTP/time, and remote access related commands in Kali.

Practical folder:

```text
~/cyber_project/kali_practise/dns-ipv6-time-remote-access
```

Commands used:

```bash
pwd
date
timedatectl
ip -br a
ip -6 addr
ip -6 route
cat /etc/resolv.conf
nslookup google.com
nslookup -type=A google.com
nslookup -type=AAAA google.com
nslookup -type=CNAME google.com
nslookup -type=MX google.com
nslookup -type=TXT google.com
nslookup -type=NS google.com
nslookup 1.1.1.1
ping -c 4 1.1.1.1
ping -c 4 google.com
ssh -V
ss -tuln
ss -tun
```

---

## Practical Findings

### Time and NTP

`timedatectl` showed:

```text
Time zone: Asia/Kolkata (IST, +0530)
System clock synchronized: yes
NTP service: active
```

This means time synchronization is working.

---

### IPv6 Addresses

`ip -6 addr` showed:

```text
::1/128 scope host
fd17:625c:f037:2::/64 scope global dynamic
fe80::a00:27ff:fe08:b07e/64 scope link
```

Meaning:

- `::1` = loopback
- `fd17:...` = dynamic IPv6 address
- `fe80::...` = link-local IPv6 address

---

### IPv6 Routing

`ip -6 route` showed:

```text
fd17:625c:f037:2::/64 dev eth0 proto ra
default via fe80::2 dev eth0 proto ra
```

Important learning:

```text
proto ra means the route came from Router Advertisement.
```

This connects directly to SLAAC and IPv6 Router Advertisements.

---

### DNS Resolver Configuration

`/etc/resolv.conf` showed:

```text
nameserver 192.168.1.1
nameserver fd17:625c:f037:2::3
```

This means the system has both IPv4 and IPv6 DNS resolvers configured.

---

### DNS A and AAAA Records

`nslookup google.com` returned IPv4 and IPv6 addresses.

`nslookup -type=A google.com` returned IPv4 addresses.

`nslookup -type=AAAA google.com` returned IPv6 addresses.

---

### CNAME Record Check

`nslookup -type=CNAME google.com` returned no answer.

This means `google.com` itself is not a CNAME record.

The output showed SOA authority information instead.

---

### MX Record

`nslookup -type=MX google.com` showed:

```text
google.com mail exchanger = 10 smtp.google.com.
```

This means Google has an MX record pointing to `smtp.google.com` with priority 10.

---

### TXT Record

`nslookup -type=TXT google.com` returned multiple TXT records.

One important record was:

```text
v=spf1 include:_spf.google.com ~all
```

This is related to SPF email security.

The output also showed:

```text
Truncated, retrying in TCP mode.
```

This happened because the TXT response was large.

DNS commonly uses UDP first, but can retry using TCP when the response is too large.

---

### NS Record

`nslookup -type=NS google.com` showed:

```text
ns1.google.com
ns2.google.com
ns3.google.com
ns4.google.com
```

These are Google name servers.

---

### Reverse DNS / PTR Record

`nslookup 1.1.1.1` showed:

```text
1.1.1.1.in-addr.arpa name = one.one.one.one.
```

This is a reverse DNS lookup using a PTR record.

---

### Connectivity Tests

Ping to `1.1.1.1` succeeded:

```text
4 packets transmitted
4 received
0% packet loss
```

Ping to `google.com` also succeeded:

```text
4 packets transmitted
4 received
0% packet loss
```

This confirms:

- IP connectivity works
- DNS resolution works

---

### SSH Version

`ssh -V` showed OpenSSH installed.

This confirms SSH client is available for remote access.

---

### Listening Services

`ss -tuln` showed no visible listening TCP/UDP services.

`ss -tun` showed DHCP client traffic:

```text
10.0.2.15:68 → 10.0.2.2:67
```

Meaning:

- Local DHCP client port = UDP 68
- DHCP server port = UDP 67

---

## Mistakes Corrected

### timedateclt typo

Wrong:

```bash
timedateclt
```

Correct:

```bash
timedatectl
```

### Missing slash in /etc/resolv.conf

Wrong:

```bash
cat etc/resolv.conf
```

Correct:

```bash
cat /etc/resolv.conf
```

Important:

```text
/etc/resolv.conf is an absolute path.
```

---

## Weak Areas Found Today

I need to revise:

- Full backup vs incremental vs differential
- Failover
- Single point of failure
- IPv6 = 128-bit
- fe80:: = link-local
- ::1 = loopback
- :: = unspecified
- SLAAC process
- Router Advertisement
- Root DNS vs TLD vs authoritative DNS
- MX record
- TXT record security uses
- PTR record
- SRV record
- RDP port 3389
- RDP internet exposure risk
- Remote access hardening

---

## Interview Lines

RTO is the maximum acceptable downtime.

RPO is the maximum acceptable data loss.

A full backup backs up all selected data.

An incremental backup backs up changes since the last backup.

A differential backup backs up changes since the last full backup.

Failover is the process of switching from a failed primary system to a backup system.

A single point of failure is one component whose failure can bring down the whole service.

IPv6 is 128-bit and uses hexadecimal.

SLAAC allows an IPv6 device to automatically configure its own address using Router Advertisements.

DNS resolves domain names into IP addresses.

A records map names to IPv4 addresses.

AAAA records map names to IPv6 addresses.

MX records identify mail servers.

TXT records are often used for SPF, DKIM, DMARC, and domain verification.

PTR records are used for reverse DNS lookups.

NTP synchronizes time across network devices.

Kerberos is time-sensitive, so NTP is important in Active Directory environments.

SSH uses TCP 22.

Telnet uses TCP 23 and is insecure.

RDP uses TCP 3389.

RDP should not be exposed directly to the internet because it is commonly targeted by attackers.

A jump box is a hardened intermediate server used to access internal systems securely.

---

## Final Takeaway

This block connected disaster recovery, redundancy, IPv6, DNS, time synchronization, and remote access.

The most important practical lessons were:

```text
RTO = downtime limit
RPO = data loss limit
IPv6 uses Router Advertisements for SLAAC
fe80:: means link-local
DNS records can be tested with nslookup
NTP must be active for accurate logs and Kerberos
RDP should be protected behind VPN/MFA/jump box
```
