# TCM PNPT PENTESTING HANDBOOK

**Reference Guide for the [TCM PNPT Certification](https://certifications.tcm-sec.com/pnpt/)**

Comprehensive handbook covering all pentesting phases: reconnaissance, scanning, enumeration, exploitation, privilege escalation, post-exploitation, Active Directory attack chains, web application enumeration, and common web vulnerabilities.

---

## Contents

### Foundation
- [QUICK-START](TCM-PNPT-Notes/better-notes/0-Foundation/QUICK-START.md)
- [NETWORKING](TCM-PNPT-Notes/better-notes/0-Foundation/NETWORKING.md)
- [TOOLS-RESOURCES](TCM-PNPT-Notes/better-notes/0-Foundation/TOOLS-RESOURCES.md)

### Reconnaissance
- [PASSIVE-RECON](TCM-PNPT-Notes/better-notes/1-Reconnaissance/PASSIVE-RECON.md)
- [EMAIL-CREDENTIALS](TCM-PNPT-Notes/better-notes/1-Reconnaissance/EMAIL-CREDENTIALS.md)

### Scanning & Enumeration
- [NMAP](TCM-PNPT-Notes/better-notes/2-Scanning/NMAP.md)
- [SUBDOMAIN-TECH](TCM-PNPT-Notes/better-notes/2-Scanning/SUBDOMAIN-TECH.md)
- [HTTP-ENUMERATION](TCM-PNPT-Notes/better-notes/2-Scanning/HTTP-ENUMERATION.md)
- [SMB-ENUMERATION](TCM-PNPT-Notes/better-notes/2-Scanning/SMB-ENUMERATION.md)
- [SSH-ENUMERATION](TCM-PNPT-Notes/better-notes/2-Scanning/SSH-ENUMERATION.md)
- [DNS-OTHER-SERVICES](TCM-PNPT-Notes/better-notes/2-Scanning/DNS-OTHER-SERVICES.md)
- [VULN-SCANNING](TCM-PNPT-Notes/better-notes/2-Scanning/VULN-SCANNING.md)

### Exploitation
- [BRUTE-FORCE](TCM-PNPT-Notes/better-notes/3-Exploitation/BRUTE-FORCE.md)
- [REVERSE-SHELLS](TCM-PNPT-Notes/better-notes/3-Exploitation/REVERSE-SHELLS.md)
- [METASPLOIT](TCM-PNPT-Notes/better-notes/3-Exploitation/METASPLOIT.md)
- [WEB-EXPLOITATION](TCM-PNPT-Notes/better-notes/3-Exploitation/WEB-EXPLOITATION.md)
- [ACTIVE-DIRECTORY](TCM-PNPT-Notes/better-notes/3-Exploitation/ACTIVE-DIRECTORY.md)

### Privilege Escalation
- [PRIVESC](TCM-PNPT-Notes/better-notes/4-Privesc/PRIVESC.md)

### Active Directory

**Initial Attack Vectors**
- [LLMNR Poisoning](TCM-PNPT-Notes/better-notes/5-ActiveDirectory/1Attacking%20Active%20Directory%20-%20Initial%20Attack%20Vectors/llmnr%20poisoning.md)
- [SMB Relay](TCM-PNPT-Notes/better-notes/5-ActiveDirectory/1Attacking%20Active%20Directory%20-%20Initial%20Attack%20Vectors/smb%20relay.md)
- [Gaining Shell Access](TCM-PNPT-Notes/better-notes/5-ActiveDirectory/1Attacking%20Active%20Directory%20-%20Initial%20Attack%20Vectors/Gaining%20Shell%20Access.md)
- [IPv6 DNS Takeover via mitm6](TCM-PNPT-Notes/better-notes/5-ActiveDirectory/1Attacking%20Active%20Directory%20-%20Initial%20Attack%20Vectors/IPv6%20DNS%20Takeover%20via%20mitm6.md)

**Post-Compromise Enumeration**
- [BloodHound / PlumHound / PingCastle](TCM-PNPT-Notes/better-notes/5-ActiveDirectory/2Attacking%20Active%20Directory%20-%20Post-Compromise%20Enumeration/01-BLOODHOUND-PLUMHOUND-PINGCASTLE.md)
- [LDAPDomainDump](TCM-PNPT-Notes/better-notes/5-ActiveDirectory/2Attacking%20Active%20Directory%20-%20Post-Compromise%20Enumeration/02-LDAPDOMAINDUMP.md)

**Post-Compromise Attacks**
- [Post-Compromise Attack Strategy](TCM-PNPT-Notes/better-notes/5-ActiveDirectory/3Attacking%20Active%20Directory%20-%20Post-Compromise%20Attacks/Post-Compromise%20Attack%20Strategy.md)
- [Dumping Hashes](TCM-PNPT-Notes/better-notes/5-ActiveDirectory/3Attacking%20Active%20Directory%20-%20Post-Compromise%20Attacks/01-DUMPING-HASHES.md)
- [Kerberoasting](TCM-PNPT-Notes/better-notes/5-ActiveDirectory/3Attacking%20Active%20Directory%20-%20Post-Compromise%20Attacks/02-KERBEROASTING.md)
- [Pass Attacks](TCM-PNPT-Notes/better-notes/5-ActiveDirectory/3Attacking%20Active%20Directory%20-%20Post-Compromise%20Attacks/03-PASS-ATTACKS.md)
- [Token Impersonation](TCM-PNPT-Notes/better-notes/5-ActiveDirectory/3Attacking%20Active%20Directory%20-%20Post-Compromise%20Attacks/Token%20Impersonation.md)
- [LNK File Attacks](TCM-PNPT-Notes/better-notes/5-ActiveDirectory/3Attacking%20Active%20Directory%20-%20Post-Compromise%20Attacks/LNK%20File%20Attacks.md)
- [GPP Attack](TCM-PNPT-Notes/better-notes/5-ActiveDirectory/3Attacking%20Active%20Directory%20-%20Post-Compromise%20Attacks/GPP%20Attack.md)

**We've Compromised the Domain — Now What?**
- [Dumping the NTDS.dit](TCM-PNPT-Notes/better-notes/5-ActiveDirectory/4We've%20Compromised%20the%20Domain%20%20Now%20What/Dumping%20the%20NTDS.dit.md)
- [Golden Ticket Attacks](TCM-PNPT-Notes/better-notes/5-ActiveDirectory/4We've%20Compromised%20the%20Domain%20%20Now%20What/Golden%20Ticket%20Attacks.md)

**Additional Active Directory Attacks**
- [PrintNightmare (CVE-2021-1675)](TCM-PNPT-Notes/better-notes/5-ActiveDirectory/5Additional%20Active%20Directory%20Attacks/PrintNightmare%20(CVE-2021-1675).md)
- [ZeroLogon](TCM-PNPT-Notes/better-notes/5-ActiveDirectory/5Additional%20Active%20Directory%20Attacks/ZeroLogon.md)

### Post-Exploitation
- [POST-EXPLOITATION](TCM-PNPT-Notes/better-notes/5-PostExploitation/POST-EXPLOITATION.md)
- [FILE-CRACKING](TCM-PNPT-Notes/better-notes/5-PostExploitation/FILE-CRACKING.md)
- [File Transfers](TCM-PNPT-Notes/better-notes/6-Post%20Exploitation/File%20Transfers.md)
- [Maintaining Access](TCM-PNPT-Notes/better-notes/6-Post%20Exploitation/Maintaining%20Access.md)
- [Pivoting](TCM-PNPT-Notes/better-notes/6-Post%20Exploitation/Pivoting.md)

### Web Application Enumeration
- [Assetfinder, Amass & httprobe](TCM-PNPT-Notes/better-notes/7-Web%20Application%20Enumeration/Assetfinder%20and%20Amass%20and%20httprobe.md)
- [Screenshotting with GoWitness](TCM-PNPT-Notes/better-notes/7-Web%20Application%20Enumeration/Screenshotting%20Websites%20with%20GoWitness.md)
- [Automating the Enumeration Process](TCM-PNPT-Notes/better-notes/7-Web%20Application%20Enumeration/Automating%20the%20Enumeration%20Process.md)
- [Additional Resources](TCM-PNPT-Notes/better-notes/7-Web%20Application%20Enumeration/Additional%20Resources.md)

### Common Web Vulnerabilities
- [SQL Injection](TCM-PNPT-Notes/better-notes/Common%20Web%20Vulnerabilities/SQL_Injection.md)
- [XSS](TCM-PNPT-Notes/better-notes/Common%20Web%20Vulnerabilities/XSS.md)
- [Command Injection](TCM-PNPT-Notes/better-notes/Common%20Web%20Vulnerabilities/Command_Injection.md)
- [IDOR](TCM-PNPT-Notes/better-notes/Common%20Web%20Vulnerabilities/IDOR.md)
- [Attacking Authentication](TCM-PNPT-Notes/better-notes/Common%20Web%20Vulnerabilities/Attacking_Authentication.md)
- [XXE](TCM-PNPT-Notes/better-notes/Common%20Web%20Vulnerabilities/XXE.md)
- [Insecure File Upload](TCM-PNPT-Notes/better-notes/Common%20Web%20Vulnerabilities/InsecureFileUpload.md)

### Reference
- [BURP-SUITE](TCM-PNPT-Notes/better-notes/Reference/01-BURP-SUITE.md)
- [CHEATSHEET](TCM-PNPT-Notes/better-notes/Reference/02-CHEATSHEET.md)
- [REPORTING-LEGAL](TCM-PNPT-Notes/better-notes/Reference/03-REPORTING-LEGAL.md)

---
