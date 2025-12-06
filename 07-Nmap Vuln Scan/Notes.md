
# ##05 – Nmap Vuln Scan

---

## 🛠 Tool  
**Nmap.**

## 🎯 Technique  
SMB Enumeration & Recon

## 🖥 Target  
**192.168.56.102 (Metasploitable 2)**

## 📌 Command Used 
    sudo nmap --script vuln 192.168.56.102

[sudo] password for lucifer:
Starting Nmap 7.95 ( https://nmap.org ) at 2025-12-05 22:22 IST
Nmap scan report for 192.168.56.102
Host is up (0.00016s latency).
Not shown: 977 closed tcp ports (reset)

PORT     STATE SERVICE
21/tcp   open  ftp
| ftp-vsftpd-backdoor:
|   VULNERABLE:
|   vsFTPd version 2.3.4 backdoor
|   State: VULNERABLE (Exploitable)
|   IDs: BID:48539 CVE:CVE-2011-2523
|   vsFTPd version 2.3.4 backdoor, reported on 2011-07-04.
|   Disclosure date: 2011-07-03
|   Exploit results:
|     Shell command: id
|     Results: uid=0(root) gid=0(root)
|   References:
|     https://www.securityfocus.com/bid/48539
|     https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2011-2523
|     http://scarybeastsecurity.blogspot.com/2011/07/alert-vsftpd-download-backdoored.html
|     https://github.com/rapid7/metasploit-framework/blob/master/modules/exploits/unix/ftp/vsftpd_234_backdoor.rb

22/tcp   open  ssh
23/tcp   open  telnet
25/tcp   open  smtp
|_sslv2-drown: ERROR: Script execution failed (use -d to debug)

| ssl-dh-params:
|   VULNERABLE: Anonymous Diffie-Hellman Key Exchange MitM Vulnerability
|   State: VULNERABLE
|   Transport Layer Security (TLS) services using anonymous Diffie-Hellman key exchange
|   are vulnerable to active man-in-the-middle attacks.
|   Check results:
|     ANONYMOUS DH GROUP 1
|     Cipher Suite: TLS_DH_anon_EXPORT_WITH_DES40_CBC_SHA
|     Modulus Length: 512
|   References:
|     https://www.ietf.org/rfc/rfc2246.txt

| Transport Layer Security (TLS) Protocol DHE_EXPORT Ciphers Downgrade MitM (Logjam)
|   State: VULNERABLE
|   IDs: BID:74733 CVE:CVE-2015-4000
|   The TLS protocol contains a flaw triggered with DHE_EXPORT ciphers.
|   Check results:
|     EXPORT-GRADE DH GROUP 1
|     Cipher Suite: TLS_DHE_RSA_EXPORT_WITH_DES40_CBC_SHA
|     Modulus Length: 512
|   References:
|     https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-4000
|     https://www.securityfocus.com/bid/74733
|     https://weakdh.org

| Diffie-Hellman Key Exchange Insufficient Group Strength
|   State: VULNERABLE
|   Check results:
|     WEAK DH GROUP 1
|     Cipher Suite: TLS_DHE_RSA_WITH_AES_128_CBC_SHA
|     Modulus Length: 1024
|   References:
|     https://weakdh.org

| smtp-vuln-cve2010-4344:
|   The SMTP server is not Exim: NOT VULNERABLE

| ssl-poodle:
|   VULNERABLE: SSL POODLE information leak
|   State: VULNERABLE
|   IDs: BID:70574 CVE:CVE-2014-3566
|   Check results:
|     TLS_RSA_WITH_AES_128_CBC_SHA
|   References:
|     https://www.securityfocus.com/bid/70574
|     https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-3566
|     https://www.openssl.org/~bodo/ssl-poodle.pdf
|     https://www.imperialviolet.org/2014/10/14/poodle.html

53/tcp   open  domain
80/tcp   open  http
|_http-trace: TRACE is enabled

| http-sql-injection:
|   Possible SQLi for queries:
|     http://192.168.56.102:80/dav/?C=N%3BO%3DD' OR sqlspider
|     http://192.168.56.102:80/mutillidae/index.php?page=set-background-color.php' OR sqlspider
|     http://192.168.56.102:80/mutillidae/index.php?page=view-someones-blog.php' OR sqlspider
|     (many other similar URLs detected)
