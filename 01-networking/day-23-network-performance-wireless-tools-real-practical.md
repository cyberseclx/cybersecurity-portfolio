# Day 23 - Network+ Performance, Wireless, Tools, and Commands Real Practical

## Block

**Clockify:** `D23-B03 | Network+ Practical | Real Performance Wireless Tools Commands`  
**Project:** `CS Sprint | Practical Labs`

## Reason For Practical Change

Earlier practicals were becoming too repetitive with simulated logs and `grep` only.

This practical used real Kali networking tools instead:

- `ip`
- `ip route`
- `cat /etc/resolv.conf`
- `ss`
- `ping`
- `dig`
- `tracepath` / `traceroute`
- `ethtool`
- `nmap`
- `nmcli`
- `iw`
- `curl` timing output

## Important Note

The commands were run from:

```bash
/home/kali
```

For better evidence organization, future practicals should first create and enter a lab folder, for example:

```bash
mkdir -p ~/cyber_project/kali_practise/networking/network-real-tools-day23
cd ~/cyber_project/kali_practise/networking/network-real-tools-day23
```

## 1. Interface Check

Command:

```bash
ip -br a
```

Output summary:

```text
lo      UNKNOWN  127.0.0.1/8 ::1/128
eth0    UP       10.0.2.15/24 ... fe80::a00:27ff:fe08:b07e/64
```

Interpretation:

```text
eth0 is active.
Kali has IPv4 address 10.0.2.15/24.
Kali also has IPv6 addresses.
```

## 2. Routing Check

Command:

```bash
ip route
```

Output:

```text
default via 10.0.2.2 dev eth0 proto dhcp src 10.0.2.15 metric 100
10.0.2.0/24 dev eth0 proto kernel scope link src 10.0.2.15 metric 100
```

Interpretation:

```text
Default gateway is 10.0.2.2.
Local subnet is 10.0.2.0/24.
```

Memory:

```text
ip route = check default gateway and routing table.
```

## 3. DNS Resolver Check

Command:

```bash
cat /etc/resolv.conf
```

Output:

```text
nameserver 192.168.1.1
nameserver fd17:625c:f037:2::3
```

Interpretation:

```text
Kali is using 192.168.1.1 and fd17:625c:f037:2::3 as DNS resolvers.
```

Memory:

```text
/etc/resolv.conf = DNS server configuration on Linux.
```

## 4. Listening Services Check

Command:

```bash
ss -tuln
```

Output showed no listening services.

Interpretation:

```text
No TCP/UDP services were shown listening locally.
This means there are no obvious exposed local services in this output.
```

Memory:

```text
ss -tuln = show listening TCP/UDP ports.
```

## 5. Latency and Packet Loss Check

### Ping to 8.8.8.8

Command:

```bash
ping -c 5 8.8.8.8
```

Result:

```text
5 packets transmitted, 5 received, 0% packet loss
rtt min/avg/max/mdev = 31.792/32.485/32.869/0.396 ms
```

Interpretation:

```text
Connectivity to 8.8.8.8 is working.
Packet loss is 0%.
Average latency is about 32.5 ms.
Jitter/variation is low because mdev is 0.396 ms.
```

### Ping to google.com

Command:

```bash
ping -c 5 google.com
```

Result:

```text
5 packets transmitted, 5 received, 0% packet loss
rtt min/avg/max/mdev = 32.985/33.473/33.848/0.283 ms
```

Interpretation:

```text
DNS resolution and connectivity to google.com are working.
Packet loss is 0%.
Average latency is about 33.5 ms.
Variation is low.
```

Memory:

```text
ping checks connectivity, latency, and packet loss.
mdev shows variation in response time, which helps think about jitter.
```

## 6. DNS Query Check With dig

Command:

```bash
dig google.com
```

Important output:

```text
status: NOERROR
google.com A records returned
Query time: 4 msec
SERVER: 192.168.1.1#53
```

Interpretation:

```text
DNS is working.
google.com resolved successfully.
DNS server used was 192.168.1.1.
Query time was 4 ms.
```

Memory:

```text
dig = detailed DNS query tool.
NOERROR = DNS query succeeded.
A record = domain to IPv4 address.
```

## 7. Path Testing

Command attempted:

```bash
tracepath google.com
```

Output:

```text
Command 'tracepath' not found
```

Interpretation:

```text
tracepath is not installed on this Kali VM.
```

Next alternatives:

```bash
traceroute google.com
```

Or install tracepath later:

```bash
sudo apt install iputils-tracepath
```

Memory:

```text
traceroute / tracepath = check path and hops to destination.
```

## 8. Interface Speed / Duplex Check

Command:

```bash
ethtool eth0
```

Important output:

```text
Speed: 1000Mb/s
Duplex: Full
Auto-negotiation: on
Port: Twisted Pair
Link detected: yes
```

Interpretation:

```text
eth0 link is up.
Speed is 1 Gbps.
Duplex is full.
Auto-negotiation is enabled.
Cable type is twisted pair.
```

The output also showed:

```text
netlink error: Operation not permitted
```

Meaning:

```text
Some ethtool details require root/sudo permission.
The main link/speed/duplex information was still visible.
```

Memory:

```text
ethtool = useful for interface speed, duplex, negotiation, and link state.
```

## 9. Local Port Scan With Nmap

Command:

```bash
nmap -sV localhost
```

Output summary:

```text
Host is up.
All 1000 scanned ports on localhost are closed/reset.
```

Interpretation:

```text
localhost is reachable.
No common TCP services are open on localhost.
No service versions were detected because no ports were open.
```

Memory:

```text
nmap -sV = service/version scan.
If no ports are open, no services will be identified.
```

## 10. Network Manager Device Status

Command:

```bash
nmcli dev status
```

Output:

```text
eth0    ethernet  connected               Wired connection 1
lo      loopback  connected (externally)  lo
```

Interpretation:

```text
Kali is connected through wired ethernet eth0.
No wireless device is visible in nmcli output.
```

## 11. Wireless Device Check

Command:

```bash
iw dev
```

No wireless interface output was shown.

Interpretation:

```text
The VM likely does not have a wireless adapter passed through to Kali.
This is normal in many virtual machines.
Wireless tools need a real USB Wi-Fi adapter or passed-through wireless interface.
```

Memory:

```text
iw dev = shows wireless interfaces.
No output usually means no wireless interface detected.
```

## 12. HTTP Timing With curl

Command:

```bash
curl -o /dev/null -s -w "DNS:%{time_namelookup} Connect:%{time_connect} StartTransfer:%{time_starttransfer} Total:%{time_total}\n" https://google.com
```

Output:

```text
DNS:0.011419 Connect:0.027677 StartTransfer:0.172913 Total:0.173560
```

Interpretation:

```text
DNS lookup took about 11 ms.
TCP connection took about 28 ms.
First response/start transfer took about 173 ms.
Total request took about 174 ms.
```

Memory:

```text
curl timing helps separate DNS delay, connection delay, server response delay, and total request time.
```

## 13. Practical Tool Mapping

```text
ping = connectivity, latency, packet loss
ip -br a = interface/IP summary
ip route = gateway/routing table
/etc/resolv.conf = DNS servers
ss -tuln = listening services
-dig = DNS troubleshooting
traceroute/tracepath = path/hop troubleshooting
ethtool = speed, duplex, link state
nmap = open ports and service detection
nmcli = network device status
iw dev = wireless interface detection
curl timing = HTTP performance timing
```

Correction:

```text
dig = DNS troubleshooting
```

## 14. Key Findings

```text
Kali IP: 10.0.2.15/24
Default gateway: 10.0.2.2
DNS servers: 192.168.1.1 and fd17:625c:f037:2::3
Ping to 8.8.8.8: 0% loss, avg 32.5 ms
Ping to google.com: 0% loss, avg 33.5 ms
DNS query: successful, 4 ms query time
Interface: 1000Mb/s, full duplex, link detected
Localhost nmap: no open common TCP ports
Wireless: no Wi-Fi interface detected in VM
HTTP timing: total about 174 ms
```

## 15. What This Practical Proved

```text
Real command-line tools are better for this block than repeated simulated grep logs.
This practical connected Messer's tools section to real Kali commands.
```

## 16. Next Commands To Practice Later

```bash
sudo tcpdump -i eth0 -nn icmp
traceroute google.com
nmap -sV <target-ip>
nmap -O <target-ip>
nmap --script default <target-ip>
speedtest-cli
```
