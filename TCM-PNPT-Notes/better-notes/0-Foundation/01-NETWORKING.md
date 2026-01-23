# NETWORKING BASICS

## OSI Model (7 Layers)
```
7. Application  - HTTP, SMTP, DNS
6. Presentation - Encryption, compression (JPEG, MOV)
5. Session      - Connection management
4. Transport    - TCP, UDP
3. Network      - IP, Routing
2. Data Link    - Switching, MAC addresses
1. Physical     - Cables, hardware
```

## IP Addressing
- **IPv4:** 32-bit (max 2^32 addresses)
- **IPv6:** 128-bit (max 2^128 addresses)
- **Decimal Format:** 192.168.1.1
- **Hex Format (IPv6):** 2001:0db8::ff00:42:8329

## TCP vs UDP
### TCP (Transmission Control Protocol)
- Connection-oriented
- 3-way handshake: SYN → SYN-ACK → ACK
- Reliable, ordered delivery
- **Use:** HTTPS, SMTP, SSH, FTP

### UDP (User Datagram Protocol)
- Connectionless
- No handshake
- Fast, no guarantees
- **Use:** DNS, DHCP, VoIP, Gaming

## Subnetting Basics
- **Private Ranges:** 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16
- **Tools:** Online subnet calculator, CIDR notation
- **Key:** /24 = 254 usable hosts, /16 = 65,534 usable hosts

## MAC Addresses
- 48-bit (6 octets): AA:BB:CC:DD:EE:FF
- Physical addressing on local network
- First 3 octets = Manufacturer (OUI)

## Key Resources
- Subnet Calculator: https://www.ipaddressguide.com
- Whois/IP Lookup tools

