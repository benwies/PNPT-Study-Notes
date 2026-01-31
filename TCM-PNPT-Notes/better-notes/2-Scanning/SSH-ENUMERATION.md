# SSH ENUMERATION & EXPLOITATION

## Basic SSH Commands
```bash
# Connect
$ ssh user@192.168.1.100

# With non-standard port
$ ssh -p 2222 user@192.168.1.100

# Specify key
$ ssh -i key.pem user@192.168.1.100
```

## SSH with Weak Algorithms (CVE Bypass)
```bash
# If modern SSH won't connect to old servers:
$ ssh -oKexAlgorithms=+diffie-hellman-group1-sha1 user@192.168.1.100

# With cipher options
$ ssh -oKexAlgorithms=+diffie-hellman-group1-sha1 \
  -c aes128-cbc user@192.168.1.100
```

## Brute Force SSH
```bash
# Hydra
$ hydra -l root -P /usr/share/wordlists/rockyou.txt ssh://192.168.1.100:22 -t 4 -V

# Metasploit
$ msfconsole
> search ssh_login
> use auxiliary/scanner/ssh/ssh_login
> set RHOSTS 192.168.1.100
> set USERPASS_FILE creds.txt
> run
```

## SSH Version Scanning
```bash
$ nmap -p 22 -sV 192.168.1.100
```

## Security Tips During Recon
- Check version for known CVEs
- Look for:
  - Weak algorithms
  - Key-based auth allowed
  - Default credentials (pi:raspberry, debian:debian)
  - SSH tunneling opportunities

