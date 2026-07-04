# Network+ — IPv4, Binary Math, CIDR, Subnetting, and VLSM

## Topics Covered

* Binary Math
* IPv4 Addressing
* Classful Subnetting
* IPv4 Subnet Masks
* Calculating IPv4 Subnets and Hosts
* Magic Number Subnetting
* Seven Second Subnetting
* CIDR
* VLSM

---

## IPv4 Addressing

IPv4 is a 32-bit addressing system.

An IPv4 address has 4 octets.

Example:

```text
192.168.1.10
```

Each octet has 8 bits.

```text
8 bits + 8 bits + 8 bits + 8 bits = 32 bits
```

So IPv4 is called a 32-bit address.

---

## CIDR

CIDR stands for Classless Inter-Domain Routing.

Example:

```text
192.168.1.10/24
```

The `/24` means the first 24 bits are network bits.

Since IPv4 has 32 bits:

```text
32 - 24 = 8 host bits
```

So:

```text
Network bits = 24
Host bits = 8
```

---

## Subnet Mask

A subnet mask separates the network portion and host portion of an IP address.

Example:

```text
192.168.1.10/24
Subnet mask = 255.255.255.0
```

Common subnet masks:

```text
/24 = 255.255.255.0
/25 = 255.255.255.128
/26 = 255.255.255.192
/27 = 255.255.255.224
/28 = 255.255.255.240
/29 = 255.255.255.248
/30 = 255.255.255.252
```

---

## Important Subnetting Table

```text
CIDR   Mask              Block Size   Total IPs   Usable Hosts
/24    255.255.255.0     256          256         254
/25    255.255.255.128   128          128         126
/26    255.255.255.192   64           64          62
/27    255.255.255.224   32           32          30
/28    255.255.255.240   16           16          14
/29    255.255.255.248   8            8           6
/30    255.255.255.252   4            4           2
```

---

## Host Calculation Formula

```text
Host bits = 32 - CIDR
Total IPs = 2^host bits
Usable hosts = Total IPs - 2
```

The two reserved addresses are:

```text
Network address
Broadcast address
```

Example:

```text
/26
Host bits = 32 - 26 = 6
Total IPs = 2^6 = 64
Usable hosts = 64 - 2 = 62
```

---

## Magic Number / Block Size

The block size helps find subnet ranges.

Formula:

```text
Block size = 256 - subnet mask value
```

Example:

```text
/27 = 255.255.255.224
Block size = 256 - 224 = 32
```

So the subnet ranges go by 32:

```text
0 - 31
32 - 63
64 - 95
96 - 127
128 - 159
160 - 191
192 - 223
224 - 255
```

---

## Example 1 — 192.168.1.75/26

```text
CIDR:           /26
Subnet mask:    255.255.255.192
Block size:     64
```

Ranges:

```text
192.168.1.0   - 192.168.1.63
192.168.1.64  - 192.168.1.127
192.168.1.128 - 192.168.1.191
192.168.1.192 - 192.168.1.255
```

`192.168.1.75` falls inside:

```text
192.168.1.64 - 192.168.1.127
```

Answer:

```text
Network address: 192.168.1.64
First usable:    192.168.1.65
Last usable:     192.168.1.126
Broadcast:       192.168.1.127
Usable hosts:    62
```

---

## Example 2 — 10.10.5.130/27

```text
CIDR:           /27
Subnet mask:    255.255.255.224
Block size:     32
```

Ranges:

```text
10.10.5.0   - 10.10.5.31
10.10.5.32  - 10.10.5.63
10.10.5.64  - 10.10.5.95
10.10.5.96  - 10.10.5.127
10.10.5.128 - 10.10.5.159
10.10.5.160 - 10.10.5.191
10.10.5.192 - 10.10.5.223
10.10.5.224 - 10.10.5.255
```

`10.10.5.130` falls inside:

```text
10.10.5.128 - 10.10.5.159
```

Answer:

```text
Network address: 10.10.5.128
First usable:    10.10.5.129
Last usable:     10.10.5.158
Broadcast:       10.10.5.159
Usable hosts:    30
```

---

## VLSM

VLSM stands for Variable Length Subnet Mask.

It allows different subnet sizes based on actual host requirements.

Example:

```text
Sales needs 100 hosts      → /25
IT needs 50 hosts          → /26
HR needs 25 hosts          → /27
Management needs 10 hosts  → /28
```

VLSM prevents IP wastage.

Without VLSM, every department may get the same large subnet even if they do not need it.

---

## Interview Lines

IPv4 is a 32-bit addressing system divided into 4 octets.

CIDR shows how many bits belong to the network portion.

Subnetting divides a larger network into smaller networks.

VLSM allows different subnet sizes based on different host requirements and reduces IP wastage.

For host calculation, I use the formula: host bits equal 32 minus CIDR, total IPs equal 2 to the power of host bits, and usable hosts equal total IPs minus 2.
