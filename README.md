# TCM PNPT PENTESTING HANDBOOK

**Study & Reference Guide for the [TCM PNPT Certification](https://www.tcm-sec.com/penetration-tester-certification/)**

## Overview

This is a comprehensive, well-organized reference handbook for **Practical Network Penetration Testing (PNPT)** engagements. It covers the complete attack chain from reconnaissance through post-exploitation, with practical commands, tools, and techniques for each phase.

The handbook is structured for **quick reference during security assessments** - organized by attack phase with minimal fluff, maximum actionable content. Each section includes specific tools, command syntax, and step-by-step workflows.

### What's Covered

- **Reconnaissance & OSINT** - Passive information gathering, email/credential discovery
- **Scanning & Enumeration** - Nmap, service detection, vulnerability scanning
- **Exploitation** - Brute force, web attacks, reverse shells, Active Directory attacks
- **Privilege Escalation** - Linux & Windows techniques
- **Post-Exploitation** - Data extraction, persistence, cleanup
- **Active Directory** - Complete attack chain from initial compromise to domain dominance

---

## Table of Contents

### Foundation
- [QUICK-START](TCM-PNPT-Notes/better-notes/0-Foundation/QUICK-START.md) - 5-stage methodology, tools overview, common ports
- [NETWORKING](TCM-PNPT-Notes/better-notes/0-Foundation/NETWORKING.md) - OSI model, TCP/UDP, IP addressing, subnetting
- [TOOLS-RESOURCES](TCM-PNPT-Notes/better-notes/0-Foundation/TOOLS-RESOURCES.md) - Essential tools by phase, reference links

### Reconnaissance
- [PASSIVE-RECON](TCM-PNPT-Notes/better-notes/1-Reconnaissance/PASSIVE-RECON.md) - OSINT platforms, domain/email discovery, no-alarm gathering
- [EMAIL-CREDENTIALS](TCM-PNPT-Notes/better-notes/1-Reconnaissance/EMAIL-CREDENTIALS.md) - Email harvesting, breach database lookup, credential intelligence

### Scanning & Enumeration
- [NMAP](TCM-PNPT-Notes/better-notes/2-Scanning/NMAP.md) - Port scanning strategies, service fingerprinting, advanced scripts
- [SUBDOMAIN-TECH](TCM-PNPT-Notes/better-notes/2-Scanning/SUBDOMAIN-TECH.md) - Subdomain enumeration, technology stack identification
- [HTTP-ENUMERATION](TCM-PNPT-Notes/better-notes/2-Scanning/HTTP-ENUMERATION.md) - Web directory brute force, Burp Suite, Nikto scanning
- [SMB-ENUMERATION](TCM-PNPT-Notes/better-notes/2-Scanning/SMB-ENUMERATION.md) - Windows share enumeration, SMB version detection
- [SSH-ENUMERATION](TCM-PNPT-Notes/better-notes/2-Scanning/SSH-ENUMERATION.md) - SSH service reconnaissance, version detection
- [DNS-OTHER-SERVICES](TCM-PNPT-Notes/better-notes/2-Scanning/DNS-OTHER-SERVICES.md) - DNS enumeration, NFS, Telnet, hash identification
- [VULN-SCANNING](TCM-PNPT-Notes/better-notes/2-Scanning/VULN-SCANNING.md) - Nessus, SearchSploit, CVE research methodology

### Exploitation
- [BRUTE-FORCE](TCM-PNPT-Notes/better-notes/3-Exploitation/BRUTE-FORCE.md) - Hydra syntax, credential spraying, service-specific attacks
- [REVERSE-SHELLS](TCM-PNPT-Notes/better-notes/3-Exploitation/REVERSE-SHELLS.md) - MSFVenom payloads, one-liners, staged vs non-staged
- [METASPLOIT](TCM-PNPT-Notes/better-notes/3-Exploitation/METASPLOIT.md) - MSFConsole fundamentals, auxiliary modules, exploit workflow
- [WEB-EXPLOITATION](TCM-PNPT-Notes/better-notes/3-Exploitation/WEB-EXPLOITATION.md) - SQL injection, LFI/RFI, file upload exploits, PHP shells
- [ACTIVE-DIRECTORY](TCM-PNPT-Notes/better-notes/3-Exploitation/ACTIVE-DIRECTORY.md) - LLMNR poisoning, Kerberoasting, Pass-the-Hash basics

### Privilege Escalation
- [PRIVESC](TCM-PNPT-Notes/better-notes/4-Privesc/PRIVESC.md) - Linux (SUID, sudo, cron) & Windows (UAC, DLL hijacking) escalation techniques

### Post-Exploitation
- [POST-EXPLOITATION](TCM-PNPT-Notes/better-notes/5-PostExploitation/POST-EXPLOITATION.md) - Data exfiltration, file transfer, log cleanup
- [FILE-CRACKING](TCM-PNPT-Notes/better-notes/5-PostExploitation/FILE-CRACKING.md) - Hash cracking (John, Hashcat), file extraction

### Active Directory Attacks
**Initial Attack Vectors:**
- [LLMNR Poisoning](TCM-PNPT-Notes/better-notes/active%20directory/Attacking%20Active%20Directory%20-%20Initial%20Attack%20Vectors/llmnr%20poisoning.md) - Responder-based credential capture
- [SMB Relay](TCM-PNPT-Notes/better-notes/active%20directory/Attacking%20Active%20Directory%20-%20Initial%20Attack%20Vectors/smb%20relay.md) - NTLM relay attacks to bypass SMB signing
- [Gaining Shell Access](TCM-PNPT-Notes/better-notes/active%20directory/Attacking%20Active%20Directory%20-%20Initial%20Attack%20Vectors/Gaining%20Shell%20Access.md) - PSExec exploitation, password & hash-based access

**Post-Compromise Enumeration:**
- [Users & Groups](TCM-PNPT-Notes/better-notes/active%20directory/Attacking%20Active%20Directory%20-%20Post-Compromise%20Enumeration/USERS-GROUPS.md) - User/group discovery, membership enumeration
- [Domain Structure](TCM-PNPT-Notes/better-notes/active%20directory/Attacking%20Active%20Directory%20-%20Post-Compromise%20Enumeration/DOMAIN-STRUCTURE.md) - Domain trusts, OUs, ACL analysis
- [Shares & Resources](TCM-PNPT-Notes/better-notes/active%20directory/Attacking%20Active%20Directory%20-%20Post-Compromise%20Enumeration/SHARES-RESOURCES.md) - Network share discovery, access enumeration

**Post-Compromise Attacks:**
- [Privilege Escalation](TCM-PNPT-Notes/better-notes/active%20directory/Attacking%20Active%20Directory%20-%20Post-Compromise%20Attacks/PRIVILEGE-ESCALATION.md) - Kerberoasting, delegation abuse, privesc chains
- [Lateral Movement](TCM-PNPT-Notes/better-notes/active%20directory/Attacking%20Active%20Directory%20-%20Post-Compromise%20Attacks/LATERAL-MOVEMENT.md) - Pass-the-Hash, Pass-the-Ticket, lateral techniques
- [Persistence](TCM-PNPT-Notes/better-notes/active%20directory/Attacking%20Active%20Directory%20-%20Post-Compromise%20Attacks/PERSISTENCE.md) - Backdoor accounts, GPO abuse, scheduled task persistence

### Reference
- [BURP-SUITE](TCM-PNPT-Notes/better-notes/Reference/BURP-SUITE.md) - Configuration, intercepting, scanning techniques
- [CHEATSHEET](TCM-PNPT-Notes/better-notes/Reference/CHEATSHEET.md) - Quick command reference
- [REPORTING-LEGAL](TCM-PNPT-Notes/better-notes/Reference/REPORTING-LEGAL.md) - Documentation standards, legal framework

---


