# IDOR — INSECURE DIRECT OBJECT REFERENCE

## Core Concept
An object (file, record, account) is accessed directly via a user-controlled reference (ID, filename)
without authorization checks. Attacker changes the reference to access another user's data.

## Types

| Type | Description |
|------|-------------|
| Horizontal | Access another user's data at the same privilege level |
| Vertical | Access data/functions of a higher privilege level (admin) |

## Where to Look

```
/api/user/1337          → change ID
/files/report_42.pdf    → change filename
/account?id=100         → change parameter
/invoice/download/55    → change number
```

Common parameter names: `id`, `user_id`, `account`, `file`, `doc`, `order`, `uid`

Also check:
- **Request body** (JSON/POST): `{"user_id": 1337}`
- **Cookies**: encoded user IDs
- **Hidden form fields**

## Testing with Burp Suite

1. Log in as user A, note your ID (e.g. `id=100`)
2. Send request to **Repeater**
3. Change ID to another value (`id=101`, `id=1`, `id=99`)
4. Check if you receive another user's data

## Fuzzing IDs with ffuf

```bash
# Generate a number wordlist
$ seq 1 1000 > numbers.txt

# Fuzz the ID
$ ffuf -u "http://target.com/api/user/FUZZ" -w numbers.txt \
  -H "Cookie: session=YOUR-SESSION-COOKIE" \
  -fs <size-of-unauthorized-response>
```

Or with a request file:
```bash
$ ffuf -request req.txt -request-proto http -w numbers.txt -fs <failed-size>
```

## Burp Intruder Approach

1. Intercept request with ID parameter
2. Send to **Intruder**
3. Mark ID as payload position: `/user/§100§`
4. Payload type: Numbers (sequential)
5. Filter by response length → different size = IDOR hit

## Signs of a Successful IDOR

- Response contains another user's name, email, or sensitive data
- Response code changes (403 → 200)
- File downloads that shouldn't be accessible

## Resources
- https://portswigger.net/web-security/access-control/idor
- https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Insecure%20Direct%20Object%20References
