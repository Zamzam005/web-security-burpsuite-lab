# Lab Findings report

## Target: http://localhost (Bug Bounty Labs)

---

## Finding 1 — Username Enumeration + Brute Force
**Lab:** Auth 0x01
**Severity:** High
**Tool used:** Burp Suite Intruder

**What I found:**
The login form reveals whether a username exists
or not through different error messages.
This allowed me to enumerate valid usernames
and then brute force the password.

**Steps:**
1. Intercepted login request in Burp Suite
2. Sent to Intruder
3. Fuzzed username field with wordlist
4. Identified valid username from response length
5. Brute forced password successfully

**Impact:**
Attacker can gain unauthorized access to any account

**Fix:**
Use same error message for wrong username and password

---

## Finding 2 — MFA Bypass
**Lab:** Auth 0x02
**Severity:** Critical
**Tool used:** Burp Suite Intruder

**What I found:**
The MFA code was not rate limited — allowing
an attacker to brute force all possible codes
until the correct one is found.

**Steps:**
1. Logged in with valid credentials
2. Intercepted MFA request in Burp Suite
3. Sent to Intruder
4. Fuzzed MFA code field with numbers 000000-999999
5. Found correct code from different response

**Impact:**
Attacker can bypass MFA and access any account
even without the victim's phone

**Fix:**
Add rate limiting and lockout after failed attempts

---

## Finding 3 — IDOR (Insecure Direct Object Reference)
**Lab:** Auth 0x03
**Severity:** High
**Tool used:** Burp Suite

**What I found:**
User profile pages use predictable numeric IDs
in the URL. Changing the ID allows access to
other users' private data.

**Steps:**
1. Logged in as jeremy
2. Intercepted profile request in Burp Suite
3. Changed id parameter from 2 to 1
4. Accessed another user's private data

**Impact:**
Attacker can access any user's private information

**Fix:**
Use unpredictable IDs and check authorization
on every request
