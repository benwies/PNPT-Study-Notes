# DNS & OTHER SERVICES

## DNS Enumeration
```bash
# Basic DNS query
$ nslookup example.com
$ dig example.com

# Full zone transfer attempt
$ dig axfr example.com @ns1.example.com

# Reverse lookup
$ dig -x 192.168.1.1

# DNS recon
$ dnsrecon -d example.com -t axfr

# Specific network range
$ dnsrecon -r 192.168.1.0/24 -n 192.168.1.1 -d local.com
```

## NFS Enumeration
```bash
# Show NFS shares
$ showmount -e 192.168.1.100

# Mount NFS share
$ mount -t nfs 192.168.1.100:/export /mnt/nfs

# Enumerate shares
$ nmap -p 111,2049 --script nfs-* 192.168.1.100
```

## Telnet
```bash
# Quick test (unencrypted!)
$ telnet 192.168.1.100 23
$ telnet 192.168.1.100 80
```

## Hash Identification
```bash
# Identify hash type
$ hash-identifier

# Or manually:
# MD5: 32 hex chars
# SHA1: 40 hex chars
# SHA256: 64 hex chars
# NTLM: Windows hashes

# Crack online: https://hashes.com
```

## Notes
- Always note service versions
- DNS zone transfers = gold
- NFS shares often world-readable
- Telnet = unencrypted (usually disabled)

