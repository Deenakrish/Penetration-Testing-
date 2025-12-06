
# ## 04 – HTTP Reconnaissance (Nikto Scan)

---

## 🛠 Tool  
**Nikto** – popular and in-demand web server vulnerability scanner.

## 🎯 Technique  
HTTP enumeration & vulnerability detection on port **80**.

## 🖥 Target  
**http://192.168.56.102 (Metasploitable 2)**

## 📌 Command Used

    nikto -h http://192.168.56.102

## 🖥 Output  

- Nikto v2.5.0
---------------------------------------------------------------------------
+ Target IP:          192.168.56.102
+ Target Hostname:    192.168.56.102
+ Target Port:        80
+ Start Time:         2025-12-05 22:16:46 (GMT5.5)
---------------------------------------------------------------------------
+ Server: Apache/2.2.8 (Ubuntu) DAV/2
+ /: Retrieved x-powered-by header: PHP/5.2.4-2ubuntu5.10.
+ /: The anti-clickjacking X-Frame-Options header is not present.
+ /: The X-Content-Type-Options header is not set.
+ Apache/2.2.8 appears to be outdated (current is at least Apache/2.4.54).
+ /index: Uncommon header 'tcn' found.
+ /index: Apache mod_negotiation is enabled with MultiViews; attackers can brute-force filenames.
+ /: Web server responds to junk HTTP methods (possible false positives).
+ /: HTTP TRACE method is active → vulnerable to XST.
+ /phpinfo.php: Output from phpinfo() found.
+ /doc/: Directory indexing found.
+ /doc/: Directory is browsable (possibly /usr/doc).
+ /?=PHPB8B5F2A0-3C92-11d3-A3A9-4C7B08C10000: PHP reveals sensitive info (OSVDB-12184)
+ /?=PHPE9568F36-D428-11d2-A769-00AA001ACF42: Sensitive PHP info leak.
+ /?=PHPE9568F34-D428-11d2-A769-00AA001ACF42: Sensitive PHP info leak.
+ /?=PHPE9568F35-D428-11d2-A769-00AA001ACF42: Sensitive PHP info leak.
+ /phpMyAdmin/changelog.php: phpMyAdmin exposed – should be restricted.
+ /phpMyAdmin/ChangeLog: ETag inode leak (CVE-2003-1418).
+ /test/: Directory indexing found.
+ /test/: This directory may be interesting.
+ /phpinfo.php: Reveals system info (CWE-552).
+ /icons/: Directory indexing found.
+ /icons/README: Apache default file exposed.
+ /phpMyAdmin/: phpMyAdmin directory found (high risk).
+ /phpMyAdmin/Documentation.html: phpMyAdmin not secured.
+ /phpMyAdmin/README: phpMyAdmin not secured.
+ /#wp-config.php#: Sensitive WordPress config file exposed.
+ 8910 requests: 0 error(s), 27 item(s) reported.
+ End Time:           2025-12-05 22:17:03 (GMT5.5) (17 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested

# ## Key Findings

### 🔥 High-Risk Vulnerabilities
- **phpinfo.php exposed** → reveals system internals
- **phpMyAdmin directory exposed** → critical attack surface 
- **wp-config.php backup file found** → contains credentials
- **HTTP TRACE enabled** → vulnerable to Cross-Site Tracing (XST)
- **Directory indexing enabled** → in /doc/, /icons/, /test/

### ⚠️ Outdated Software
- **Apache 2.2.8** → extremely outdated, EOL
- **PHP 5.2.4** → end-of-life, vulnerable

### 🟡 Missing Security Headers
- **X-Frame-Options** → Clickjacking protection  
- **X-Content-Type-Options** → MIME-type sniffing prevention 
