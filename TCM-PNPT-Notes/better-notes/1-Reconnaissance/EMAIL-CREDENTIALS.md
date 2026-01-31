# EMAIL & CREDENTIAL HARVESTING

## Email Discovery
```bash
# Sublist3r - subdomain enum with email hunting
$ sublist3r -d example.com -t 100 -v

# Certificate transparency (common names)
# Visit: https://crt.sh
# Search: %.tesla.com
```

## Breach Database Lookups
```bash
# Dehashed - search breached credentials
# https://dehashed.com

# Hashes.com - crack hashes
# https://hashes.com/en/decrypt/hash
```

## Tools
- **breach-parse:** https://github.com/hmaverickadams/breach-parse
- **Amass:** Network mapping + email discovery
- **HTTProbe:** Test found subdomains

## Commands
```bash
$ amass enum -d example.com
```

## Key Points
- Gather employee emails, usernames
- Check if credentials in breaches
- Build target list for spraying attacks
- Document all findings

