# SMB ENUMERATION

## Quick Commands
```bash
# View SMB shares
$ smbclient -L \\\\192.168.1.100

# Connect to share
$ smbclient \\\\192.168.1.100\\sharename

# List with credentials
$ smbclient -L \\\\192.168.1.100 -U username%password
```

## Metasploit SMB Enumeration
```bash
$ msfconsole

# Find SMB version
> search smb_version
> use auxiliary/scanner/smb/smb_version
> set RHOSTS 192.168.1.100
> set THREADS 10
> run

# Find SMB login vulnerabilities
> search smb_login
> use auxiliary/scanner/smb/smb_login
> set USERPASS_FILE /path/to/creds.txt
> run
```

## Nmap SMB Scripts
```bash
$ nmap -p 445 --script smb-enum-shares,smb-enum-users,smb-vuln-* 192.168.1.100
```

## Common Vulnerabilities
- **EternalBlue (CVE-2017-0144)** - SMB remote code execution
- Null sessions (no credentials needed)
- Weak credentials
- Unpatched SMB (Windows XP, Server 2003)

## Next Steps
- Mount shares
- Extract files
- Look for credentials, documents
- Check for sensitive data

