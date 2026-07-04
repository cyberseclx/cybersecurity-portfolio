# Network+ — Spanning Tree Protocol and Loop Prevention

## Topics Covered

* Switching Loops
* Broadcast Storms
* STP
* Root Bridge
* Port Blocking
* Redundancy

---

## The Problem STP Solves

STP stands for Spanning Tree Protocol.

STP prevents Layer 2 switching loops.

Layer 2 Ethernet frames do not have TTL like Layer 3 IP packets.

Because of this, if a Layer 2 loop exists, frames can continue circulating endlessly.

---

## Switching Loop

A switching loop happens when there are multiple active Layer 2 paths between switches.

Example:

```text
Switch A ===== Switch B
   |             |
   |             |
Switch C =========
```

If all links are active and no loop prevention exists, frames can loop continuously.

---

## Why Layer 2 Loops Are Dangerous

Layer 2 loops can cause:

```text
Broadcast storms
MAC address table instability
Duplicate frames
High switch CPU usage
Network slowdown
Network outage
```

---

## Broadcast Storm

A broadcast storm happens when broadcast frames loop and multiply across switches.

Example:

```text
ARP request = broadcast traffic
```

If ARP broadcasts loop repeatedly, they can consume bandwidth and affect the entire network.

Important distinction:

```text
Unknown destination MAC flooding is normal switch behavior.
Broadcast storm is repeated broadcast traffic caused by loops.
```

---

## STP

STP creates a loop-free Layer 2 topology.

It keeps some links forwarding and blocks other redundant links.

If the active link fails, STP can unblock a backup path.

---

## Root Bridge

The root bridge is the central reference switch elected by STP.

All switches calculate their best loop-free path toward the root bridge.

The root bridge is selected using bridge priority and MAC address.

Memory line:

```text
Root bridge = main reference switch for STP path calculation
```

---

## Why STP Blocks Ports

STP blocks some ports to prevent loops.

The blocked port is not useless. It can become active if the main forwarding path fails.

This gives both:

```text
Loop prevention
Redundancy
```

---

## Redundancy Risk

Redundancy is good because it provides backup paths.

But redundant Layer 2 links can become dangerous if all paths forward traffic at the same time.

Without STP, redundancy can create loops.

With STP, one path forwards and another path can stay blocked as backup.

---

## Interview Lines

STP prevents Layer 2 switching loops.

Layer 2 loops are dangerous because Ethernet frames do not have TTL.

A broadcast storm happens when broadcast frames loop and consume network bandwidth.

The root bridge is the central reference switch used by STP to calculate loop-free paths.

STP blocks some ports to prevent loops while still keeping backup links available.
