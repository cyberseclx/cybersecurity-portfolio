# Day 17 — Network Devices, Cabling, Ethernet and Topologies

## Status

Completed

---

## Topics Revised

Today I revised the following Network+ topics:

- Networking Devices
- Network Communication
- Wireless Networking
- Ethernet Standards
- Optical Fiber
- Copper Cabling
- Network Transceivers
- Fiber Connectors
- Copper Connectors
- Network Topologies

---

## Networking Devices

### Hub

A hub is a Layer 1 device.

It repeats incoming traffic to all connected ports.

A hub does not intelligently forward traffic.

### Switch

A switch is a Layer 2 device.

It forwards Ethernet frames using MAC addresses.

Switches are used to connect devices inside the same LAN or VLAN.

### Router

A router is a Layer 3 device.

It forwards packets between different networks using IP addresses.

Example:

- LAN to internet
- VLAN to VLAN
- Branch office to branch office

### Firewall

A firewall controls inbound and outbound network traffic based on security rules.

It can filter traffic using:

- Source IP
- Destination IP
- Port number
- Protocol
- Application
- Connection state

### Layer 2 Switch vs Layer 3 Switch

A Layer 2 switch forwards traffic using MAC addresses.

A Layer 3 switch can also perform routing between VLANs or networks using IP addresses.

### Access Point

An access point allows wireless devices to connect to a wired network.

Example flow:

Laptop or phone → Access Point → Switch → Router

### Modem

A modem converts signals between the ISP network and the customer network.

Modem stands for:

- Modulator
- Demodulator

Example flow:

ISP line → Modem → Router → Switch or Wi-Fi

### Load Balancer

A load balancer distributes client traffic across multiple servers.

It improves:

- Performance
- Availability
- Fault tolerance

### Proxy Server

A proxy server sits between clients and the internet or between clients and servers.

It can provide:

- Filtering
- Logging
- Caching
- Access control

### IDS vs IPS

IDS stands for Intrusion Detection System.

It detects suspicious activity and alerts.

IPS stands for Intrusion Prevention System.

It detects suspicious activity and can block or prevent it.

Memory line:

IDS = Alarm

IPS = Block

---

## Network Communication Types

### Unicast

Unicast is one-to-one communication.

Example:

Client to server communication.

### Broadcast

Broadcast is one-to-all communication inside a broadcast domain.

Example:

ARP request.

### Multicast

Multicast is one-to-many selected communication.

Only interested receivers receive the traffic.

### Anycast

Anycast is one-to-nearest or one-to-best destination communication.

Example:

DNS anycast servers.

---

## Copper Cabling

Copper cabling uses electrical signals over copper wires.

Common Ethernet copper cables include:

- Cat5e
- Cat6
- Cat6a

### UTP

UTP stands for Unshielded Twisted Pair.

It is twisted pair copper cable without extra shielding.

It is commonly used in homes and offices.

### STP

STP stands for Shielded Twisted Pair.

It has shielding to reduce electromagnetic interference.

Important:

STP cable means Shielded Twisted Pair.

STP protocol means Spanning Tree Protocol.

They are different topics.

---

## Fiber Cabling

Fiber cabling uses light signals over glass or plastic fiber.

Fiber is useful for:

- Longer distance
- Higher speed
- Less electromagnetic interference

### Single-Mode Fiber

Single-mode fiber has a smaller core.

It carries one main light path.

It is used for long-distance links.

### Multi-Mode Fiber

Multi-mode fiber has a larger core.

It carries multiple light paths.

It is used for shorter-distance links.

Memory line:

Single-mode = long distance

Multi-mode = shorter distance

---

## Transceivers and Connectors

### Transceiver

A transceiver is a device or module that can transmit and receive network signals.

In networking, it can convert between electrical and optical signals.

### SFP

SFP stands for Small Form-factor Pluggable.

It is a hot-swappable transceiver module used in switches, routers, and network devices.

### RJ45

RJ45 is a copper Ethernet connector.

It is used with Ethernet cables such as Cat5e, Cat6, and Cat6a.

### LC Connector

LC is a fiber optic connector.

It is commonly used with fiber optic cables.

### Patch Panel

A patch panel is a central termination point for network cables.

Example flow:

Office wall port → Cable inside wall → Patch panel → Patch cable → Switch

Patch panels help with:

- Cable management
- Troubleshooting
- Organization
- Easy port changes

---

## Ethernet Standards

Ethernet standards define details such as:

- Speed
- Media type
- Distance
- Signaling
- Cabling requirements

### 1000BASE-T

1000 = 1000 Mbps or 1 Gbps

BASE = Baseband

T = Twisted pair copper

Meaning:

1000BASE-T is 1 Gigabit Ethernet over twisted pair copper cabling.

### 10GBASE-SR

10G = 10 Gigabit

BASE = Baseband

SR = Short Range

Meaning:

10GBASE-SR is 10 Gigabit Ethernet over short-range fiber, usually multi-mode fiber.

---

## Network Topologies

### Star Topology

In star topology, devices connect to a central switch or hub.

This is common in modern LANs.

### Mesh Topology

In mesh topology, devices have multiple paths between them.

Types:

- Full mesh
- Partial mesh

Full mesh means every device connects to every other device.

Partial mesh means only some devices have multiple connections.

### Bus Topology

Bus topology uses one main backbone cable with devices connected along it.

### Ring Topology

Ring topology connects devices in a circular path.

### Hybrid Topology

Hybrid topology combines two or more topology types.

Example:

- Star + mesh
- Star + bus

---

## Why Full Mesh Is Expensive

Full mesh is expensive because every device needs a direct connection to every other device.

This requires many:

- Cables
- Interfaces
- Switch ports
- Router ports
- Configuration effort

The number of links increases quickly as devices increase.

Formula:

n × (n - 1) / 2

Example:

5 devices need 10 links.

10 devices need 45 links.

---

## Practical Commands Used

I used the following Linux commands in Kali:

```bash
ip -br a
ip link show
ip route
ip neigh
nmcli dev status
ethtool eth0
lspci | grep -i ethernet
lsusb
