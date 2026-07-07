# Day 18 — Network Operations, Monitoring, Documentation and Troubleshooting

## Status

Completed

---

## Topics Revised

Today I revised these Network+ topics:

- Installing Networks
- Power
- Environmental Factors
- Network Documentation
- Life Cycle Management
- Configuration Management
- SNMP
- Logs and Monitoring
- Network Solutions

---

## Installing Networks

Before installing a network, proper planning is required.

Basic steps:

- Understand business requirements
- Perform site survey
- Create physical and logical diagrams
- Plan cabling
- Plan rack space
- Plan power requirements
- Plan cooling and ventilation
- Prepare IP addressing plan
- Prepare VLAN plan
- Install devices and cables
- Label everything
- Test connectivity
- Document final setup

---

## Site Survey

A site survey helps understand physical and technical requirements before installation.

It may include:

- Building layout
- Cable distance
- Cable path
- Rack location
- Power availability
- UPS availability
- Cooling
- Wireless coverage
- Wireless interference
- Device placement
- Physical security

A site survey reduces mistakes during installation.

---

## Labeling

Labeling is important for cables, patch panels, switch ports, rack devices, wall ports, and power connections.

Labeling helps with:

- Troubleshooting
- Maintenance
- Cable tracing
- Faster fault isolation
- Better documentation

Interview line:

Labeling helps identify ports, cables, patch panels, and devices during troubleshooting and maintenance.

---

## Testing After Installation

After installation, devices and links should be tested.

Testing may include:

- Cable testing
- Link status check
- IP connectivity
- Gateway ping
- DNS test
- DHCP test
- VLAN test
- Internet access test
- Performance check
- Documentation verification

---

## Power

Network devices need stable power.

Unstable power can cause:

- Device shutdown
- Network downtime
- Hardware damage
- Configuration corruption
- Service disruption

Examples of devices needing stable power:

- Switches
- Routers
- Firewalls
- Wireless access points
- Servers
- Modems
- Network storage

---

## UPS

UPS stands for Uninterruptible Power Supply.

A UPS provides short-term backup power when main power fails.

It helps keep devices running until:

- Power returns
- Generator starts
- Devices are safely shut down

Memory line:

UPS = immediate short-term backup power.

---

## UPS vs Generator

| Power Source | Purpose |
|---|---|
| UPS | Immediate short-term backup |
| Generator | Longer-term backup power |

A UPS provides instant backup for short duration.

A generator provides longer backup but may take time to start.

---

## Power Redundancy

Power redundancy helps maintain uptime.

Examples:

- Dual power supplies
- UPS
- Generator
- Separate power circuits
- Redundant PDUs

If a switch or router loses power, users connected through that device may lose network access.

---

## Environmental Factors

Environmental factors can affect network equipment.

Important factors:

- Temperature
- Humidity
- Dust
- Airflow
- Water leakage
- Fire risk
- Electrical interference
- Physical access
- Vibration

---

## Temperature

High temperature can cause:

- Poor performance
- Overheating
- Device shutdown
- Hardware damage
- Fire risk in extreme cases

---

## Humidity

Low humidity can increase static electricity risk.

High humidity can cause condensation, corrosion, and moisture damage.

---

## Ventilation and Cooling

Proper ventilation and cooling help prevent overheating, hardware failure, performance degradation, and unexpected shutdowns.

---

## Dust Protection

Dust can block ventilation, reduce airflow, increase device temperature, and damage internal components.

---

## Network Documentation

Network documentation records how a network is designed, connected, configured, addressed, monitored, and maintained.

Good documentation helps with:

- Troubleshooting
- Auditing
- Change management
- Onboarding
- Disaster recovery
- Maintenance
- Security review

---

## Things To Document

Important things to document:

- IP address inventory
- VLAN information
- Device hostnames
- Device models
- Serial numbers
- Rack diagrams
- Cable labels
- Patch panel ports
- Switch port mappings
- Firewall rules
- Routing information
- Wireless SSIDs
- Configuration backups
- Vendor contacts
- Warranty details
- EOL/EOS dates

---

## Network Diagram

A network diagram shows how devices and networks are connected.

It may include routers, switches, firewalls, servers, internet links, VLANs, subnets, wireless access points, and WAN links.

---

## Physical Diagram vs Logical Diagram

| Diagram Type | Shows |
|---|---|
| Physical Diagram | Physical location, racks, cables, ports |
| Logical Diagram | IPs, VLANs, routing, network flow |

---

## Rack Diagram

A rack diagram shows the physical placement of equipment inside a rack.

It may show rack units, patch panels, switches, routers, firewalls, servers, UPS, and cable managers.

---

## IP Address Inventory

An IP address inventory is a record of assigned and available IP addresses.

It may include:

- IP address
- Hostname
- Device owner
- MAC address
- VLAN
- Subnet
- Static or DHCP status
- Location

---

## Life Cycle Management

Life cycle management tracks network devices from purchase to retirement.

Stages may include:

- Purchase
- Deployment
- Maintenance
- Updates
- Warranty tracking
- End of Life
- End of Support
- Replacement
- Disposal

---

## EOL and EOS

EOL means End of Life.

EOS may mean End of Support or End of Sale depending on vendor context.

For Network+ understanding:

- End of Support means support, updates, patches, or fixes are no longer provided.
- End of Sale means the vendor no longer sells the product.

Old devices should be replaced because they may have vulnerabilities, unsupported firmware, poor performance, hardware failure risk, compatibility issues, and no vendor support.

---

## Firmware and Software Update Tracking

Firmware and software update tracking is important because updates may:

- Fix bugs
- Patch vulnerabilities
- Improve stability
- Improve performance
- Maintain vendor support

---

## Configuration Management

Configuration management is the process of tracking, controlling, backing up, and documenting device configurations and changes.

It applies to switches, routers, firewalls, wireless controllers, and servers.

---

## Configuration Backups

Device configurations should be backed up.

Backups help restore service after:

- Device failure
- Accidental change
- Misconfiguration
- Replacement
- Factory reset

Interview line:

Configuration backups help restore a device quickly after failure, misconfiguration, or accidental change.

---

## Baseline Configuration

A baseline configuration is an approved standard configuration used as a reference.

Examples:

- Hostname format
- Management IP
- SNMP settings
- NTP settings
- Logging settings
- Security settings
- VLAN settings
- Access control

---

## Change Management

Change management ensures network changes are reviewed, approved, documented, tested, scheduled, and reversible.

Undocumented changes can cause outages, security gaps, and troubleshooting difficulty.

---

## SNMP

SNMP stands for Simple Network Management Protocol.

SNMP is used to monitor and manage network devices such as switches, routers, firewalls, servers, printers, UPS devices, and wireless controllers.

---

## SNMP Agent

An SNMP agent runs on the managed device.

The agent collects local device information and responds to the SNMP manager.

Example:

A switch has an SNMP agent that reports interface status, bandwidth usage, CPU usage, memory usage, uptime, and errors.

---

## SNMP Manager

An SNMP manager is the central monitoring system.

It queries SNMP agents and receives alerts.

Examples:

- PRTG
- Zabbix
- SolarWinds
- Nagios
- LibreNMS

---

## SNMP Trap

An SNMP trap is an automatic alert sent by an SNMP agent to the SNMP manager when an event occurs.

Examples:

- Interface down
- High CPU
- Device reboot
- Power supply failure
- Temperature alert

---

## SNMP Metrics

SNMP can collect:

- Interface status
- Bandwidth usage
- Packet errors
- CPU usage
- Memory usage
- Device uptime
- Temperature
- Power supply status
- Fan status
- Port status
- Device name
- Device location

---

## Logs

Logs are records of events generated by systems, devices, applications, and security tools.

Examples:

- Login attempts
- Interface up/down
- Service errors
- Firewall allow/deny events
- System reboot
- Configuration changes
- Authentication failures

---

## Logs for Troubleshooting

Logs help identify what happened, when it happened, where it happened, which error was recorded, and which user or device was involved.

---

## Logs for SOC and Security

Logs are important for SOC because they provide evidence of authentication attempts, suspicious activity, malware behavior, privilege use, network traffic, attack timelines, failed logins, and configuration changes.

---

## Monitoring

Monitoring is the continuous observation of network devices, services, performance, availability, and security events.

Monitoring helps detect issues early before they become outages.

---

## What To Monitor

Important things to monitor:

- Device uptime
- Interface status
- Bandwidth usage
- CPU usage
- Memory usage
- Disk usage
- Errors and drops
- Latency
- Packet loss
- Logs
- Temperature
- Power status
- Services
- Security alerts

---

## Network Troubleshooting Examples

### Internet Is Slow

Check:

- One user or many users?
- Wi-Fi or wired?
- Ping gateway
- Ping internet IP
- Check DNS
- Check bandwidth usage
- Check interface errors
- Check switch/AP status
- Check firewall/router load
- Check ISP status
- Check recent changes

### Switch Port Is Down

Check:

- Cable connected
- Device powered on
- Correct switch port
- Port administratively disabled?
- Speed/duplex issue
- Bad cable
- Bad NIC
- VLAN assignment
- Switch logs
- Link lights
- Patch panel connection

### Server Is Unreachable

Check:

- Ping server IP
- DNS name resolution
- Server power/status
- Gateway/routing
- Firewall rules
- Switch port
- VLAN
- Service status
- Recent changes
- Logs

### Users Cannot Get IP Address

Possible issues:

- DHCP server failure
- DHCP scope exhausted
- DHCP relay/helper issue
- Wrong VLAN
- Network connectivity to DHCP server

### Users Can Ping IP But Not Website Name

Possible issues:

- DNS server failure
- DNS misconfiguration
- DNS reachability issue

### Device Has Power But No Network

Possible causes:

- Bad cable
- Wrong port
- Port disabled
- Incorrect VLAN
- NIC issue
- No IP address
- DHCP failure
- Firewall block
- Bad switch port
- Incorrect gateway

---

## Reactive Troubleshooting vs Proactive Monitoring

Reactive troubleshooting happens after a problem is reported.

Proactive monitoring detects warning signs before the problem becomes serious.

Monitoring is better because it helps detect issues early before many users are affected.

---

## Kali Practical

Practical folder:

```text
~/cyber_project/kali_practise/network-ops-monitoring
```

Commands used:

```bash
pwd
date
hostname
uptime
ip -br a
ip route
ip neigh
nmcli dev status
ping -c 4 10.0.2.2
ping -c 4 1.1.1.1
ss -tuln
df -h
free -h
journalctl -n 20 --no-pager
dmesg | tail -n 20
```

---

## Practical Findings

Hostname:

```text
kali-vm1
```

Interface:

```text
eth0 UP
```

IP address:

```text
10.0.2.15/24
```

Default gateway:

```text
10.0.2.2
```

Network:

```text
10.0.2.0/24
```

Gateway ping:

```text
4 packets transmitted
4 received
0% packet loss
```

Internet IP ping:

```text
1.1.1.1
4 packets transmitted
4 received
0% packet loss
```

Listening services:

```text
No visible listening TCP/UDP services from ss -tuln
```

Disk usage:

```text
/dev/sda1
38G total
17G used
19G available
47% used
Mounted on /
```

Memory:

```text
1.9Gi total
799Mi used
1.1Gi available
2.1Gi swap
```

Logs:

```text
journalctl showed cron/session activity
```

Kernel messages:

```text
dmesg showed VirtualBox guest/service messages
```

---

## Command Meaning

| Command | Purpose |
|---|---|
| uptime | Shows system uptime and load average |
| ip -br a | Shows interfaces, status, and IP addresses |
| ip route | Shows routing table and default gateway |
| ip neigh | Shows ARP/neighbor table |
| nmcli dev status | Shows NetworkManager device status |
| ping | Tests reachability and packet loss |
| ss -tuln | Shows listening TCP/UDP ports |
| df -h | Shows disk usage |
| free -h | Shows memory and swap usage |
| journalctl | Shows systemd logs |
| dmesg | Shows kernel messages |

---

## Weak Areas Found Today

I need to revise:

- SNMP agent
- SNMP manager
- SNMP trap
- SNMP monitored metrics
- Network documentation examples
- Physical vs logical diagram
- IP address inventory
- Switch port down troubleshooting
- Server unreachable troubleshooting
- Device has power but no network troubleshooting
- Monitoring metrics
- EOL vs EOS

---

## Interview Lines

SNMP is used to monitor and manage network devices.

An SNMP agent runs on the managed device and reports local device information.

An SNMP manager is the central monitoring system that queries agents and receives alerts.

An SNMP trap is an automatic alert sent from a device to the monitoring system.

Logs are records of events generated by systems, devices, applications, and security tools.

Monitoring is the continuous observation of network devices, services, performance, availability, and security events.

A baseline configuration is an approved standard configuration used as a reference.

Change management ensures network changes are reviewed, approved, documented, tested, and reversible.

A physical network diagram shows physical placement and cabling.

A logical network diagram shows IPs, VLANs, routing, and network structure.

EOL means End of Life.

EOS may mean End of Support or End of Sale depending on vendor context.

Reactive troubleshooting happens after a problem is reported.

Proactive monitoring detects warning signs before the problem becomes serious.
