# SUBDOMAIN & TECHNOLOGY ENUMERATION

## Subdomain Discovery
```bash
# Sublist3r
$ sublist3r -d example.com -t 100 -v

# Amass (comprehensive)
$ amass enum -d example.com

# Certificate transparency
# https://crt.sh
# Search: %.domain.com
```

## Probe Subdomains
```bash
# HTTProbe - check which are alive
$ cat subdomains.txt | httprobe

# Nmap verification
$ nmap -iL alive-subdomains.txt -p 80,443
```

## Website Technology Stack
```bash
# WhatWeb - identify tech
$ whatweb example.com

# With UA spoofing
$ whatweb -a 3 --user-agent "Mozilla/5.0" https://example.com

# Online tools
# BuiltWith: https://builtwith.com
# Wappalyzer: https://www.wappalyzer.com
```

## Output & Analysis
- Create target list (alive subdomains)
- Document tech stack (CMS, frameworks, servers)
- Note version numbers for exploit research
- Save HTML for later analysis

