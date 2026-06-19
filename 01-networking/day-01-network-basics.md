# Networking Day 1 — Kali Linux Network Basics

## Goal

Understand how my Kali Linux virtual machine connects to a network, reaches the internet, and resolves domain names using DNS.

## Commands Practiced

```bash
ip a
ip route
cat /etc/resolv.conf
ping -c 4 1.1.1.1
ping -c 4 google.com
nslookup google.com
```

## Key Concepts

### IP Address

An IP address is an address given to a device on a network so it can send and receive data.

### Private IP Address

A private IP address is used inside a local network such as a home, office, or virtual machine network. Private IP addresses are not directly reachable from the public internet.

Common private IP ranges include:

```text
10.x.x.x
172.16.x.x - 172.31.x.x
192.168.x.x
```

### Public IP Address

A public IP address is used on the internet. Usually, a home router or ISP connection has a public IP address, while devices inside the home or VM network use private IP addresses.

### Default Gateway

A default gateway is the router or network path used by a system when it needs to reach another network or the internet.

Simple flow:

```text
Kali VM → Default Gateway → Internet
```

### DNS

DNS stands for Domain Name System. DNS resolves human-readable domain names into IP addresses.

Example:

```text
google.com → IP address
```

Computers communicate using IP addresses, but humans usually remember names. DNS connects both.

## My Practical Test Results

### Test 1: Checking the Network Interface

Command used:

```bash
ip a
```

What I observed:

My Kali VM used `eth0` as the active network interface. I also saw the loopback interface `lo`, which is used by the system to communicate with itself.

My Kali VM received a private IP address in the `10.x.x.x` range. I am not publishing the exact IP address publicly.

### Test 2: Checking the Default Gateway

Command used:

```bash
ip route
```

What I observed:

The output showed a default route through the active network interface. This tells me which gateway Kali uses to reach outside networks and the internet.

### Test 3: Checking the DNS Resolver

Command used:

```bash
cat /etc/resolv.conf
```

What I observed:

The output showed the DNS resolver being used by the system. I am not publishing the exact resolver address publicly.

### Test 4: Pinging an IP Address

Command used:

```bash
ping -c 4 1.1.1.1
```

Result:

The ping was successful with `4 packets transmitted, 4 received, 0% packet loss`.

What this means:

This proved that my Kali VM had working internet connectivity using a direct IP address.

### Test 5: Pinging a Domain Name

Command used:

```bash
ping -c 4 google.com
```

Result:

The ping was successful with `4 packets transmitted, 4 received, 0% packet loss`.

What this means:

This proved that DNS resolution and internet connectivity were both working. Kali first resolved `google.com` into an IP address and then successfully reached it.

### Test 6: DNS Lookup

Command used:

```bash
nslookup google.com
```

Result:

The command returned multiple IP addresses for `google.com`.

What this means:

A single domain name can resolve to multiple IP addresses. This is common for large services like Google because they use multiple servers and IPs.

## What I Learned

* My Kali VM connects to the network through an active interface called `eth0`.
* The loopback interface `lo` is used by the machine to communicate with itself.
* A private IP address is used inside a local or virtual network.
* The default gateway is used when Kali needs to reach outside networks.
* DNS resolves domain names like `google.com` into IP addresses.
* Pinging `1.1.1.1` tests direct IP connectivity.
* Pinging `google.com` tests both DNS resolution and internet connectivity.
* `nslookup` shows which DNS server answered and which IP addresses were returned for a domain.

## Why This Matters in Cybersecurity

Networking fundamentals are important in cybersecurity because SOC analysts, NOC analysts, network support engineers, and penetration testers need to understand how systems communicate.

When investigating alerts, suspicious traffic, malware activity, phishing links, or network issues, it is important to understand IP addresses, DNS, routing, gateways, and connectivity tests.

## Next Topics

* MAC addresses
* ARP
* TCP vs UDP
* Common ports
* Wireshark packet capture
* Subnetting
