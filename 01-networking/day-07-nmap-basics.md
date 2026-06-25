# Day 07 Bonus — Nmap Basics

## Topic

TryHackMe — Nmap: The Basics

## What I Practiced

Today I practiced basic Nmap scanning using my own Kali VM as the target. I scanned localhost, started a test Python web server, detected an open port, performed service version detection, scanned selected ports, saved scan output, and compared Nmap results with `ss`.

## Key Concepts

### Nmap

Nmap is a network scanning tool used to discover hosts, open ports, and running services.

### Open Port

An open port means a service is actively listening and accepting connections.

### Closed Port

A closed port means the host is reachable, but no service is listening on that port.

### Service Detection

The `-sV` option tries to identify the service and version running on an open port.

### Saving Output

The `-oN` option saves Nmap results in normal readable format.

## Commands Practiced

### Create lab folder

```bash
mkdir -p ~/portfolio-labs/day07-nmap
cd ~/portfolio-labs/day07-nmap
```

### Set target as localhost

```bash
export TARGET=127.0.0.1
echo $TARGET
```

### Basic scan

```bash
nmap $TARGET
```

Initial result showed all scanned ports were closed.

### Start test web server

```bash
python3 -m http.server 8000
```

This started a local HTTP server on port `8000`.

### Scan again

```bash
nmap $TARGET
```

Result:

```text
8000/tcp open http-alt
```

### Service version detection

```bash
nmap -sV -p 8000 $TARGET
```

Result:

```text
8000/tcp open http SimpleHTTPServer 0.6 (Python 3.13.12)
```

### Scan selected ports

```bash
nmap -p 22,80,443,8000 $TARGET
```

Result:

* `22/tcp` closed
* `80/tcp` closed
* `443/tcp` closed
* `8000/tcp` open

### Save scan output

```bash
nmap -sV -p 8000 -oN day07-nmap-localhost-scan.txt $TARGET
```

### Read saved output

```bash
cat day07-nmap-localhost-scan.txt
```

### Check listening services from inside the system

```bash
ss -tuln
```

Result showed:

```text
0.0.0.0:8000
```

This means the Python web server was listening on all IPv4 interfaces.

## Key Takeaway

Nmap shows what ports and services are visible from a scanner’s point of view. The `ss` command shows what the system itself is listening on. Together, they help confirm whether a service is actually running and reachable.
