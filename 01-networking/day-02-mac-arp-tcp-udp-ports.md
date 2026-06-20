# Networking Day 2 — MAC, ARP, TCP, UDP and Ports

## Goal

Understand how devices communicate inside a local network using network interfaces, MAC addresses, ARP, TCP/UDP, and ports.

## Commands Practiced

```bash
ip link show
ip -br a
ip route
GATEWAY=$(ip route | awk '/default/ {print $3}')
echo $GATEWAY
ip neigh show
ping -c 4 $GATEWAY
ip neigh show
ping -c 4 1.1.1.1
ip neigh show
ss -tuln
ss -tun
```

## Key Concepts

### Network Interface

A network interface is the network “door” through which a device connects to a network.

Examples of network interfaces include:

* Wi-Fi adapter
* Ethernet adapter
* VPN adapter
* Loopback interface
* Virtual machine network adapter

In my Kali VM, the active network interface was `eth0`.

### eth0

`eth0` is the network interface used by my Kali Linux virtual machine.

Since Kali is running inside a VM, `eth0` is not my laptop’s physical Wi-Fi card. It is a virtual network adapter created for the Kali VM by the virtualization software.

### MAC Address

MAC stands for Media Access Control.

A MAC address belongs to a network interface and is used for communication inside a local network.

The original hardware MAC address is usually assigned by the manufacturer, but it can be spoofed or changed in software.

In my Kali VM, the MAC address was visible under the `link/ether` field for `eth0`. I am not publishing the exact MAC address publicly.

### ARP

ARP stands for Address Resolution Protocol.

ARP automatically maps a local IP address to a MAC address.

Simple memory:

```text
ARP = IP address to MAC address finder inside a local network
```

ARP is not usually done manually. Linux automatically uses ARP when it needs to communicate with a local device and does not already know that device’s MAC address.

### Default Gateway and ARP

My Kali VM had a default gateway visible in the `ip route` output.

When Kali wants to reach the internet, it first sends traffic to the default gateway. To send traffic to the gateway inside the local network, Kali needs the gateway’s MAC address.

That is why ARP is important.

Simple flow:

```text
Kali VM → ARP finds gateway MAC → Gateway → Internet
```

### TCP

TCP stands for Transmission Control Protocol.

TCP is connection-oriented and reliable. It confirms communication and delivery, so it is used when accuracy matters.

Examples:

* SSH
* HTTP
* HTTPS
* FTP
* Email

### UDP

UDP stands for User Datagram Protocol.

UDP is connectionless and does not guarantee delivery. It is useful when speed matters more than perfect reliability.

Examples:

* DNS
* Video calls
* Streaming
* Online games

### Ports

A port is a number that identifies which service or application should receive network traffic.

Analogy:

```text
IP address = building address
Port = room number
```

Important ports:

| Port  | Service |
| ----- | ------- |
| 20/21 | FTP     |
| 22    | SSH     |
| 23    | Telnet  |
| 25    | SMTP    |
| 53    | DNS     |
| 80    | HTTP    |
| 443   | HTTPS   |
| 3389  | RDP     |

## My Practical Test Results

### Test 1: Checking Interfaces and MAC Address

Command used:

```bash
ip link show
```

What I observed:

My Kali VM showed `lo` and `eth0`.

* `lo` is the loopback interface.
* `eth0` is Kali VM’s active virtual network interface.
* `link/ether` showed the MAC address for `eth0`.

I am not publishing the exact MAC address publicly.

### Test 2: Checking IP Address

Command used:

```bash
ip -br a
```

What I observed:

The output showed that `eth0` was up and had a private IPv4 address in the `10.x.x.x` range.

This confirmed that Kali had an active network interface and a private IP address.

### Test 3: Checking Default Gateway

Command used:

```bash
ip route
```

What I observed:

The output showed a default route through `eth0`.

This means Kali sends outside traffic to the default gateway first.

### Test 4: Saving the Gateway in a Variable

Command used:

```bash
GATEWAY=$(ip route | awk '/default/ {print $3}')
echo $GATEWAY
```

What I observed:

The command stored the default gateway IP into a variable called `GATEWAY`.

This helped me reuse the gateway value in later commands.

### Test 5: Checking Neighbour Table Before Ping

Command used:

```bash
ip neigh show
```

What I observed:

The neighbour table showed existing neighbour entries. At first, the gateway’s IPv4 entry was not clearly visible.

The neighbour table shows local IP-to-MAC mappings learned by the system.

### Test 6: Pinging the Gateway

Command used:

```bash
ping -c 4 $GATEWAY
```

Result:

The ping to the gateway was successful with `4 packets transmitted, 4 received, 0% packet loss`.

What this means:

Kali was able to reach its local gateway.

### Test 7: Checking Neighbour Table After Gateway Ping

Command used:

```bash
ip neigh show
```

What I observed:

After pinging the gateway, the neighbour table showed the gateway IP mapped to a MAC address.

This happened because Kali used ARP to learn the gateway’s MAC address and stored the mapping.

### Test 8: Pinging a Public IP

Command used:

```bash
ping -c 4 1.1.1.1
```

Result:

The ping was successful with `4 packets transmitted, 4 received, 0% packet loss`.

What this means:

Kali could reach the internet using a public IP address.

Important learning:

Kali did not need the MAC address of `1.1.1.1`. Since `1.1.1.1` is outside the local network, Kali only needed the MAC address of the gateway. The gateway then forwarded the traffic toward the internet.

### Test 9: Checking Listening Ports

Command used:

```bash
ss -tuln
```

What I observed:

The output showed no major listening TCP/UDP services on my Kali VM.

Meaning of options:

```text
-t = TCP
-u = UDP
-l = listening
-n = numeric output
```

### Test 10: Checking Active TCP/UDP Connections

Command used:

```bash
ss -tun
```

What I observed:

The output showed UDP traffic between Kali and the gateway using ports `68` and `67`.

This is related to DHCP.

```text
UDP 68 = DHCP client
UDP 67 = DHCP server
```

DHCP helps assign network settings such as IP address, gateway, and DNS.

## What I Learned

* `eth0` is Kali VM’s virtual network interface.
* A network interface is the network door through which a device connects to a network.
* A MAC address belongs to a network interface.
* ARP automatically maps local IP addresses to MAC addresses.
* Kali needs the gateway’s MAC address to send traffic outside the local network.
* `ip neigh show` displays local neighbour mappings.
* The neighbour table changed after pinging the gateway because Kali learned the gateway’s MAC address.
* ARP works inside the local network; it does not find the MAC address of public internet servers.
* TCP is reliable and connection-oriented.
* UDP is connectionless and does not guarantee delivery.
* Ports identify services/applications.
* `ss -tuln` shows listening TCP/UDP ports.
* `ss -tun` shows active TCP/UDP connections.
* DHCP uses UDP ports 67 and 68.

## Why This Matters in Cybersecurity

Understanding MAC addresses, ARP, TCP, UDP, and ports is important because SOC analysts, NOC analysts, network support engineers, and penetration testers need to understand how devices communicate.

These concepts are useful for:

* troubleshooting network connectivity
* understanding local network traffic
* identifying services running on systems
* reading network logs
* understanding alerts involving IPs, ports, and protocols
* later learning scanning, packet analysis, and network attacks

## Next Topics

* Common ports in more detail
* TCP three-way handshake
* Wireshark packet capture
* Basic service detection
* Subnetting fundamentals
