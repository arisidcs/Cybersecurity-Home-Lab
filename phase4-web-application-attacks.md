# Phase 4 — Web Application Attack Simulation (DVWA)

## Objective
Set up a deliberately vulnerable web application and demonstrate 
common web attack techniques in a controlled lab environment.

---

## Environment

| Role | Details |
|---|---|
| Target | DVWA (Damn Vulnerable Web Application) on Ubuntu 22.04 |
| Attacker | Kali Linux |
| Target IP | 192.168.64.3 |
| Web Server | Apache 2.4.52 |
| Database | MariaDB |
| Language | PHP 8.1 |

---

## Setup Summary
- Installed Apache, PHP, MariaDB on Ubuntu
- Cloned DVWA from GitHub
- Configured dedicated database user with least-privilege access
- Verified setup via DVWA setup page

---

## Attack 1 — SQL Injection

### What is SQL Injection?
SQL Injection occurs when user input is inserted directly into a 
database query without sanitization. An attacker can manipulate 
the query to return unauthorized data or bypass authentication.

### Test Performed
On the DVWA SQL Injection module (Security Level: Low), entered 
the following payload in the User ID field:
