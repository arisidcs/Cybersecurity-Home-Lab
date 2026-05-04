# Cybersecurity Home Lab

A hands-on cybersecurity home lab built on Apple M2 Mac Mini using 
UTM virtualization. This lab simulates real-world attack and defense 
scenarios to develop practical SOC analyst skills.

---

## Lab Environment

| Machine | OS | IP | Role |
|---|---|---|---|
| Host | macOS (M2) | — | Hypervisor |
| Attacker | Kali Linux ARM64 | 192.168.64.2 | Offensive |
| Target | Ubuntu 22.04 ARM64 | 192.168.64.3 | Defensive |

---

## Phases Completed

### Phase 2 — SSH Brute Force: Detection & Analysis ✅
- Simulated brute force attack using Hydra
- Analyzed attack evidence in SSH logs via journalctl
- Identified IOCs: single source IP, 48 attempts in 62 seconds, 
  4 parallel connections
- Configured and verified Fail2Ban — attacker IP auto-banned 
  after 5 attempts
- [View Report](phase2-ssh-bruteforce-analysis.md)

### Phase 3 — Network Traffic Analysis ✅
- Captured live attack traffic using tcpdump
- Analyzed PCAP file in Wireshark
- Identified brute force signature at network level
- Correlated network evidence with Fail2Ban logs
- [View Report](phase3-network-traffic-analysis.md)

### Phase 4 — Web Application Attack Simulation ✅
- Deployed DVWA on Ubuntu (Apache, PHP, MariaDB)
- Performed SQL Injection attack — extracted all user records
- Documented vulnerability, impact, and remediation
- [View Report](phase4-web-application-attacks.md)

### Phase 5 — Network Reconnaissance ✅
- Performed basic, version, and OS detection scans using Nmap
- Identified open ports, exact software versions, and OS fingerprint
- Analyzed findings from SOC analyst perspective
- Documented defensive recommendations
- [View Report](phase5-nmap-reconnaissance.md)

---

## Skills Demonstrated
- Log analysis & threat detection
- Intrusion detection & automated response (Fail2Ban)
- Network traffic capture & analysis (tcpdump, Wireshark)
- Web application security (SQL Injection, OWASP Top 10)
- Network reconnaissance (Nmap)
- Linux system administration
- SOC analyst reporting & documentation

---

## Tools Used
Kali Linux, Ubuntu 22.04, UTM, Hydra, Fail2Ban, tcpdump, 
Wireshark, Nmap, DVWA, Apache, MariaDB, journalctl

---

## Certifications
- ISC2 Certified in Cybersecurity (CC)
- TryHackMe: SOC Level 1, SOC Simulation, Threat Hunting Simulator,
  Jr. Penetration Tester, Cyber Security 101, Pre-Security
# Cybersecurity Home Lab

A personal home lab built on Apple Silicon (M2 Mac Mini) using UTM virtualization.
Designed to practice SOC operations, log analysis, network reconnaissance, and web application testing.


## Lab Environment

| Machine | OS | IP Address | Role |
|---|---|---|---|
| Attacker | Kali Linux (ARM64) | 192.168.64.2 | Offensive / Recon |
| Target | Ubuntu ARM64 | 192.168.64.3 | Defensive / Target |

---

## Phase 1 — Environment Setup ✅

- Installed UTM virtualization on Apple Silicon (M2)
- Deployed Kali Linux and Ubuntu on isolated internal network
- Verified connectivity between machines (0% packet loss on ping test)

---

## Phase 2 — SOC & Log Analysis ✅
- [SSH Brute Force Attack: Detection & Analysis](phase2-ssh-bruteforce-analysis.md)
- Fail2Ban configured and verified — attacker IP auto-banned
  
---
## Phase 3 — Network Traffic Analysis ✅
- [Wireshark Analysis of SSH Brute Force](phase3-network-traffic-analysis.md)

## Phase 4 — Web Application Attack Simulation ✅
- [SQL Injection Attack on DVWA](phase4-web-application-attacks.md)

## Phase 5 — Network Reconnaissance ✅
- [Nmap Scanning & Analysis](phase5-nmap-reconnaissance.md)
