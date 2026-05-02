
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
## Phase 3 — Network & Web Application Testing (Upcoming)
