


ping google.com

![[Pasted image 20250808214154.png]]



nmap -T4 -p- -A 192.168.57.4


![[Pasted image 20250808221326.png]]

![[Pasted image 20250808223412.png]]

Enumeration sbm:
msfconsole
use auxiliary/scanner/smb/smb_version

![[Pasted image 20250812145702.png]]

 smbclient -L \\\\192.168.57.4\\


![[Pasted image 20250812150050.png]]


![[Pasted image 20250812150225.png]]

DEADEND


