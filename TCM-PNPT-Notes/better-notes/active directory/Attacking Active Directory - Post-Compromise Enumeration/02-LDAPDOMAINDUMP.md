# LDAP DOMAIN DUMP

Extract comprehensive LDAP information from Active Directory including users, groups, computers, and policies.

## Installation

\\\ash
pip install ldapdomaindump
\\\

## Basic Usage

Unencrypted LDAP (port 389):

\\\ash
ldapdomaindump ldap://10.0.2.15 -u 'MARVEL\\fcastle' -p Password1
\\\

Encrypted LDAPS (port 636):

\\\ash
ldapdomaindump ldaps://10.0.2.15 -u 'MARVEL\\fcastle' -p Password1
\\\

Null authentication:

\\\ash
ldapdomaindump ldap://10.0.2.15 -u '' -p ''
\\\

Full domain dump to directory:

\\\ash
ldapdomaindump -o output_dir ldaps://10.0.2.15 -u 'MARVEL\\fcastle' -p Password1
\\\

## Output Files

Generates HTML and CSV reports:
- \domain_users.html\, \domain_groups.html\, \domain_computers.html\
- \domain_policy.html\, \domain_trusts.html\
- \.csv\ files for further analysis

## Advanced Options

\\\ash
ldapdomaindump -o /custom/path ldaps://10.0.2.15 -u 'MARVEL\\fcastle' -p Password1
ldapdomaindump --machines ldaps://10.0.2.15 -u 'MARVEL\\fcastle' -p Password1
ldapdomaindump --quiet ldaps://10.0.2.15 -u 'MARVEL\\fcastle' -p Password1
\\\

## Integration

### With CrackMapExec

Identify targets for password spraying:

\\\ash
ldapdomaindump ldaps://10.0.2.15 -u 'MARVEL\\fcastle' -p Password1 -o ldd_output
crackmapexec smb 10.0.2.0/24 -u [users.csv] -p 'Password1' -d MARVEL.local
\\\

### With BloodHound

Combine LDAP data with BloodHound for complete enumeration and privilege escalation paths
