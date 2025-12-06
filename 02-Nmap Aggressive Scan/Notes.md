
# ##02 – Nmap Aggressive Scan (+ OS Detection)

---

## 🛠 Tool  
**Nmap**

## 🎯 Technique  
Aggressive Scan (Version Detection + OS Detection + Script Scan)

## 🖥 Target  
**192.168.56.102 (Metasploitable 2)**

## 📌 Command Used
```bash
sudo nmap -A 192.168.56.102
```

---

# ## 1. Host Status

**Host is up (0.00048s latency)**  
**MAC Address:** 08:00:27:F0:BB:3D (Oracle VirtualBox / PCS Systemtechnik)

### 🔎 Interpretation
- Extremely low latency → same local network  
- MAC vendor indicates VirtualBox → expected for Metasploitable 2  

---

# ## 2. Ports & Services Identified (Aggressive Scan Result)

This scan revealed **all major services** running on Metasploitable 2.

| Port | Service | Version / Info | Script Results / Notes |
|------|---------|----------------|------------------------|
| 21/tcp | ftp | vsftpd 2.3.4 | Anonymous login allowed |
| 22/tcp | ssh | OpenSSH 4.7p1 | SSH host keys shown |
| 23/tcp | telnet | Linux telnetd | Cleartext login |
| 25/tcp | smtp | Postfix smtpd | SSLv2 enabled, weak cert |
| 53/tcp | domain | ISC BIND 9.4.2 | Version disclosed via dns-nsid |
| 80/tcp | http | Apache 2.2.8 (Ubuntu) | Web homepage accessible |
| 111/tcp | rpcbind | RPC #100000 | NFS services discovered |
| 139/tcp | netbios-ssn | Samba 3.X–4.X | Workgroup: WORKGROUP |
| 445/tcp | netbios-ssn | Samba 3.0.20-Debian | Vulnerable version |
| 512/tcp | exec | netkit-rsh | Legacy RSH |
| 513/tcp | login | — | Remote login service |
| 514/tcp | shell | rshd | No encryption |
| 1099/tcp | java-rmi | GNU Classpath | RMI registry open |
| 1524/tcp | bindshell | Metasploitable root shell | Intentional backdoor |
| 2049/tcp | nfs | v2–4 | NFS mounts exposed |
| 2121/tcp | ftp | ProFTPD 1.3.1 | Known vulnerabilities |
| 3306/tcp | mysql | MySQL 5.0.51a | Version disclosure + salt |
| 5432/tcp | postgresql | PostgreSQL 8.3.x | Weak SSL certificate |
| 5900/tcp | vnc | VNC protocol 3.3 | No encrypted auth |
| 6000/tcp | X11 | Access Denied | Still exposed |
| 6667/tcp | irc | UnrealIRCd | Backdoored version |
| 8009/tcp | ajp13 | Apache JServ | Tomcat exploitation possible |
| 8180/tcp | http | Apache Tomcat 5.5 | Manager interface available |

---

# ## 3. OS Detection

**Detected OS:**  
**Linux Kernel 2.6.9 – 2.6.33**  
(CPE: cpe:/o:linux:linux_kernel:2.6)

### 🔎 Interpretation
- Matches known Metasploitable 2 kernel range  
- Classified as **general-purpose Linux system**  
- Network Distance: **1 hop** → same LAN  

---

# ## 4. Host Script Results

### ✔ smb-os-discovery
- OS: Unix (Samba 3.0.20-Debian)  
- FQDN: metasploitable.localdomain  
- Message signing: **disabled** (dangerous)

### ✔ rpcinfo
- NFS, mountd, status services exposed  
- Useful for later **NFS enumeration**

### ✔ smtp sslv2 & certificate checks
- SSLv2 enabled → **very weak**  
- Certificate expired (2010)  
- Common in old systems

### ✔ nbstat
- NetBIOS name: METASPLOITABLE  

### ✔ clock-skew
- Large deviation → typical for test VMs  

---

# ## 5. Traceroute

```
HOP  RTT     ADDRESS
1    0.48ms  192.168.56.102
```

### Interpretation
- Directly reachable  
- Confirms virtualization lab environment  

---

# ## 6. Key Findings

### 🔥 High-Risk Services
- **vsftpd 2.3.4** → Known backdoor  
- **UnrealIRCd** → Remote command execution  
- **ProFTPD 1.3.1** → Remote exploit  
- **Tomcat 8180** → WAR deploy exploit  
- **Samba 3.0.20** → Multiple critical vulnerabilities  
- **NFS** → Anonymous mount possible  
- **1524/tcp bindshell** → Direct root access backdoor  

### ⚠️ Outdated / Weak Services
- Apache 2.2.8  
- BIND 9.4.2  
- MySQL 5.0  
- PostgreSQL 8.3  
- Telnet  
- RSH services  

---

# ## 7. What to Check / Analyze
- OS detection accuracy (Linux 2.6)  
- Version disclosure → exploitability  
- Weak encryption (SSLv2, plaintext protocols)  
- Services known for Metasploitable:  
  - FTP  
  - SSH  
  - Telnet  
  - Apache  
  - MySQL  
  - RPC  
  - Samba  

---

