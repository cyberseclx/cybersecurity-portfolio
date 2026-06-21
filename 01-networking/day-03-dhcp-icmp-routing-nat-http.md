# Day 03 - DHCP, ICMP, Routing, NAT, and HTTP Basics

## Objective

The goal of this lab was to understand how a Linux/Kali machine receives network settings, reaches the gateway, resolves domains, tests connectivity, traces routes, and communicates with a web server using HTTP.

Topics covered:

* DHCP
* ICMP and ping
* Routing table
* Default gateway
* NAT
* DNS lookup
* Traceroute
* HTTP and HTTPS headers
* Manual HTTP request using Telnet

---

## 1. Network Interface and IP Check

Command used:

```bash
ip -br a
```

Observation:

* `lo` was the loopback interface.
* `eth0` was the active network interface of the Kali VM.
* Kali had a private IPv4 address in the `10.x.x.x/24` range.
* IPv6 addresses were also present.

Learning:

`eth0` is the virtual network interface created for the Kali VM. The private IP shows that Kali is inside a local/virtual network.

---

## 2. Routing Table

Command used:

```bash
ip route
```

Observation:

```text
default via 10.x.x.x dev eth0 proto dhcp
```

Learning:

The routing table shows how traffic leaves the machine.

Important points:

* The default route is used when traffic is going outside the local network.
* The default gateway is reached through `eth0`.
* `proto dhcp` means the route was learned through DHCP.

Correction learned:

`ip route` shows the local routing table of my machine. It does not show all internet hops. Traceroute is used to try to show the path/hops to a destination.

---

## 3. DNS Resolver

Command used:

```bash
cat /etc/resolv.conf
```

Observation:

Kali had DNS resolvers configured, including IPv4 and IPv6 resolvers.

Learning:

DNS resolvers are used to convert domain names like `google.com` into IP addresses.

---

## 4. DHCP Connection Check

Command used:

```bash
ss -tun
```

Observation:

```text
UDP local port 68 communicating with remote port 67
```

Learning:

* UDP port 68 = DHCP client
* UDP port 67 = DHCP server

This showed DHCP-related communication between Kali and the gateway/DHCP server.

DHCP stands for Dynamic Host Configuration Protocol. It can automatically provide:

* IP address
* Subnet mask
* Default gateway
* DNS server
* Lease time

Memory:

DHCP = automatic network settings provider.

---

## 5. Ping Gateway

Commands used:

```bash
GATEWAY=$(ip route | awk '/default/ {print $3}')
echo $GATEWAY
ping -c 4 $GATEWAY
```

Observation:

The gateway responded successfully with 0% packet loss.

Learning:

This proved that Kali could reach its local gateway.

---

## 6. Ping Public IP

Command used:

```bash
ping -c 4 1.1.1.1
```

Observation:

The public IP responded successfully with 0% packet loss.

Learning:

This proved that Kali had internet connectivity by direct IP address.

Important:

This test does not require DNS because an IP address was used directly.

---

## 7. Ping Domain

Command used:

```bash
ping -c 4 google.com
```

Observation:

`google.com` resolved to an IP address and responded successfully.

Learning:

This proved two things:

1. DNS was working.
2. Internet connectivity was working.

Ping is a tool. ICMP is the protocol used by ping.

ICMP stands for Internet Control Message Protocol and is used for network control and troubleshooting messages.

---

## 8. DNS Lookup

Command used:

```bash
nslookup google.com
```

Observation:

The DNS resolver returned multiple IPv4 and IPv6 addresses for `google.com`.

Learning:

One domain can resolve to multiple IP addresses.

Also, DNS commonly uses port 53.

---

## 9. Traceroute

Command used:

```bash
traceroute 1.1.1.1
```

Observation:

The first hop was the VM gateway. Later hops showed `* * *`.

Learning:

Traceroute tries to show the path or hops between my machine and a destination.

The `* * *` output does not always mean the internet is broken. It can happen when routers or firewalls do not respond to traceroute probes.

Ping already confirmed that the destination was reachable.

---

## 10. HTTP Headers with Curl

Commands used:

```bash
curl -I http://example.com
curl -I https://example.com
```

Observation:

The server returned successful responses such as:

```text
HTTP/1.1 200 OK
HTTP/2 200
Content-Type: text/html
Server: cloudflare
```

Learning:

`curl -I` shows only the response headers, not the full page body.

Important points:

* `200 OK` means the request was successful.
* `Content-Type: text/html` means the response is an HTML page.
* HTTP usually uses port 80.
* HTTPS usually uses port 443.

---

## 11. Manual HTTP Request Using Telnet

Command used:

```bash
telnet example.com 80
```

Manual request sent:

```http
GET / HTTP/1.1
Host: example.com

```

Observation:

After sending the correct request, the server returned:

* HTTP response headers
* HTML content
* Example Domain page body

Learning:

Telnet to port 80 proved that I can manually connect to a web server over TCP and send a plain-text HTTP request.

Important format:

```http
GET / HTTP/1.1
Host: example.com

```

Meaning:

* `GET` = HTTP method
* `/` = homepage/path requested
* `HTTP/1.1` = protocol version
* `Host: example.com` = website/domain being requested
* Blank line = request is complete

Correction learned:

`GET / HTTP/1.1` is correct.

`GET /HTTP/1.1` is wrong because it is missing a space.

---

## 12. NAT Understanding

NAT stands for Network Address Translation.

Learning:

Kali uses a private IP because it is inside a virtual/local network created by the VM software. NAT allows this private IP to access the internet by forwarding/translating the traffic through another address.

My traffic path:

```text
Kali VM private IP
→ eth0
→ VM gateway
→ NAT
→ host/laptop network
→ router/ISP
→ internet
```

Memory:

NAT allows private IP devices to access the internet through another public-facing address.

---

## Final Summary

In this lab, I learned and practiced:

* DHCP automatically provides network settings.
* ICMP is used by ping to test reachability.
* The routing table shows the default gateway and local routes.
* NAT allows a private IP device to access the internet.
* DNS resolves domain names into IP addresses.
* Traceroute tries to show the route/hops to a destination.
* `curl -I` displays HTTP/HTTPS response headers.
* HTTP requests can be manually sent as plain text using Telnet on port 80.

Key corrections:

* `ip route` shows the local routing table, not all internet hops.
* `traceroute` is used to try to show hops.
* Port 80 = HTTP.
* Port 443 = HTTPS.
* HTTP/1.1 needs the Host header because one server can host multiple websites.
