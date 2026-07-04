# Network+ — VLANs, Trunking, Access Ports, and Inter-VLAN Routing

## Topics Covered

* VLANs
* Access Ports
* Trunk Ports
* 802.1Q
* Inter-VLAN Routing

---

## VLAN

VLAN stands for Virtual Local Area Network.

A VLAN is a logical Layer 2 network created on a switch.

It separates devices into different broadcast domains even if they are connected to the same physical switch.

Example:

```text
VLAN 10 = HR
VLAN 20 = Finance
VLAN 30 = IT
```

Each VLAN usually maps to a different IP subnet.

Example:

```text
VLAN 10 → 192.168.10.0/24
VLAN 20 → 192.168.20.0/24
VLAN 30 → 192.168.30.0/24
```

---

## Why Companies Use VLANs

Companies use VLANs for:

```text
Department separation
Security
Reducing broadcast traffic
Better network organization
Access control
```

Example:

```text
HR systems should not be in the same broadcast domain as guest Wi-Fi devices.
```

---

## Access Port

An access port is a switch port assigned to one VLAN.

It is usually used for end devices.

Examples:

```text
PC
Printer
IP phone
Camera
```

Example:

```text
Switch port 1 → Access port → VLAN 10 → HR PC
Switch port 2 → Access port → VLAN 20 → Finance PC
```

Access ports usually carry untagged traffic from the end device.

---

## Trunk Port

A trunk port carries traffic for multiple VLANs.

Trunk ports are commonly used between:

```text
Switch to switch
Switch to router
Switch to firewall
Switch to Layer 3 switch
```

Example:

```text
Switch A ===== trunk ===== Switch B

Traffic carried:
VLAN 10
VLAN 20
VLAN 30
```

---

## 802.1Q

802.1Q is the VLAN tagging standard used on trunk links.

It adds a VLAN tag to Ethernet frames so the receiving device knows which VLAN the frame belongs to.

Simple memory line:

```text
802.1Q = VLAN tagging on trunk links
```

---

## Why VLAN 10 Cannot Talk to VLAN 20 by Default

VLANs are separate Layer 2 broadcast domains.

Usually, each VLAN also belongs to a separate IP subnet.

Example:

```text
VLAN 10 → 192.168.10.0/24
VLAN 20 → 192.168.20.0/24
```

Traffic between VLANs requires Layer 3 routing.

---

## Inter-VLAN Routing

Inter-VLAN routing allows devices in different VLANs to communicate.

Devices that can perform inter-VLAN routing:

```text
Router
Layer 3 switch
Firewall
```

Devices that cannot perform inter-VLAN routing by themselves:

```text
Layer 2 switch
Hub
```

---

## Real-World Example

```text
HR PC:
IP address: 192.168.10.50
VLAN: 10
Gateway: 192.168.10.1

Finance PC:
IP address: 192.168.20.50
VLAN: 20
Gateway: 192.168.20.1
```

If HR wants to communicate with Finance, traffic must go through a router, Layer 3 switch, or firewall.

---

## Interview Lines

A VLAN is a logical Layer 2 network that separates devices into different broadcast domains.

An access port belongs to one VLAN and is usually used for end devices.

A trunk port carries multiple VLANs between network devices.

802.1Q is the standard used to tag VLAN traffic on trunk links.

Inter-VLAN routing is required when devices in different VLANs need to communicate.
