# Network+ — Static Routing, Dynamic Routing, and Routing Technologies

## Topics Covered

* Static Routing
* Dynamic Routing
* Routing Technologies
* Default Route
* Longest Prefix Match
* RIP
* OSPF
* BGP

---

## Switching vs Routing

Switching happens inside the same LAN or VLAN using MAC addresses.

Routing happens between different networks using IP addresses.

```text
Switching = Layer 2 = MAC address
Routing   = Layer 3 = IP address
```

Example:

```text
PC1 to PC2 in same VLAN → switching
VLAN 10 to VLAN 20      → routing
LAN to internet         → routing
```

---

## Routing Table

A routing table tells a device where to send traffic.

On Linux, the routing table can be viewed with:

```bash
ip route
```

Example from Kali:

```text
default via 10.0.2.2 dev eth0
10.0.2.0/24 dev eth0
```

Meaning:

```text
10.0.2.0/24 dev eth0
Traffic for local subnet 10.0.2.0/24 goes directly through eth0.

default via 10.0.2.2 dev eth0
Traffic for unknown destinations goes to default gateway 10.0.2.2.
```

---

## Default Route

A default route is used when no more specific route exists in the routing table.

It is commonly written as:

```text
0.0.0.0/0
```

Example:

```text
default via 10.0.2.2 dev eth0
```

This means:

```text
If destination is not local or specifically known, send traffic to 10.0.2.2 through eth0.
```

---

## Static Routing

A static route is manually configured by an administrator.

Example concept:

```text
To reach 192.168.20.0/24, send traffic to next-hop router 192.168.10.1
```

Advantages:

```text
Simple for small networks
Predictable path
No routing protocol overhead
```

Disadvantages:

```text
Does not scale well
Manual changes required
No automatic failover unless configured
Difficult to manage in large networks
```

---

## Dynamic Routing

Dynamic routing uses routing protocols so routers can automatically learn and update routes.

Routers share routing information with each other.

Advantages:

```text
Scales better
Automatically adapts to network changes
Useful in large networks
```

Disadvantages:

```text
More complex
Requires correct configuration
Can consume CPU, memory, and bandwidth
```

---

## RIP

RIP stands for Routing Information Protocol.

Important points:

```text
Old routing protocol
Uses hop count
Maximum hop count is 15
16 means unreachable
```

Memory line:

```text
RIP = old + hop count
```

---

## OSPF

OSPF stands for Open Shortest Path First.

Important points:

```text
Common internal routing protocol
Used inside organizations
Link-state routing protocol
Finds best path based on cost
```

Memory line:

```text
OSPF = common internal routing protocol
```

---

## BGP

BGP stands for Border Gateway Protocol.

Important points:

```text
Used on the internet
Routes between autonomous systems
Used by ISPs and large networks
```

Memory line:

```text
BGP = internet routing
```

---

## Longest Prefix Match

Routers choose the most specific matching route.

Example routes:

```text
10.0.0.0/8
10.10.10.0/24
0.0.0.0/0
```

Destination:

```text
10.10.10.50
```

Winning route:

```text
10.10.10.0/24
```

Reason:

```text
/24 is more specific than /8 and /0.
```

---

## Kali Practical Commands

```bash
ip -br a
ip route
ip neigh
ping -c 4 10.0.2.2
sudo tcpdump -i eth0 icmp -c 4
```

What I observed:

```text
Kali IP: 10.0.2.15/24
Default gateway: 10.0.2.2
Interface: eth0
ICMP ping to gateway worked
tcpdump captured ICMP echo request and echo reply
```

---

## Interview Lines

Switching forwards frames inside the same LAN or VLAN using MAC addresses.

Routing forwards packets between different networks using IP addresses.

A default route is used when no specific route exists for a destination.

Static routes are manually configured, while dynamic routes are learned using routing protocols.

RIP uses hop count, OSPF is commonly used inside organizations, and BGP is used for internet routing.
