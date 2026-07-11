# Day 22 - Network+ Troubleshooting Device Security Issues Practical

## Block

**Clockify:** `D22-B03 | Network+ Practical | Troubleshooting Device Security Issues`  
**Project:** `CS Sprint | Practical Labs`

## Lab Folder

```bash
/home/kali/cyber_project/kali_practise/networking/network-troubleshooting-day22
```

## Files Created

```bash
troubleshooting_events.log
fix_map.txt
```

## Practical Objective

This was a safe Network+ troubleshooting practical.

The goal was to identify issues from logs and map each issue to:

- Layer
- Category
- Evidence
- Fix

---

## 1. Cable Problem

### Evidence

```bash
2026-07-11 09:00:01 issue=Cable_Problem host=PC-01 symptom=link_light_off evidence=no_carrier probable_layer=Layer1
```

### Interpretation

This is a Layer 1 physical issue.

Important signs:

```text
link_light_off
no_carrier
```

### Fix Map

```bash
Cable_Problem: check_link_light reseat_cable replace_cable use_cable_tester check_patch_panel
```

### Memory

```text
No link light = cable/interface/hardware check first.
```

---

## 2. Interface Down

### Evidence

```bash
2026-07-11 09:03:22 issue=Interface_Down device=SW-01 port=Gi0/10 status=administratively_down probable_layer=Layer2
```

### Interpretation

The port is disabled by configuration.

### Fix Map

```bash
Interface_Down: enable_interface check_admin_status verify_speed_duplex check_errors
```

### Memory

```text
Administratively down = disabled by admin/config.
```

---

## 3. Switching Issues

### Evidence

```bash
2026-07-11 09:05:10 issue=Wrong_VLAN host=PC-02 port=Gi0/15 expected_vlan=20 actual_vlan=30 probable_layer=Layer2
2026-07-11 09:21:20 issue=STP_Change device=SW-03 event=frequent_topology_change suspected=switching_loop probable_layer=Layer2
2026-07-11 09:25:40 issue=Port_Security device=SW-04 port=Gi0/22 status=err_disabled reason=mac_violation probable_layer=Layer2
```

### Interpretation

These are Layer 2 switching issues.

- Wrong VLAN = port assigned to incorrect VLAN.
- STP change = possible switching loop or unstable link.
- Port security = switch port shut down due to MAC violation.

### Fix Maps

```bash
Wrong_VLAN: verify_access_vlan correct_vlan_assignment check_switchport_config
Port_Security: check_MAC_limit verify_allowed_MAC clear_violation enable_port
```

### Memory

```text
Wrong VLAN = Layer 2.
STP = loop prevention.
Port security violation = unauthorized or unexpected MAC.
```

---

## 4. Routing / IP Issues

### Evidence

```bash
2026-07-11 09:07:44 issue=DHCP_Failure host=LAPTOP-01 ip=169.254.10.25 gateway=none probable_layer=Layer3
2026-07-11 09:12:30 issue=Default_Gateway_Problem host=PC-04 ip=192.168.10.44 gateway=192.168.99.1 probable_layer=Layer3
2026-07-11 09:28:11 issue=Duplicate_IP host1=PC-05 host2=PRINTER-01 ip=192.168.20.55 probable_layer=Layer3
2026-07-11 09:31:33 issue=NAT_Problem host=PC-06 can_ping_gateway=yes can_ping_8.8.8.8=no probable_layer=Layer3
```

### Interpretation

These are Layer 3 routing/IP issues.

- `169.254.x.x` = DHCP failed / APIPA.
- Wrong gateway = device may not reach outside local network.
- Duplicate IP = two devices have same IP.
- Can ping gateway but not `8.8.8.8` = problem beyond local LAN, such as NAT/firewall/upstream route.

### Fix Maps

```bash
DHCP_Failure: check_DHCP_server check_scope renew_DHCP check_vlan_helper_address
NAT_Problem: check_default_route check_NAT check_firewall check_upstream_ISP
```

### Memory

```text
169.254.x.x = DHCP failed.
Can ping gateway but not 8.8.8.8 = routing/NAT/firewall/upstream issue.
```

---

## 5. DNS Problem

### Evidence

```bash
2026-07-11 09:10:15 issue=DNS_Problem host=PC-03 can_ping_ip=yes can_resolve_domain=no dns_server=wrong probable_layer=Layer7
```

### Interpretation

The host can reach an IP address but cannot resolve domain names.

### Fix Map

```bash
DNS_Problem: check_resolv_conf use_nslookup use_dig correct_DNS_server
```

### Memory

```text
Can ping IP but not domain = DNS issue.
```

---

## 6. Firewall / ACL Block

### Evidence

```bash
2026-07-11 09:15:51 issue=Firewall_ACL_Block src=Users_VLAN dst=Web_Server port=443 action=deny probable_layer=Layer4
```

### Interpretation

Traffic to TCP port 443 is denied by firewall/ACL.

### Fix Map

```bash
Firewall_ACL_Block: check_firewall_rules check_ACL_order allow_required_port verify_logs
```

### Memory

```text
Server is up and routing is correct but port is blocked = check firewall/ACL/security rule.
```

---

## 7. Hardware Failure

### Evidence

```bash
2026-07-11 09:18:04 issue=Hardware_Failure device=SW-02 symptom=fan_alarm temperature=high probable_layer=Physical
```

### Interpretation

The switch has a fan/temperature issue. This is a physical hardware problem.

### Memory

```text
Fan alarm / overheating / power issue = hardware issue.
```

---

## 8. Issue Count

```bash
      1 issue=Cable_Problem
      1 issue=Default_Gateway_Problem
      1 issue=DHCP_Failure
      1 issue=DNS_Problem
      1 issue=Duplicate_IP
      1 issue=Firewall_ACL_Block
      1 issue=Hardware_Failure
      1 issue=Interface_Down
      1 issue=NAT_Problem
      1 issue=Port_Security
      1 issue=STP_Change
      1 issue=Wrong_VLAN
```

All simulated issue types appeared once.

---

## 9. Real Kali Network Checks

### IP Address

```bash
eth0             UP             10.0.2.15/24
```

Interpretation:

```text
Kali interface eth0 is up.
IPv4 address is 10.0.2.15/24.
```

### Default Gateway

```bash
default via 10.0.2.2 dev eth0 proto dhcp src 10.0.2.15 metric 100
```

Interpretation:

```text
Default gateway is 10.0.2.2.
```

### Neighbor / ARP Table

```bash
10.0.2.2 dev eth0 lladdr 52:54:00:12:35:00 STALE
fe80::2 dev eth0 lladdr 52:54:00:12:35:00 router STALE
fd17:625c:f037:2::2 dev eth0 lladdr 52:54:00:12:35:00 router STALE
```

Interpretation:

```text
Gateway/neighbor entries are visible.
In ARP troubleshooting, watch for duplicate or changing MAC mappings.
```

### DNS Servers

```bash
nameserver 192.168.1.1
nameserver fd17:625c:f037:2::3
```

Interpretation:

```text
Kali is using 192.168.1.1 and fd17:625c:f037:2::3 as DNS servers.
```

### Listening Services

```bash
ss -tuln
```

Output showed no listening services.

Interpretation:

```text
No local listening TCP/UDP services were shown in this output.
```

---

## 10. ethtool Evidence

```bash
Speed: 1000Mb/s
Duplex: Full
Auto-negotiation: on
Port: Twisted Pair
Link detected: yes
```

Interpretation:

```text
eth0 link is detected.
Speed is 1000Mb/s.
Duplex is full.
Auto-negotiation is on.
The port type is twisted pair.
```

This is useful for cable/interface troubleshooting.

---

## 11. Command Mistakes Fixed

### Case-sensitive grep

Wrong:

```bash
grep "Cable_problem" troubleshooting_events.log
```

Correct:

```bash
grep "Cable_Problem" troubleshooting_events.log
```

Linux is case-sensitive by default.

### grep -i placement

Wrong:

```bash
grep "Cable_Problem"-i troubleshooting_events.log
```

Correct:

```bash
grep -i "Cable_Problem" troubleshooting_events.log
```

### Typo

Wrong:

```bash
gre "Cable_Problem" troubleshooting_events.log
```

Correct:

```bash
grep "Cable_Problem" troubleshooting_events.log
```

### Regex pipe spacing

Wrong:

```bash
grep -E "Wrong_VLAN | STP_Change | Port_Security" troubleshooting_events.log
```

Better:

```bash
grep -E "Wrong_VLAN|STP_Change|Port_Security" troubleshooting_events.log
```

Do not add spaces around `|` unless the log text actually contains those spaces.

---

## 12. Key Memory Rules

```text
Layer 1 = cable / physical
Layer 2 = switch / VLAN / MAC / STP
Layer 3 = IP / gateway / routing / subnet / NAT
Layer 4 = port / TCP / UDP / firewall rule
Layer 7 = DNS / application-level issue
```

Troubleshooting logic:

```text
No link light = cable/interface/hardware
Administratively down = interface disabled
Wrong VLAN = Layer 2 switching issue
169.254.x.x = DHCP failure
Can ping IP but not domain = DNS issue
Can ping gateway but not 8.8.8.8 = routing/NAT/firewall/upstream issue
Port 443 denied = firewall/ACL/security rule
Fan alarm / overheating = hardware issue
```

---

## 13. Weak Areas To Repair

```text
Security rules vs device security
Routing/IP issue definition
Native VLAN mismatch
Broadcast storm
Layer 2 signs
Layer 3 signs
Command evidence
Firewall/ACL scenario logic
```
