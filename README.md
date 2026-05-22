
# Web Application Security Testing — Burp Suite Lab Report

## Overview
Practical web application penetration testing performed 
on a local vulnerable lab environment as part of 
TCM Security Practical Bug Bounty course.

## Tester
- Name: Zamzam Hassan
- Focus: Web Penetration Testing
- OS: Kali Linux
- Tools: Burp Suite, ffuf

## Target
- URL: http://localhost (Bug Bounty Labs)
- Type: Local vulnerable web application
- Setup: Docker

## Vulnerabilities Found

### 1. Username Enumeration + Brute Force
- Lab: Auth 0x01
- Severity: High
- Tool: Burp Suite Intruder

### 2. MFA Bypass
- Lab: Auth 0x02
- Severity: Critical
- Tool: Burp Suite Intruder

### 3. IDOR (Insecure Direct Object Reference)
- Lab: Auth 0x03
- Severity: High
- Tool: Burp Suite

### 4. IDOR via Account Fuzzing
- Lab: Auth 0x02
- Severity: High
- Tool: ffuf

### 5. Password Brute Force
- Lab: Auth 0x01
- Severity: High
- Tool: ffuf

## Commands Used
```bash
# IDOR account fuzzing
ffuf -u 'http://localhost/labs/e0x02.php?account=FUZZ' \
     -w num.txt -mr 'admin'

# Password brute force
ffuf -request req.txt -request-proto http \
     -w /usr/share/seclists/Passwords/Common-Credentials/\
xato-net-10-million-passwords-10000.txt
```

## Screenshots
All proof of concept screenshots are in the 
screenshots/ folder

## Skills Demonstrated
- Burp Suite interception and manipulation
- Burp Suite Intruder for fuzzing
- IDOR vulnerability testing
- MFA bypass techniques
- Password brute forcing with ffuf
- Authentication attack techniques
