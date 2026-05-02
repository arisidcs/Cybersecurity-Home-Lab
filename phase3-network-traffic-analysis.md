# Phase 3 — Network Traffic Analysis with Wireshark

## Objective
Capture and analyze SSH brute force attack traffic at the network 
level using tcpdump and Wireshark.

---

## Tools Used
- tcpdump — packet capture
- Wireshark 4.0.7 — packet analysis
- Hydra — attack simulation (from Phase 2)

---

## Capture Method

Traffic captured on Kali (eth0) using:
```bash
sudo tcpdump -i eth0 host 192.168.64.3 -w ~/ssh_bruteforce.pcap
```
Hydra brute force ran simultaneously in a second terminal.

---

## Findings

### TCP Conversations (Statistics → Conversations → TCP)

| Metric | Value |
|---|---|
| Total TCP Conversations | 5 |
| Packets (Kali → Ubuntu) | 17 |
| Packets (Ubuntu → Kali) | 22 |
| Source IP | 192.168.64.2 (Kali) |
| Destination IP | 192.168.64.3 (Ubuntu) |

---

## Traffic Pattern Analysis

### Observed Packet Types
- **SYN** — Kali initiating connection to Ubuntu port 22
- **SYN-ACK** — Ubuntu accepting the connection
- **ACK** — TCP handshake completion
- **Key Exchange Init** — SSH encryption negotiation (visible per attempt)

### Brute Force Signature in Network Traffic
A normal user establishes one SSH connection. The capture shows 5 
rapid consecutive TCP connections from a single source IP — a clear 
automated brute force signature visible at the network layer.

---

## Fail2Ban Correlation

Only 5 conversations were captured despite Hydra attempting many 
more. This directly correlates with the Fail2Ban configuration 
(maxretry = 5) from Phase 2 — the attacker's IP was automatically 
banned after the 5th failed attempt, cutting off further connections.

This demonstrates two layers of detection:
1. **Log-based detection** — journalctl showing failed password attempts
2. **Network-based evidence** — Wireshark confirming connection attempts 
match the log entries

---

## Commands Reference
```bash
# Capture traffic
sudo tcpdump -i eth0 host 192.168.64.3 -w ~/ssh_bruteforce.pcap

# Open in Wireshark
wireshark ~/ssh_bruteforce.pcap

# Wireshark display filter for SSH
tcp.port == 22
```
