# Day 06 - Wireshark Basics

## Goal
Learn basic Wireshark operations and practice packet capture and packet analysis.

## Concepts Practiced
- Open PCAP files
- Packet List Pane
- Packet Details Pane
- Packet Bytes Pane
- Packet dissection by layers
- Display filters
- Conversation filters
- Mark and unmark packets
- Add packet comments
- Apply fields as columns
- Go to packet
- Change time format to UTC Date Time
- Export selected packets
- Export Objects
- Save captured PCAP files

## My Live Capture
I captured traffic on the eth0 interface in Kali.

Traffic generated:
- ping 8.8.8.8
- DNS lookup
- HTTP request
- HTTPS request

## Filters Practiced
- icmp
- dns
- http
- tcp.port == 80
- tcp.port == 443
- ip.addr == 8.8.8.8

## Key Learning
Wireshark breaks packets into layers:
Frame → Ethernet → IP → TCP/UDP/ICMP → Application Protocol → Packet Bytes

HTTP traffic can be readable in Wireshark.
HTTPS traffic is encrypted unless TLS decryption keys are available.

## Important Notes
- Display filters filter packets after capture.
- Capture filters decide what packets are captured before capture starts.
- Conversation filter shows the full communication flow related to a selected packet.
- Export Objects only works when Wireshark finds exportable transferred files, usually in unencrypted traffic.

## Interview Line
Wireshark is a packet analysis tool used to inspect captured network traffic, troubleshoot issues, and investigate suspicious communication.
