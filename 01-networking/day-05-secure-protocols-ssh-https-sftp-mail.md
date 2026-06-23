# Day 05 - Secure Protocols: SSH, HTTPS, TLS, SFTP, FTPS and Secure Mail

## Goal

Today I studied secure versions of common network protocols and tested them practically in Kali Linux.

The main focus was understanding how insecure protocols are replaced or protected by encrypted versions.

---

## Secure vs Insecure Protocols

| Use Case                      | Insecure Protocol |        Secure Version | Port / Note            |
| ----------------------------- | ----------------: | --------------------: | ---------------------- |
| Web browsing                  |     HTTP - TCP 80 |                 HTTPS | TCP 443                |
| Email sending                 |     SMTP - TCP 25 | SMTPS / SMTP with TLS | TCP 465 / 587          |
| Email receiving               |    POP3 - TCP 110 |                 POP3S | TCP 995                |
| Email sync                    |    IMAP - TCP 143 |                 IMAPS | TCP 993                |
| Remote login                  |   Telnet - TCP 23 |                   SSH | TCP 22                 |
| File transfer                 |   FTP - TCP 20/21 |                  FTPS | TCP 990 / FTP with TLS |
| File transfer                 |   FTP - TCP 20/21 |                  SFTP | TCP 22 via SSH         |
| Remote/private network access |   Public internet |                   VPN | Encrypted tunnel       |

---

## Important Difference: SFTP vs FTPS

SFTP and FTPS are not the same.

* **SFTP** means SSH File Transfer Protocol. It runs over SSH and usually uses TCP port 22.
* **FTPS** means FTP protected with TLS/SSL. It commonly uses TCP port 990 or FTP ports with TLS.

---

## Kali Lab Folder

```bash
mkdir -p ~/portfolio-labs/networking-day5-secure-protocols
cd ~/portfolio-labs/networking-day5-secure-protocols
pwd
```

Lab path:

```text
/home/kali/portfolio-labs/networking-day5-secure-protocols
```

---

## Tool Version Checks

```bash
ssh -V
openssl version
curl -V | head -n 3
```

Output observed:

```text
OpenSSH_10.2p1 Debian-6, OpenSSL 3.6.1 27 Jan 2026
OpenSSL 3.6.1 27 Jan 2026
curl 8.19.0
```

Curl supported many protocols, including:

```text
ftp, ftps, http, https, imap, imaps, pop3, pop3s, scp, sftp, smtp, smtps, telnet
```

This shows that curl can be used to test both insecure and secure protocol support.

---

## HTTP vs HTTPS Test

HTTP test:

```bash
curl -I http://example.com
```

Output observed:

```text
HTTP/1.1 200 OK
Server: cloudflare
Content-Type: text/html
```

HTTPS test:

```bash
curl -I https://example.com
```

Output observed:

```text
HTTP/2 200
server: cloudflare
content-type: text/html
```

### Learning

HTTP normally uses TCP port 80 and sends data without TLS protection.

HTTPS uses TLS protection over TCP port 443. It helps protect communication between the client and the server.

---

## TLS Certificate Test

Command used:

```bash
echo | openssl s_client -connect example.com:443 -servername example.com 2>/dev/null | openssl x509 -noout -subject -issuer -dates
```

Output observed:

```text
subject=CN=example.com
issuer=C=US, O=SSL Corporation, CN=Cloudflare TLS Issuing ECC CA 3
notBefore=May 31 21:39:12 2026 GMT
notAfter=Aug 29 21:41:26 2026 GMT
```

### Learning

The HTTPS server presented a TLS certificate.

The certificate showed:

* Subject: the certificate belongs to `example.com`
* Issuer: the certificate was issued by Cloudflare TLS Issuing ECC CA 3
* Validity dates: the certificate has a start and expiry date

Interview line:

```text
TLS certificates help prove server identity and enable encrypted HTTPS communication.
```

---

## Port Testing with Netcat

HTTPS port test:

```bash
nc -vz example.com 443
```

Output observed:

```text
example.com [172.66.147.243] 443 (https) open
```

### Learning

Port 443 was open, which means the HTTPS service was reachable.

SSH port test:

```bash
nc -vz example.com 22
```

Output observed:

```text
example.com [104.20.23.154] 22 (ssh) : Connection refused
```

### Learning

Port 22 was not accepting SSH connections on this server.

Important difference:

```text
Open = service is accepting connections
Refused = host responded, but service is closed or not accepting connections
Timeout = no response, possibly filtered by firewall or network issue
```

---

## Checking Common Ports in Linux

Command used:

```bash
grep -wE 'http|https|ssh|smtp|pop3|imap|pop3s|imaps|sftp|ftps' /etc/services | head -n 30
```

Important output observed:

```text
ssh             22/tcp
smtp            25/tcp
http            80/tcp
pop3            110/tcp
imap2           143/tcp
https           443/tcp
https           443/udp
ftps-data       989/tcp
ftps            990/tcp
imaps           993/tcp
pop3s           995/tcp
http-alt        8080/tcp
```

### Learning

Linux stores common service and port mappings in:

```text
/etc/services
```

Important note:

```text
HTTPS normally uses TCP 443.
HTTP/3 can use UDP 443.
```

---

## VPN Notes

VPN means Virtual Private Network.

A VPN creates an encrypted tunnel over an untrusted network such as the internet.

Common VPN concepts:

* Client-to-site VPN: one remote user connects to a company network
* Site-to-site VPN: one office network connects securely to another office network
* Full tunnel: all traffic goes through the VPN
* Split tunnel: only selected/company traffic goes through the VPN

VPN helps protect data and privacy while communicating over untrusted networks.

---

## Key Ports Reinforced

| Protocol |    Port |
| -------- | ------: |
| SSH      |  TCP 22 |
| SMTP     |  TCP 25 |
| HTTP     |  TCP 80 |
| POP3     | TCP 110 |
| IMAP     | TCP 143 |
| HTTPS    | TCP 443 |
| FTPS     | TCP 990 |
| IMAPS    | TCP 993 |
| POP3S    | TCP 995 |

---

## Summary

Today I learned that many older protocols have secure versions.

Main takeaways:

* HTTPS is HTTP protected by TLS.
* SSH replaced Telnet because SSH encrypts the session.
* SFTP uses SSH on TCP 22.
* FTPS is FTP protected with TLS.
* POP3S uses TCP 995.
* IMAPS uses TCP 993.
* TLS certificates help prove server identity.
* `nc` can test whether a port is open, refused, or unreachable.
* `/etc/services` is useful for checking common protocol-port mappings.

---

## Weak Topics to Review Later

* Manual SMTP command flow
* Manual POP3 command flow
* Manual IMAP command flow
* FTPS active/passive details
* VPN types and ports in more depth
