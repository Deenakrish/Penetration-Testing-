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
| 01 | Network Discovery | netdiscover | ✓ Completed |
| 02 | Basic Port Scan | nmap | ✓ Completed |
| 03 | Aggressive Scan | nmap -A | ✓ Completed |
| 04 | Banner Grabbing | netcat | ✓ Completed |
| 05 | Web Scan | nikto | ✓ Completed |
| 06 | SMB Enumeration | enum4linux | ✓ Completed |
| 07 | Vuln Script Scan | nmap --script vuln | ✓ Completed |

Each test has its own folder with:
- Notes
- Screenshots
- Commands
- Findings
