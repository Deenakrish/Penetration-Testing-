# Reconnaissance Phase

This branch contains all reconnaissance tasks performed against Metasploitable 2 using Kali Linux.

## Objective
To identify:
- Active hosts
- Open ports
- Running services and versions
- Web server configurations
- SMB information
- Potential vulnerabilities

## Tests Performed
| # | Test | Tool | Status |
|---|------|------|--------|
| 01 | Service Detection Scan | nmap -sV | ✓ Completed |
| 02 | Aggressive Scan | nmap -A | ✓ Completed |
| 03 | Banner Grabbing | netcat | ✓ Completed |
| 04 | Web Scan | nikto | ✓ Completed |
| 05 | SMB Enumeration | enum4linux | ✓ Completed |
| 06 | Vuln Script Scan | nmap --script vuln | ✓ Completed |

Each test has its own folder with:
- Notes
- Screenshots
- Commands
- Findings
