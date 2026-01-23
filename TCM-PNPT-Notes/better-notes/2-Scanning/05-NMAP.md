# SCANNING WITH NMAP

## Quick Commands
```bash
# Find live hosts
$ arp-scan -l
$ netdiscover -r 192.168.1.0/24

# Fast full port scan
$ nmap -T4 -p- 192.168.1.100

# Detailed scan on open ports
$ nmap -T4 -p 22,80,443 -A 192.168.1.100

# UDP scan
$ nmap -sU -T4 -p 53,123,161 192.168.1.100

# SYN stealth scan
$ nmap -sS 192.168.1.100
```

## Nmap Flags
| Flag | Meaning |
|------|---------|
| -sS | SYN scan (stealth) |
| -sU | UDP scan |
| -A | Aggressive (OS, service, script) |
| -p | Port(s) |
| -p- | All ports (1-65535) |
| -T4 | Timing (1-5) |
| -oX | XML output |

## Best Practice Workflow
```bash
1. $ nmap -T4 -p- 192.168.1.100 > open-ports.txt
2. Extract open ports
3. $ nmap -T4 -p "22,80,443,3306" -A -oX results.xml 192.168.1.100
4. Analyze detailed output
```

## Output
- Service identification
- OS fingerprinting
- Version detection
- Vulnerability scripts

