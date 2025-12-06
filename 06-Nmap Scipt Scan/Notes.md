
# ##06 – Nmap Script Scan

---

## 🛠 Tool  
**Nmap-Network Discovery Tool.**

## 🎯 Technique  
Default & Custom Script Scan (Nmap Scripting Engine)

## 🖥 Target  
**192.168.56.102 (Metasploitable 2)**

## 📌 Command Used 
    sudo nmap --script vuln 192.168.56.102

## 🖥 Output  

- Starting Nmap 7.95 ( https://nmap.org ) at 2025-12-05 22:22 IST
- Nmap scan report for 192.168.56.102
- Host is up (0.00016s latency).
- Not shown: 977 closed tcp ports (reset)

      PORT     STATE SERVICE
      21/tcp   open  ftp

- | ftp-vsftpd-backdoor:
- |   VULNERABLE:
- |   vsFTPd version 2.3.4 backdoor
- |   State: VULNERABLE (Exploitable)
- |   IDs: BID:48539 CVE:CVE-2011-2523
- |   vsFTPd version 2.3.4 backdoor, reported on 2011-07-04.
- |   Disclosure date: 2011-07-03
- |   Exploit results:
- |     Shell command: id
- |     Results: uid=0(root) gid=0(root)
- |   References:
- |     https://www.securityfocus.com/bid/48539
- |     https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2011-2523
- |     http://scarybeastsecurity.blogspot.com/2011/07/alert-vsftpd-download-backdoored.html
- |     https://github.com/rapid7/metasploit-framework/blob/master/modules/exploits/unix/ftp/vsftpd_234_backdoor.rb

      22/tcp   open  ssh
      23/tcp   open  telnet
      25/tcp   open  smtp
- |_sslv2-drown: ERROR: Script execution failed (use -d to debug)

- | ssl-dh-params:
- |   VULNERABLE: Anonymous Diffie-Hellman Key Exchange MitM Vulnerability
- |   State: VULNERABLE
- |   Transport Layer Security (TLS) services using anonymous Diffie-Hellman key exchange
- |   are vulnerable to active man-in-the-middle attacks.
- |   Check results:
- |     ANONYMOUS DH GROUP 1
- |     Cipher Suite: TLS_DH_anon_EXPORT_WITH_DES40_CBC_SHA
- |     Modulus Length: 512
- |   References:
- |     https://www.ietf.org/rfc/rfc2246.txt

- | Transport Layer Security (TLS) Protocol DHE_EXPORT Ciphers Downgrade MitM (Logjam)
- |   State: VULNERABLE
- |   IDs: BID:74733 CVE:CVE-2015-4000
- |   The TLS protocol contains a flaw triggered with DHE_EXPORT ciphers.
- |   Check results:
- |     EXPORT-GRADE DH GROUP 1
- |     Cipher Suite: TLS_DHE_RSA_EXPORT_WITH_DES40_CBC_SHA
- |     Modulus Length: 512
- |   References:
- |     https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-4000
- |     https://www.securityfocus.com/bid/74733
- |     https://weakdh.org

- | Diffie-Hellman Key Exchange Insufficient Group Strength
- |   State: VULNERABLE
- |   Check results:
- |     WEAK DH GROUP 1
- |     Cipher Suite: TLS_DHE_RSA_WITH_AES_128_CBC_SHA
- |     Modulus Length: 1024
- |   References:
- |     https://weakdh.org

- | smtp-vuln-cve2010-4344:
- |   The SMTP server is not Exim: NOT VULNERABLE

- | ssl-poodle:
- |   VULNERABLE: SSL POODLE information leak
- |   State: VULNERABLE
- |   IDs: BID:70574 CVE:CVE-2014-3566
- |   Check results:
- |     TLS_RSA_WITH_AES_128_CBC_SHA
- |   References:
- |     https://www.securityfocus.com/bid/70574
- |     https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-3566
- |     https://www.openssl.org/~bodo/ssl-poodle.pdf
- |     https://www.imperialviolet.org/2014/10/14/poodle.html

      53/tcp   open  domain
      80/tcp   open  http
- |_http-trace: TRACE is enabled

- | http-sql-injection:
- |   Possible SQLi for queries:
- |     http://192.168.56.102:80/dav/?C=N%3BO%3DD' OR sqlspider
- |     http://192.168.56.102:80/mutillidae/index.php?page=set-background-color.php' OR sqlspider
- |     http://192.168.56.102:80/mutillidae/index.php?page=view-someones-blog.php' OR sqlspider
- |     (many other similar URLs detected)

# ## 1. Open Ports And Services

- 21/tcp – FTP
   - Service: vsFTPd 2.3.4
   - Vulnerability: vsFTPd backdoor
       - Exploitable (allows remote shell access)
       - Reference: CVE-2011-2523
       - Exploit result: uid=0(root) gid=0(root) (indicates root shell access possible)
- 22/tcp – SSH
- 23/tcp – Telnet
- 25/tcp – SMTP
    - Some TLS vulnerabilities detected (DROWN, weak Diffie-Hellman)
- 53/tcp – DNS
- 80/tcp – HTTP
    - Several web vulnerabilities detected:
         - TRACE enabled (http-trace)
         -  Multiple potential SQL injection points (http-sql-injection) on Mutillidae pages
         -  Multiple arbitrary file inclusion vectors (arbitrary-file-inclusion.php)

# ## 2. Critical Vulnerabilities Detected

- vsFTPd 2.3.4 backdoor
   - Critical because it allows remote root access.
   - Exploitable via the vsFTPd backdoor exploit.
- TLS/SSL vulnerabilities
   - DROWN / SSLv2: Can allow decryption of TLS sessions.
   - Weak DH groups / Logjam: Man-in-the-middle attack possible, weak cryptography.
   - POODLE (SSL 3.0): Padding oracle vulnerability, allows potential decryption of sensitive data.
- Web vulnerabilities on HTTP (Mutillidae)
   - SQL Injection: Multiple potential injection points.
   - Arbitrary File Inclusion: Could allow remote code execution.
   - HTTP TRACE enabled: Potentially allows Cross-Site Tracing attacks.

---
# ## 3. Observations

- The system is intentionally vulnerable (probably a vulnerable lab setup, like Mutillidae or Metasploitable VM).
- The vsFTPd 2.3.4 backdoor is extremely high-risk.
- TLS vulnerabilities indicate weak or outdated cryptography.
- Web vulnerabilities (SQLi, arbitrary file inclusion) suggest the web app is not properly secured.

---
# ## 4. Next Steps / Recommendations

- High-Risk Issues (Immediate attention)
   - vsFTPd backdoor: disable/remove vsFTPd 2.3.4, upgrade to a secure version.
   - SSL/TLS: disable SSLv2/SSLv3, enforce strong DH groups, and update OpenSSL.
- Web Vulnerabilities
   - Test SQLi points in a safe, lab environment.
   - Review web app code for input sanitization (Mutillidae is intentionally vulnerable, so these are expected in the lab).
- Lab Context
   - If this is for training (Metasploitable/Mutillidae), your findings are normal.
   - If this is a production system, all detected vulnerabilities are critical and must be remediated.

---
