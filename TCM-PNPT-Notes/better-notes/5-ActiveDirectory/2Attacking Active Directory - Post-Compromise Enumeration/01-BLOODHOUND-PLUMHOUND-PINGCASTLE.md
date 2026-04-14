# BLOODHOUND, PLUMHOUND & PINGCASTLE

Map Active Directory structure, identify attack paths, and visualize privilege escalation chains.

## BloodHound

Collects and analyzes AD data to visualize attack paths and identify privilege escalation routes.

### Data Collection

#### SharpHound (Windows)

```bash
.\\SharpHound.exe -c All --zipfilename output.zip
```

#### BloodHound Python (Linux)

```bash
bloodhound-python MARVEL.local/fcastle:Password1@10.0.2.15 -d MARVEL.local -c All
```

### Analysis

1. Download BloodHound GUI: https://github.com/BloodHoundAD/BloodHound/releases
2. Import .zip file from SharpHound
3. Analyze paths to Domain Admin
4. Identify weak ACL chains
5. Follow attack paths for privilege escalation

Key queries: Find Path to Domain Admin, Find Longest ACL Path, Find All Domain Admins, Find Kerberoastable Users

## PlumHound

Generates actionable security reports from BloodHound data.

```bash
git clone https://github.com/PlumHound/PlumHound
cd PlumHound && pip install -r requirements.txt

python PlumHound.py -x neo4j -u neo4j -p password --db bolt://localhost:7687
```

## PingCastle

Comprehensive Active Directory security assessment.

```bash
./PingCastle.exe --healthcheck --server 10.0.2.15
```

Assesses: Password policies, Privileged accounts, Trust relationships, SMB/RDP security, Kerberos, ACLs, Delegation abuse
