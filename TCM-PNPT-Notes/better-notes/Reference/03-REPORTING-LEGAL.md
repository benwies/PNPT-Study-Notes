# REPORTING & LEGAL

## During Engagement

### Documentation
- **Take Screenshots** - Every finding with proof
- **Note Timestamps** - When actions were taken
- **Save Command Output** - tee, > redirection
- **Keep Organized** - By target/finding type

### Careful Recording
```bash
# Record terminal session
$ script session.log
# ... run commands ...
$ exit

# Copy output to file
$ command | tee output.txt

# Screenshot on Linux
$ scrot screenshot.png
$ import screenshot.png  # with selection
```

## Scope & Authorization

### Before Engagement
- ✓ Written authorization required
- ✓ Define scope clearly (IPs, domains, systems)
- ✓ Know legal testing window (dates/times)
- ✓ Contact person for issues
- ✓ Get signed scope document

### Prohibited Activities (typically)
- Social engineering without approval
- Physical penetration
- DoS/DDoS attacks
- Accessing/modifying production data
- Using found credentials on other systems
- Public disclosure of findings

## Reporting

### Structure
1. **Executive Summary** - High level findings
2. **Findings** - Each vulnerability with:
   - Description
   - Severity (Critical/High/Medium/Low)
   - Proof (screenshot, output)
   - Impact
   - Recommendation
3. **Methodology** - What tests were run
4. **Conclusion** - Overall security posture

### Severity Ratings
- **Critical:** Immediate exploitation, full access
- **High:** Easy exploitation, major impact
- **Medium:** Moderate difficulty, some impact
- **Low:** Difficult exploitation, minor impact
- **Info:** Non-exploitable, useful info

## Professional Conduct
- No data theft (stick to scope)
- No disruption of services
- Clean up after yourself (backdoors, files)
- Maintain confidentiality
- No unauthorized system access
- Report findings to client immediately

