# Nmap Lesson 04 — Service Detection

## Objective

Learn how Nmap identifies open ports and detects the services running on those ports.

## Lab Target

Target: 127.0.0.1

This is my local Kali Linux machine.

All scanning in this lesson was performed against my own authorized lab environment.

## 1. Scan Port 8000

Command:

nmap -p 8000 127.0.0.1

### Purpose

The -p 8000 option tells Nmap to scan only TCP port 8000.

### Result

Port 8000 was found open.

Example:

8000/tcp open

## 2. Service and Version Detection

Command:

nmap -sV -p 8000 127.0.0.1

### Purpose

The -sV option attempts to identify the service and software version running on the port.

### Result

Nmap identified the HTTP service running on port 8000.

Example:

8000/tcp open http SimpleHTTPServer 0.6 (Python 3.14.7)

## 3. Full Port Scan

Command:

nmap -p- 127.0.0.1

### Purpose

The -p- option scans all TCP ports from 1 to 65535.

### Result

Port 8000 was found open.

The other TCP ports were closed in this lab at the time of testing.

## Key Learning

Open port:

An open port means a service is listening on that port.

Service detection:

Nmap can identify the service associated with an open port.

Version detection:

The -sV option attempts to identify the software and version.

## Important Commands

Scan a specific port:

nmap -p 8000 127.0.0.1

Service/version detection:

nmap -sV -p 8000 127.0.0.1

Scan all TCP ports:

nmap -p- 127.0.0.1

## Security Perspective

A basic reconnaissance workflow is:

Port Discovery
→ Open Port
→ Service Identification
→ Version Detection
→ Enumeration
→ Vulnerability Assessment

This lesson demonstrates the first stages in an authorized local lab.

## Lesson Summary

I learned:

- How to scan a specific port.
- How to identify an open port.
- How to use -sV for service/version detection.
- How to scan all TCP ports with -p-.
- Why service and version information is useful during reconnaissance.

## Lab Environment

OS: Kali Linux

Target: 127.0.0.1

Tool: Nmap

Purpose: Authorized cybersecurity learning lab

## Next Lesson

Lesson 05 will continue with Nmap reconnaissance and NSE/default script scanning.
