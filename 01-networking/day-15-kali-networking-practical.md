# Day 15 — Kali Networking Practical

## Purpose

Today I connected Network+ theory with Kali Linux practical commands.

The focus was:

```text
Interfaces
IP addressing
Routing table
Default gateway
ARP / neighbor table
Listening ports
Packet capture
ICMP traffic
```

---

## Commands Practiced

```bash
ip -br a
ip route
ip neigh
ss -tuln
tcpdump -D
ip -d link show eth0
ping -c 4 10.0.2.2
sudo tcpdump -i eth0 icmp -c 4
```

---

## Interface Output

My main interface:

```text
eth0
```

My Kali IP:

```text
10.0.2.15/24
```

Meaning:

```text
IP address: 10.0.2.15
CIDR: /24
Subnet: 10.0.2.0/24
```

---

## Routing Table

Output:

```text
default via 10.0.2.2 dev eth0
10.0.2.0/24 dev eth0
```

Meaning:

```text
Traffic for 10.0.2.0/24 stays local through eth0.
Traffic for unknown destinations goes to default gateway 10.0.2.2.
```

---

## Neighbor Table

Command:

```bash
ip neigh
```

Observed gateway mapping:

```text
10.0.2.2 → MAC address 52:54:00:12:35:00
```

This shows ARP / neighbor discovery.

Concept:

```text
IP address = Layer 3
MAC address = Layer 2
ARP maps IP addresses to MAC addresses inside a local network.
```

---

## Packet Capture

Command:

```bash
sudo tcpdump -i eth0 icmp -c 4
```

I captured ICMP traffic while pinging the gateway.

Observed:

```text
ICMP echo request
ICMP echo reply
0 packets dropped
```

This proves:

```text
Kali can reach the default gateway.
tcpdump can capture live traffic.
ICMP request and reply are visible on the interface.
```

---

## Concepts Connected

```text
ip -br a       → interface and IP address
ip route       → routing table and default gateway
ip neigh       → ARP/IP-to-MAC mapping
ss -tuln       → listening ports/services
tcpdump -D     → available capture interfaces
tcpdump icmp   → live ICMP packet capture
```

---

## Key Takeaway

This practical helped connect Network+ theory with real Linux commands.

I saw how an endpoint has:

```text
Interface
IP address
Subnet
Default gateway
Neighbor table
Routing table
Live packets
```

This is useful for IT support, NOC, SOC, and cybersecurity troubleshooting.
