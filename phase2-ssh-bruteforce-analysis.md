# Phase 2 — SSH Brute Force Attack: Detection & Analysis

## Scenario Overview
Simulated a brute force attack against an SSH service to practice 
log analysis and threat detection. Kali Linux (attacker) used Hydra 
to perform automated credential stuffing against Ubuntu Server (target).

---

## Lab Environment

| Role | OS | IP Address |
|---|---|---|
| Attacker | Kali Linux ARM64 | 192.168.64.2 |
| Target | Ubuntu 22.04 ARM64 | 192.168.64.3 |

---

## Attack Details

| Property | Value |
|---|---|
| Tool Used | Hydra |
| Protocol Targeted | SSH (Port 22) |
| Username Targeted | ubuntu |
| Wordlist Used | rockyou.txt |
| Threads | 4 (simultaneous connections) |
| Attack Duration | ~62 seconds |
| Total Failed Attempts | 48 |
| Attack Rate | ~1 attempt per 1.3 seconds |
| Attack Window | 02:31:13 – 02:32:15 (UTC) |

---

## Log Evidence

Logs collected using:
```bash
sudo journalctl -u ssh | grep "Failed password"
```

### Sample Log Entries

Apr 30 02:31:13 ubuntu sshd[5687]: Failed password for ubuntu from 192.168.64.2 port 51094 ssh2
Apr 30 02:31:13 ubuntu sshd[5689]: Failed password for ubuntu from 192.168.64.2 port 51120 ssh2
Apr 30 02:31:13 ubuntu sshd[5688]: Failed password for ubuntu from 192.168.64.2 port 51096 ssh2
Apr 30 02:31:13 ubuntu sshd[5686]: Failed password for ubuntu from 192.168.64.2 port 51092 ssh2

---

## Analysis — Indicators of Compromise (IOCs)

| Indicator | Observation | Significance |
|---|---|---|
| Source IP | 192.168.64.2 | Single IP responsible for all attempts |
| Attempt Volume | 48 failed attempts in 62 seconds | Far exceeds normal human login behavior |
| Simultaneous Connections | 4 parallel ports open at once | Confirms automated tool, not manual attempt |
| Attempt Interval | ~1.3 seconds between attempts | Consistent with automated brute force |
| Target Username | ubuntu (default) | Attacker targeting predictable default accounts |
| Server Response | Disconnected after max retries exceeded | Default SSH hardening partially effective |

---

## Detection — How a SOC Analyst Would Catch This

1. **Volume threshold alert** — 48 failed logins in under 2 minutes from a 
single IP would trigger a SIEM alert in any production environment
2. **Concurrent session anomaly** — 4 simultaneous SSH connections from 
the same source is abnormal and detectable
3. **Regular timing pattern** — human login attempts are irregular; 
1.3 second intervals indicate automation
4. **Default username targeting** — targeting 'ubuntu', 'admin', 'root' 
is a signature of credential stuffing tools

---

## Defensive Recommendations

1. **Implement Fail2Ban** — automatically block IPs after N failed attempts
2. **Disable password authentication** — enforce SSH key-based auth only
3. **Change default SSH port** — reduces automated scanning noise
4. **Restrict SSH access by IP** — whitelist known IPs via firewall rules
5. **Monitor with SIEM** — set alerts for >5 failed logins per minute 
from single source

---

## Outcome

Attack failed. Ubuntu's default SSH configuration disconnected the 
attacker after maximum authentication attempts were exceeded. 
However, without Fail2Ban or IP blocking, the attacker was free 
to reconnect and continue attempting — which is why defensive 
recommendations above are critical in production environments.

---

## Tools & Commands Used

```bash
# On Ubuntu — monitor SSH logs
sudo journalctl -u ssh -n 50

# Count failed attempts
sudo journalctl -u ssh | grep "Failed password" | wc -l

# View attack window
sudo journalctl -u ssh | grep "Failed password" | head -5
sudo journalctl -u ssh | grep "Failed password" | tail -5
```

## Defensive Implementation — Fail2Ban

Installed and configured Fail2Ban to automatically ban IPs exceeding 
the failed login threshold.

### Configuration (/etc/fail2ban/jail.local)
[DEFAULT]
backend = systemd
[sshd]
enabled = true
port = ssh
maxretry = 5
bantime = 600
findtime = 600

### Result
Re-ran Hydra brute force simulation. Fail2Ban detected the attack 
and automatically banned 192.168.64.2 (Kali) after 5 failed attempts.

Verified with:
```bash
sudo fail2ban-client status sshd
```
Output confirmed: 1 IP banned.

### What This Demonstrates
- Automated threat response without manual intervention
- 600 second ban window stops the attack immediately
- In production, bantime would typically be 24 hours or permanent
