# VULNERABILITY SCANNING

## Nessus
```bash
# Download from: https://www.tenable.com/downloads
# Steps:
1. Install Nessus
2. Access: https://localhost:8834
3. Create scan policy
4. Run scan on target(s)
```

## SearchSploit
```bash
# Search local exploit database
$ searchsploit Apache 2.4.7

# Get detailed exploit info
$ searchsploit -m 47918  # download exploit

# Update database
$ searchsploit -u
```

## Online Resources
- Google exploits + service version
- ExploitDB: https://www.exploit-db.com
- Shodan: https://www.shodan.io (if allowed)

## Workflow
1. Identify service + version (from Nmap)
2. Search for CVEs
3. Check CVSS score
4. Test POC locally first
5. Document findings

## Common Vulnerable Services
- Apache/Nginx with known CVEs
- Old PHP/MySQL versions
- Unpatched SMB (Eternal Blue)
- SSH with weak algorithms
- FTP without TLS

