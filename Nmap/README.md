# Nmap — Network Enumeration

My practical Nmap notes and authorized lab exercises.

## 🔎 Host Discovery

```bash
nmap -sn <target>
```

Discovers live hosts without performing a port scan.

## 🔐 Port Scanning

```bash
nmap -p 80,443 <target>
nmap -p- <target>
```

* `-p` — scan specific ports
* `-p-` — scan all TCP ports

## 🧰 Service & Version Detection

```bash
nmap -sV <target>
```

Attempts to identify running services and their versions.

## 📜 Default NSE Scripts

```bash
nmap -sC <target>
```

Runs Nmap's default NSE scripts.

## 🎯 OS Detection

```bash
nmap -O <target>
```

Attempts to identify the target operating system.

## ⚡ Common Scans

```bash
nmap -A <target>
nmap -F <target>
nmap -T4 <target>
nmap -Pn <target>
```

* `-A` — enables several advanced detection features
* `-F` — fast scan of commonly used ports
* `-T4` — faster timing template
* `-Pn` — treats hosts as online and skips host discovery

## 💾 Output

```bash
nmap -oN scan.txt <target>
nmap -oX scan.xml <target>
```

* `-oN` — normal human-readable output
* `-oX` — XML output

## 🌐 TCP & UDP Enumeration

```bash
nmap -sT <target>
nmap -sU <target>
```

* `-sT` — TCP connect scan
* `-sU` — UDP scan

## 🛠️ Tools Used

* Nmap
* Kali Linux
* Linux Command Line

> All scanning activities are performed only against authorized labs, CTFs, or systems where I have explicit permission to test.
