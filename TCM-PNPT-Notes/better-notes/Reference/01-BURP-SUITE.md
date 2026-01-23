# BURP SUITE COMPLETE GUIDE

## Setup

### Firefox Configuration
1. **Settings → Network Settings**
2. Select: Manual proxy configuration
3. **HTTP Proxy:** 127.0.0.1
4. **Port:** 8080
5. ✓ Use proxy for all protocols

![[Pasted image 20260122184259.png]]
![[Pasted image 20260122184339.png]]

## Basic Workflow

### 1. Intercept Traffic
- Start Burp Suite (Community/Pro)
- Enable Interception (Proxy tab)
- Browse target site
- Requests appear in Intercept tab

### 2. Send to Repeater
- Right-click request
- **Send to Repeater**
- Modify request (headers, body, params)
- Send & analyze response

### 3. Scan for Vulnerabilities
- **Scanner tab → New scan**
- Target URL
- Full scan or crawl only
- Wait for results
- Review findings

## Key Features

### Fuzzing/Testing
```
Repeater:
- Modify parameter values
- Change HTTP method (GET → POST)
- Inject payloads (SQLi, XSS, etc)
- Observe responses
```

### Spider/Crawl
- **Target → Scope**
- Add target domain
- **Spider tab → Start crawling**
- Discovers all endpoints
- Export to use with other tools

## Useful Functions
| Function | Use |
|----------|-----|
| Intercept | Pause & modify requests |
| Repeater | Test individual requests |
| Scanner | Automated vulnerability scan |
| Intruder | Automated parameter fuzzing (Pro) |
| Decoder | Decode/encode payloads |
| Comparer | Compare two responses |

## Common Testing Flow
```
1. Spider target
2. Intercept interesting requests
3. Send to Repeater for manual testing
4. Test for:
   - SQL Injection
   - XSS
   - CSRF
   - Authentication bypass
5. Modify payloads & analyze responses
```

