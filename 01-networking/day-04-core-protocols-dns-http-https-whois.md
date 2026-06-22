# Day 04 - Core Protocols: DNS, HTTP, HTTPS, WHOIS, and Ports

## Objective

The goal of this lab was to connect common Network+ ports and protocols to real Kali Linux commands.

Topics covered:

* DNS
* UDP/TCP 53
* HTTP
* HTTPS
* TCP ports 80 and 443
* Manual HTTP request
* TLS certificate handshake
* WHOIS lookup
* Local listening ports
* DHCP port reminder

---

## 1. DNS Lookup with nslookup

Command used:

```bash
nslookup example.com
```

Observation:

The DNS resolver returned IPv4 and IPv6 addresses for `example.com`.

Learning:

DNS resolves domain names into IP addresses.

Important port:

```text
DNS = UDP/TCP 53
```

---

## 2. DNS Lookup with dig

Command used:

```bash
dig example.com
```

Observation:

The response showed DNS A records for `example.com`.

The output also showed that the query used UDP.

Learning:

Normal DNS queries commonly use UDP port 53.

Important points:

* `dig` gives more detailed DNS output than `nslookup`.
* DNS A records map a domain name to IPv4 addresses.
* A single domain can resolve to multiple IP addresses.
* DNS commonly uses UDP 53 for normal lookups.

---

## 3. DNS Query Using TCP

Command used:

```bash
dig +tcp example.com
```

Observation:

The DNS response showed that the DNS server was contacted on port 53 using TCP.

Example:

```text
SERVER: DNS_RESOLVER#53 (TCP)
```

Learning:

This proved that DNS can use TCP port 53 as well.

Important points:

* DNS commonly uses UDP 53 for normal lookups.
* DNS can also use TCP 53 for larger responses, reliability, and zone transfers.
* This corrected the idea that DNS is only UDP.

---

## 4. DNS Resolver Check

Command used:

```bash
cat /etc/resolv.conf
```

Observation:

Kali had DNS resolvers configured.

Learning:

A DNS resolver is the server my machine asks when it needs to resolve a domain name into an IP address.

Note:

I should not publish my exact local DNS resolver IP in public notes.

---

## 5. HTTP Headers with curl

Command used:

```bash
curl -I http://example.com
```

Observation:

The server returned HTTP response headers including:

```text
HTTP/1.1 200 OK
Content-Type: text/html
Server: cloudflare
```

Learning:

`curl -I` shows response headers only.

Important points:

* HTTP commonly uses TCP port 80.
* `200 OK` means the request was successful.
* `Content-Type: text/html` means the response is an HTML page.
* HTTP traffic is not encrypted.

---

## 6. HTTPS Headers with curl

Command used:

```bash
curl -I https://example.com
```

Observation:

The server returned:

```text
HTTP/2 200
content-type: text/html
server: cloudflare
```

Learning:

HTTPS commonly uses TCP port 443.

HTTPS is HTTP protected by TLS encryption.

Important points:

* HTTPS = HTTP over TLS.
* HTTPS protects data in transit.
* Port 443 is the common HTTPS port.

---

## 7. Testing Open TCP Ports with netcat

Commands used:

```bash
nc -vz example.com 80
nc -vz example.com 443
nc -vz example.com 22
```

Observation:

* TCP port 80 was open.
* TCP port 443 was open.
* TCP port 22 did not respond normally and was stopped manually.

Learning:

A known port number does not mean that port is always open.

A port is open only when a service is running and listening on that port.

Examples:

```text
TCP 80 = HTTP
TCP 443 = HTTPS
TCP 22 = SSH
```

Important lesson:

```text
Known port does not mean open port.
A service must actually be running and listening.
```

---

## 8. Manual HTTP Request with Telnet

Command used:

```bash
telnet example.com 80
```

Manual HTTP request sent:

```http
GET / HTTP/1.1
Host: example.com

```

Observation:

The server returned:

* HTTP response headers
* HTML page body
* Example Domain page content

Learning:

Telnet connected to TCP port 80.

This proved that HTTP requests can be sent manually as plain text.

Important format:

```http
GET / HTTP/1.1
Host: example.com

```

Meaning:

* `GET` = HTTP method
* `/` = homepage/path
* `HTTP/1.1` = protocol version
* `Host: example.com` = website/domain requested
* Blank line = request is complete

Important correction:

```text
GET / HTTP/1.1 = correct
GET /HTTP/1.1 = wrong because it is missing a space
```

---

## 9. HTTPS TLS Handshake with OpenSSL

Command used:

```bash
openssl s_client -connect example.com:443 -servername example.com
```

Observation:

The output showed:

```text
CONNECTED
Certificate chain
Verification: OK
Protocol: TLSv1.3
```

Learning:

HTTPS uses TLS.

TLS uses certificates to help secure communication between client and server.

Important points:

* HTTP traffic is plain text.
* HTTPS traffic is encrypted using TLS.
* TLS certificates help prove the server identity.
* A valid certificate chain helps the client trust the website.

---

## 10. WHOIS Lookup

Command used:

```bash
whois example.com
```

Observation:

WHOIS returned domain registration information such as:

* Domain name
* Registrar information
* Creation date
* Expiry date
* Name servers
* Domain status

Learning:

WHOIS is used to look up domain registration information.

Common port:

```text
WHOIS = TCP 43
```

Security/SOC relevance:

WHOIS can help during investigation to understand domain registration details, name servers, domain age, and ownership/registrar information.

---

## 11. Local Listening Services

Command used:

```bash
ss -tuln
```

Observation:

No major listening services were shown.

Learning:

`ss -tuln` shows local listening TCP and UDP services.

Flags:

```text
-t = TCP
-u = UDP
-l = listening
-n = show numbers instead of names
```

If no services are listening, the machine is not exposing those ports locally.

---

## 12. Active Connections and DHCP Reminder

Command used:

```bash
ss -tun
```

Observation:

The output showed DHCP-related UDP traffic:

```text
UDP client port 68 communicating with server port 67
```

Learning:

```text
DHCP server = UDP 67
DHCP client = UDP 68
```

This connected today’s port memorization with the earlier DHCP practical.

---

## Core Protocol Memory

```text
DNS    = UDP/TCP 53
WHOIS  = TCP 43
HTTP   = TCP 80
HTTPS  = TCP 443
FTP    = TCP 20/21
SSH    = TCP 22
Telnet = TCP 23
SMTP   = TCP 25
POP3   = TCP 110
IMAP   = TCP 143
DHCP   = UDP 67/68
```

---

## TCP vs UDP Reminder

A port number alone is incomplete.

Correct format:

```text
Protocol + TCP/UDP + Port
```

Examples:

```text
TCP 80 = HTTP
TCP 443 = HTTPS
UDP 53 = common DNS query
TCP 53 = DNS over TCP
UDP 67/68 = DHCP
```

Important:

Some protocols do not use TCP or UDP ports.

Examples:

```text
ICMP = no TCP/UDP port
GRE = no TCP/UDP port
ESP/AH = IPsec protocols, not normal TCP/UDP ports
```

Ping uses ICMP. Ping does not use a port.

---

## Final Summary

In this lab, I practiced:

* DNS lookup using `nslookup`
* DNS lookup using `dig`
* DNS over TCP using `dig +tcp`
* HTTP header checking using `curl -I`
* HTTPS header checking using `curl -I`
* Open TCP port testing using `nc`
* Manual HTTP request using `telnet`
* TLS certificate inspection using `openssl s_client`
* WHOIS domain lookup using `whois`
* Local listening port checks using `ss`

Key lessons:

* DNS resolves domain names to IP addresses.
* DNS commonly uses UDP 53 but can also use TCP 53.
* HTTP uses TCP 80 and is plain text.
* HTTPS uses TCP 443 and is protected by TLS.
* A known port is not always open.
* A service must be running and listening for a port to be open.
* WHOIS gives domain registration information.
* `ss -tuln` shows local listening ports.
* DHCP uses UDP 67 for the server and UDP 68 for the client.
