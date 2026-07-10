# Day 21 - Network+ Security Attacks Detection Practical

## Block

**Clockify:** `D21-B03 | Network+ Practical | Security Attacks Detection`  
**Project:** `CS Sprint | Practical Labs`

## Lab Folder

```bash
/home/kali/cyber_project/kali_practise/networking/network-security-attacks-day21
```

Files created:

```bash
network_attacks.log
prevention_map.txt
```

## Practical Objective

This was a safe SOC/NOC-style detection practical. No real attacks were performed. The goal was to read simulated logs and identify:

- DoS / DDoS
- VLAN Hopping
- MAC Flooding
- ARP Poisoning
- DNS Poisoning
- Rogue DHCP / Rogue DNS
- Social Engineering
- Malware

---

## Evidence Collected

### 1. DoS / DDoS

```bash
2026-07-10 10:00:01 attack=DoS src_ip=198.51.100.10 dst=web_server requests=9500 status=service_slow
2026-07-10 10:00:02 attack=DDoS src_ip=multiple dst=web_server requests=85000 status=service_unavailable
```

**Interpretation:**

- DoS used one source.
- DDoS used multiple sources.
- Impact was service slowdown/unavailability.

**SOC/NOC signs:** high request count, service slow/down, possible bandwidth or resource exhaustion.

---

### 2. VLAN Hopping

```bash
2026-07-10 10:02:15 attack=VLAN_Hopping src_port=Gi0/12 event=unexpected_vlan_tag vlan=20 native_vlan=1
```

**Interpretation:** Unexpected VLAN tag was seen on a switch port. Native VLAN 1 is also a weak configuration sign.

**Defense:** Disable DTP, set user ports manually as access ports, avoid native VLAN 1, restrict allowed VLANs on trunks, disable unused ports.

---

### 3. MAC Flooding

```bash
2026-07-10 10:03:41 attack=MAC_Flooding src_port=Gi0/18 learned_macs=520 status=cam_table_pressure
```

**Interpretation:** One switch port learned too many MAC addresses. This points to CAM table pressure / possible MAC flooding.

**Defense:** Port security, MAC address limit per port, sticky MAC, disable unused ports, switch monitoring.

---

### 4. ARP Poisoning

```bash
2026-07-10 10:04:20 attack=ARP_Poisoning victim_ip=192.168.1.25 gateway_ip=192.168.1.1 fake_mac=aa:bb:cc:dd:ee:ff
```

**Interpretation:** The attacker is trying to map the gateway IP to a fake MAC address. This can create a man-in-the-middle situation.

**Memory:**

```text
ARP poisoning = IP address to MAC address trick
```

**Defense mapping:**

```bash
ARP_Poisoning: Dynamic_ARP_Inspection DHCP_snooping static_ARP HTTPS monitor_ARP_changes
```

---

### 5. DNS Poisoning

```bash
2026-07-10 10:05:11 attack=DNS_Poisoning domain=bank.example resolved_ip=203.0.113.66 expected_ip=192.0.2.10
```

**Interpretation:** The domain resolved to the wrong IP address. This can redirect users to a fake site.

**Memory:**

```text
DNS poisoning = domain name to IP address trick
```

**Defense mapping:**

```bash
DNS_Poisoning: DNSSEC secure_resolver DNS_filtering monitor_DNS_records clear_DNS_cache
```

---

### 6. Rogue DHCP / Rogue DNS

```bash
2026-07-10 10:06:44 attack=Rogue_DHCP detected_server=192.168.1.200 offered_gateway=192.168.1.200 offered_dns=192.168.1.200
2026-07-10 10:07:55 attack=Rogue_DNS server=192.168.1.201 domain=google.com fake_ip=203.0.113.99
```

**Interpretation:**

Rogue DHCP can give users wrong network settings:

- Wrong IP
- Wrong gateway
- Wrong DNS

Rogue DNS can give wrong domain-to-IP answers.

**Defense mapping:**

```bash
Rogue_DHCP_DNS: DHCP_snooping NAC asset_inventory disable_unused_ports network_monitoring
```

---

### 7. Social Engineering

```bash
2026-07-10 10:08:33 attack=Social_Engineering type=phishing user=finance clicked_link=yes submitted_password=yes
```

**Interpretation:** A finance user clicked a phishing link and submitted a password.

**Impact:** Credential theft, account compromise, possible unauthorized access.

**Defense:** Awareness training, MFA, email filtering, verification process, reporting culture.

---

### 8. Malware

```bash
2026-07-10 10:09:10 attack=Malware type=ransomware host=WIN-CLIENT-01 files_encrypted=yes outbound_ip=185.199.110.153
2026-07-10 10:10:27 attack=Malware type=worm host=WIN-CLIENT-02 spreading=yes dst_ports=445,135
2026-07-10 10:11:05 attack=Malware type=trojan host=WIN-CLIENT-03 source=cracked_software backdoor=yes
```

**Interpretation:**

- Ransomware encrypted files.
- Worm was spreading over the network.
- Trojan came from cracked software and installed a backdoor.

**Defense:** EDR / antivirus, patching, backups, email filtering, least privilege, application control, user training.

---

## Attack Count

```bash
      1 attack=ARP_Poisoning
      1 attack=DDoS
      1 attack=DNS_Poisoning
      1 attack=DoS
      1 attack=MAC_Flooding
      3 attack=Malware
      1 attack=Rogue_DHCP
      1 attack=Rogue_DNS
      1 attack=Social_Engineering
      1 attack=VLAN_Hopping
```

**Key finding:** Malware had the highest count with 3 entries.

---

## Real Kali Network Checks

### Interface

```bash
lo               UNKNOWN        127.0.0.1/8 ::1/128
eth0             UP             10.0.2.15/24 fd17:625c:f037:2:d3c5:1328:e802:9501/64 fd17:625c:f037:2:a00:27ff:fe08:b07e/64 fe80::a00:27ff:fe08:b07e/64
```

**Interpretation:** Kali has active interface `eth0` with IPv4 address `10.0.2.15/24`. It also has IPv6 addresses, including a link-local address starting with `fe80::`.

### Route

```bash
default via 10.0.2.2 dev eth0 proto dhcp src 10.0.2.15 metric 100
10.0.2.0/24 dev eth0 proto kernel scope link src 10.0.2.15 metric 100
```

**Interpretation:** Default gateway is `10.0.2.2`.

### Neighbor / ARP Table

```bash
fd17:625c:f037:2::2 dev eth0 lladdr 52:54:00:12:35:00 router STALE
fe80::2 dev eth0 lladdr 52:54:00:12:35:00 router STALE
```

**Interpretation:** The neighbor table shows IPv6 router entries. In a real ARP poisoning check, we would look for gateway IP mapped to unexpected or changing MAC addresses.

### DNS Resolver

```bash
# Generated by NetworkManager
nameserver 192.168.1.1
nameserver fd17:625c:f037:2::3
```

**Interpretation:** Kali is using DNS servers `192.168.1.1` and `fd17:625c:f037:2::3`. For DNS poisoning or rogue DNS checks, verify that DNS servers are expected and trusted.

### Listening Services

```bash
ss -tuln
```

Output showed no listening services.

**Interpretation:** No TCP/UDP services are listening on this Kali machine in the current output. That is good from a basic exposure point of view.

---

## Key Memory Corrections

```text
DoS/DDoS = service availability attack
VLAN hopping = unauthorized VLAN access
MAC flooding = CAM table overflow
ARP poisoning = IP-to-MAC trick
DNS poisoning = domain-to-IP trick
Rogue DHCP = wrong IP/gateway/DNS settings
Rogue DNS = wrong domain-to-IP answers
Social engineering = human manipulation
Malware = malicious software
```

## Weak Areas To Repair

```text
VLAN hopping methods: switch spoofing and double tagging
MAC spoofing vs switch spoofing
ARP poisoning vs DNS poisoning
Rogue DHCP impact
Rogue DNS impact
SOC/NOC alert signs
Defense mapping per attack
```
