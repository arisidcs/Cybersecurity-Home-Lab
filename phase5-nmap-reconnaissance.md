# Phase 5 — Network Reconnaissance with Nmap

## Objective
Perform network reconnaissance against a target machine to identify 
open ports, running services, software versions, and operating system 
— simulating the initial reconnaissance phase of an attack.

---

## Environment

| Role | OS | IP Address |
|---|---|---|
| Attacker | Kali Linux | 192.168.64.2 |
| Target | Ubuntu 22.04 | 192.168.64.3 |

---

## Scan 1 — Basic Port Scan

```bash
nmap 192.168.64.3
```

### Results
| Port | State | Service |
|---|---|---|
| 22/tcp | open | ssh |
| 80/tcp | open | http |

### Analysis
Two open ports discovered. Port 22 confirms SSH is running (exploited 
in Phase 2). Port 80 confirms Apache web server is active (exploited 
in Phase 4). 998 ports are closed.

---

## Scan 2 — Version & Script Detection

```bash
nmap -sV -sC 192.168.64.3
```

### Results
| Port | Service | Version |
|---|---|---|
| 22/tcp | SSH | OpenSSH 8.9p1 Ubuntu 3ubuntu0.15 |
| 80/tcp | HTTP | Apache httpd 2.4.52 (Ubuntu) |

### Analysis
Exact software versions now visible. An attacker would cross-reference 
these against CVE databases to find known vulnerabilities specific to 
these versions. Version disclosure is a significant security risk in 
production environments.

---

## Scan 3 — OS Detection

```bash
sudo nmap -O 192.168.64.3
```

### Results
- **OS Detected:** Linux kernel 4.x - 5.x
- **MAC Address:** 1A:63:23:39:A4:2C
- **Device Type:** General purpose
- **Network Distance:** 1 hop

### Analysis
Nmap successfully fingerprinted the target OS using TCP/IP stack 
behavior patterns. Combined with version detection, an attacker 
now has a complete picture of the target — OS, services, and 
exact software versions.

---

## SOC Analyst Perspective

If these scans appeared in production network logs, the indicators 
to look for are:

| Indicator | Significance |
|---|---|
| Sequential port probing | Automated scanning tool |
| Multiple scan types from single IP | Active reconnaissance |
| -sV flag behavior (version probes) | Attacker mapping attack surface |
| OS detection packets | Advanced reconnaissance |

A SIEM rule alerting on port scans from external IPs would catch 
this immediately.

---

## Defensive Recommendations
1. **Disable version disclosure** — configure Apache and SSH to hide 
exact version numbers
2. **Implement port knocking** — hide SSH behind a secret sequence
3. **Use a firewall** — restrict which IPs can reach port 22
4. **Monitor for scan patterns** — SIEM alerts on sequential port probes
5. **Close unnecessary ports** — reduce attack surface

---

## Commands Reference
```bash
# Basic scan
nmap 192.168.64.3

# Version and script detection
nmap -sV -sC 192.168.64.3

# OS detection (requires sudo)
sudo nmap -O 192.168.64.3
```# Phase 5 — Network Reconnaissance with Nmap

## Objective
Perform network reconnaissance against a target machine to identify 
open ports, running services, software versions, and operating system 
— simulating the initial reconnaissance phase of an attack.

---

## Environment

| Role | OS | IP Address |
|---|---|---|
| Attacker | Kali Linux | 192.168.64.2 |
| Target | Ubuntu 22.04 | 192.168.64.3 |

---

## Scan 1 — Basic Port Scan

```bash
