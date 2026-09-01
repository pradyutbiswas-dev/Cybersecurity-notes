

# Nmap Service Enumeration

## Overview

Nmap (Network Mapper) is an open-source tool used for network discovery, port scanning, and service identification.

This note focuses on **service enumeration** using Nmap in an authorized local lab environment.

---

## Objective

The objective is to identify:

* Open TCP ports
* Services running on those ports
* Service versions when detectable

---

## Basic Command

```bash
nmap -sV 127.0.0.1
```

### Command Breakdown

| Option      | Meaning                               |
| ----------- | ------------------------------------- |
| `nmap`      | Starts Nmap                           |
| `-sV`       | Enables service and version detection |
| `127.0.0.1` | Scans the local host                  |

---

## Practical Lab

Run:

```bash
nmap -sV 127.0.0.1
```

Example result when no services are listening:

```text
Nmap scan report for localhost (127.0.0.1)
Host is up.

All 1000 scanned ports on localhost are in ignored states.
Not shown: 1000 closed tcp ports
```

This means Nmap scanned its default 1,000 TCP ports and did not find an open service among them.

---

## Understanding the Result

If an open port is discovered, Nmap may report information such as:

```text
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH ...
80/tcp open  http    Apache ...
```

### Important Fields

**PORT**
Shows the port number and protocol.

**STATE**
Shows whether the port is open, closed, or filtered.

**SERVICE**
Shows the service Nmap associates with the port.

**VERSION**
Shows the detected software/version when Nmap can identify it.

---

## Why Service Enumeration Matters

Knowing that a port is open is only the first step.

Service enumeration helps a security analyst understand:

1. What network services are exposed
2. Which software may be running
3. What should be investigated further
4. Whether unnecessary services are exposed

This information can support security assessment and defensive hardening.

---

## Common Mistake

Do not assume that the service name alone proves what software is running.

For example:

```text
80/tcp open http
```

only indicates that Nmap identified an HTTP service. Further investigation may be required to determine the actual server software and configuration.

---

## Useful Variations

Scan specific ports:

```bash
nmap -p 22,80,443 -sV 127.0.0.1
```

Scan all TCP ports:

```bash
nmap -p- -sV 127.0.0.1
```

Save the result as a text report:

```bash
nmap -sV 127.0.0.1 -oN scan-reports/service-scan.txt
```

---

## Key Takeaways

* `-sV` enables Nmap service/version detection.
* Service enumeration provides more information than a basic port scan.
* Open ports should be investigated according to the assessment scope.
* Nmap results should be interpreted carefully rather than blindly trusted.
* Scanning should only be performed against authorized systems.

---

## Lab Scope

All examples in this note use a local host or an explicitly authorized lab environment.

**Never scan systems without permission.**
