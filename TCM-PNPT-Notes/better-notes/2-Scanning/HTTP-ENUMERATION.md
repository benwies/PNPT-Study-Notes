# ENUMERATING HTTP/HTTPS

## Manual Reconnaissance
```bash
# Visit target URL in browser
# Right-click → View Page Source
# Look for:
# - Comments with clues
# - Hidden form fields
# - API endpoints
# - Version info
```

## Nikto Web Scanner
```bash
# Basic scan
$ nikto -h http://192.168.1.100

# Save results
$ nikto -h http://192.168.1.100 -o report.html

# Specific port
$ nikto -h http://192.168.1.100:8080
```

## Directory Brute Force
```bash
# FFUF - very fast
$ ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt:FUZZ \
  -u http://192.168.1.100/FUZZ -o ffuf-results.txt

# DirBuster (GUI)
$ dirbuster &
# Set URL, wordlist, threads
![[Pasted image 20260122191229.png]]```

## Burp Suite
```bash
1. Set Firefox proxy: 127.0.0.1:8080
2. Start Burp Suite
3. Intercept traffic
4. Send requests to Repeater
5. Analyze responses
```

## Common Findings
- Sensitive files: /admin, /backup, /.git, /config
- API endpoints: /api/v1, /graphql
- Default credentials: admin/admin
- Version disclosure

