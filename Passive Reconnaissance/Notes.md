
# Phase 2 – Passive Reconnaissance  
## 2.1 WHOIS & DNS Enumeration

Passive reconnaissance helps gather information **without directly interacting with the target system**.  
Even though Metasploitable 2 is a **local machine**, WHOIS & DNS checks are still documented to show reconnaissance methodology.

---

## 🛠 Tool 1: `whois`  
### **Purpose**
- Identify IP ownership  
- Check whether the target is public or private  
- Understand allocated IP ranges  

Since Metasploitable 2 uses a **private IP (192.168.x.x)**, WHOIS reveals IANA private address space information.

---

### **Command**
    whois 192.168.56.102

## Output

    NetRange:       192.168.0.0 - 192.168.255.255
    CIDR:           192.168.0.0/16
    NetName:        PRIVATE-ADDRESS-CBLK-RFC1918-IANA-RESERVED
    NetType:        IANA Special Use
    Organization:   Internet Assigned Numbers Authority (IANA)
    Comment: These addresses are used in private networks by millions of devices✔ Safe to continue reconnaissance without internet exposure.
             and cannot be routed on the public Internet.

## Findings
- The IP belongs to RFC 1918 Private Address Space.
- It is not a public server but an isolated lab machine.
- Traffic does NOT leave the internal network.

## Interpretation
- ✔ Confirms our target (Metasploitable 2) is inside a private virtual network.
- ✔ Safe to continue reconnaissance without internet exposure.

---

## 🛠 Tool 2: nslookup 
### **Purpose**
- Query DNS records
- Check whether the target has any hostname associated

---

### **Command**
    nslookup 192.168.56.102

## Output

    ** server can't find 102.56.168.192.in-addr.arpa: NXDOMAIN

## Findings
- No PTR (reverse DNS) record exists.
- Expected in local/isolated lab networks.

## Interpretation
- ✔ No DNS hostname assigned — normal for Metasploitable.

---

## 🛠 Tool 3: dig -x (Reverse DNS Lookup)
### **Purpose**
- Verify DNS reverse lookup
- Check if any DNS server inside the network has mappings

---

### **Command**
    dig -x 192.168.56.102

## Output

    ;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN
    ;; ANSWER: 0, AUTHORITY: 0

## Findings
- Reverse DNS does not exist.
- Confirms this is an unmanaged private VM, not an enterprise environment.

## Interpretation
- ✔ No DNS information leaked.
- ✔ Typical for private lab targets.

---

## 📌 Metasploitable 2 – Default Services Overview

Metasploitable 2 is an intentionally vulnerable Linux VM designed for penetration testing practice.
It automatically runs several outdated, misconfigured, and vulnerable services.

---

## Key Default Services

- 1. FTP – vsftpd 2.3.4
     - Contains a backdoor vulnerability
     - Allows remote code execution
- 2. SSH – OpenSSH 4.7p1
     - Outdated and vulnerable
     - Useful for brute-force or exploit practice
- 3. Telnet
     - Enabled by default
     - Sends credentials in plaintext
- 4. Samba (SMB) – Samba 3.0.20
     - Misconfigured anonymous shares
     - Vulnerable to usermap_script exploit
- 5. HTTP – Apache 2.2.8
  Hosts several intentionally vulnerable web apps:
     - Damn Vulnerable Web Application (DVWA)
     - Mutillidae
     - phpMyAdmin
     - Tiki Wiki CMS
- 6. Databases
     - PostgreSQL (default creds: postgres:postgres)
     - MySQL (root user with empty password)
- 7. VNC
     - Weak password: password
- 8. IRC – UnrealIRCd 3.2.8.1
     - Contains a known backdoor
     - Contains a known backdoor
- 9. DistCC Service
      - Remote command execution vulnerability
---





