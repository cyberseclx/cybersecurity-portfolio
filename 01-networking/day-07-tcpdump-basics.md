# Day 07 — Tcpdump Basics

## Room / Topic

TryHackMe Cyber Security 101 — Tcpdump: The Basics

## What I Practiced

Today I practiced using `tcpdump`, a command-line packet capture and packet analysis tool. This helped me understand how to capture live traffic from a network interface, apply filters, save packets into a `.pcap` file, and read saved packet captures.

## Key Concepts

### tcpdump

`tcpdump` is a command-line tool used to capture and inspect network packets.

### libpcap

`libpcap` is the packet capture library used by tcpdump.

### Interface

An interface is a network adapter such as `eth0` or `lo`. Tcpdump needs an interface to know where to capture traffic from.

### PCAP

A `.pcap` file is a saved packet capture file. It can be opened later using tcpdump or Wireshark.

## Commands Practiced

### Create lab folder

```bash
mkdir -p ~/portfolio-labs/day07-tcpdump
cd ~/portfolio-labs/day07-tcpdump
pwd
```

### Check active interface

```bash
ip -br a
```

Active interface found:

```text
eth0
```

### Check tcpdump version

```bash
tcpdump --version
```

### List capture interfaces

```bash
tcpdump -D
```

### Basic packet capture

```bash
sudo tcpdump -i eth0 -c 5
```

Meaning:

* `sudo` = required for packet capture permission
* `-i eth0` = capture on eth0 interface
* `-c 5` = stop after 5 packets

### Capture ICMP traffic

```bash
sudo tcpdump -i eth0 icmp -c 4
```

This captured ping request and reply packets.

### Save packets to a file

```bash
sudo tcpdump -i eth0 icmp -c 4 -w day07-icmp.pcap
```

Meaning:

* `-w` writes packets to a pcap file.

### Read saved packet capture

```bash
tcpdump -r day07-icmp.pcap
```

Meaning:

* `-r` reads packets from a saved pcap file.

### Capture TCP traffic

```bash
sudo tcpdump -i eth0 tcp -c 5
```

### Capture UDP traffic

```bash
sudo tcpdump -i eth0 udp -c 5
```

### Filter by host

```bash
sudo tcpdump -i eth0 host 8.8.8.8 -c 5
```

### Filter by port

```bash
sudo tcpdump -i eth0 port 53 -c 5
```

This showed DNS traffic.

### Disable name and port resolution

```bash
sudo tcpdump -i eth0 -nn -c 5
```

Meaning:

* `-n` disables hostname resolution
* `-nn` disables hostname and port name resolution

### Show packet data in hex and ASCII

```bash
sudo tcpdump -i eth0 -X -c 3
```

Meaning:

* `-X` shows packet contents in hex and ASCII.

## Important Output Observations

* Tcpdump without `sudo` gave a permission error.
* `eth0` was the active interface.
* ICMP traffic showed echo request and echo reply packets.
* DNS traffic appeared on port 53.
* `-nn` showed raw IP addresses and port numbers.
* `-X` displayed packet content including readable text like `google.com`.

## Key Takeaway

Wireshark is useful for visual packet analysis, but tcpdump is powerful for terminal-based packet capture, especially on Linux servers, SSH sessions, SOC work, and quick troubleshooting.
