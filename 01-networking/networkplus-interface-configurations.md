# Network+ — Interface Configurations

## Topics Covered

* Interface Status
* Speed
* Duplex
* MTU
* Link Aggregation
* Basic Linux Interface Commands

---

## Network Interface

A network interface is the connection point between a device and a network.

Examples:

```text
Ethernet adapter
Wi-Fi adapter
Virtual machine network adapter
```

In Kali, my main interface was:

```text
eth0
```

---

## Interface Status

Linux command:

```bash
ip -br a
```

Example output:

```text
eth0 UP 10.0.2.15/24
```

Meaning:

```text
eth0 = interface name
UP = interface is active
10.0.2.15/24 = IP address and CIDR
```

---

## Speed

Speed is how fast a network interface can send or receive data.

Examples:

```text
100 Mbps
1 Gbps
10 Gbps
```

---

## Duplex

Duplex describes whether communication can happen in one direction or both directions at the same time.

```text
Half-duplex = send or receive, not both at the same time
Full-duplex = send and receive at the same time
```

Modern Ethernet normally uses full-duplex.

Speed and duplex should match between connected interfaces.

Mismatch can cause:

```text
Slow network
Collisions
Retransmissions
Poor performance
```

---

## MTU

MTU stands for Maximum Transmission Unit.

It is the maximum packet size that can be sent over a network link without fragmentation.

Common Ethernet MTU:

```text
1500 bytes
```

Wrong MTU can cause:

```text
Fragmentation
Packet drops
Slow connections
Broken VPNs
Websites not loading properly
Unstable communication
```

---

## Link Aggregation

Link aggregation combines multiple physical links into one logical link.

It is used for:

```text
More total bandwidth
Redundancy
Load balancing
```

Example:

```text
Switch A === Link 1 === Switch B
Switch A === Link 2 === Switch B
Switch A === Link 3 === Switch B

Grouped as one logical connection
```

Important correction:

```text
Link aggregation is not multiple LANs acting as one LAN.
It is multiple physical links acting as one logical link.
```

---

## Kali Practical Commands

```bash
ip -br a
ip -d link show eth0
ip route
ip neigh
ss -tuln
tcpdump -D
```

Observed:

```text
eth0 was UP
Kali IP was 10.0.2.15/24
Gateway was 10.0.2.2
tcpdump showed eth0 as capture interface
```

---

## Interview Lines

Speed means how fast an interface can transmit data.

Duplex means whether communication is one-way at a time or both ways at the same time.

MTU is the maximum packet size that can be sent without fragmentation.

Link aggregation combines multiple physical links into one logical link for bandwidth and redundancy.
