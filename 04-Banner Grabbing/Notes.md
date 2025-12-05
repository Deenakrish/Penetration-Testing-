
# ##03 – Banner Grabbing (-sV)

---

## 🛠 Tool  
**Nmap**

## 🎯 Technique  
Service & Version Detection

## 🖥 Target  
**192.168.56.102 (Metasploitable 2)**

## 📌 Command Used

```bash
nc 192.168.56.102 21    # FTP
nc 192.168.56.102 22    # SSH
nc 192.168.56.102 23    # Telnet

```

---

# ## 1. Host Status

**Host is up (0.00036s latency)**  
**MAC Address:** 08:00:27:F0:BB:3D (Oracle VirtualBox virtual NIC)

### 🔎 Interpretation
- Target is reachable with very low latency → same local network  
- MAC vendor confirms VirtualBox → expected for Metasploitable 2  

---

# ## 2. Banner captured

Nmap found **23 open ports**, including several **high‑value vulnerable services**.

| Port | Service | Version / Info | Notes |
|------|---------|----------------|-------|
| 21/tcp | ftp | vsftpd 2.3.4 | Known backdoor vulnerability |
| 22/tcp | ssh | OpenSSH 4.7p1 | Outdated, weak defaults |
| 23/tcp | telnet | Linux telnetd | Cleartext credentials |
| 25/tcp | smtp | Postfix smtpd | Mail server, relay checks later |
| 53/tcp | dns | BIND 9.4.2 | Old DNS server |
| 80/tcp | http | Apache 2.2.8 | Outdated, likely directory issues |
| 111/tcp | rpcbind | RPC service | Useful for NFS enumeration |
| 139/tcp | netbios-ssn | Samba 3.x–4.x | SMB enumeration possible |
| 445/tcp | netbios-ssn | Samba 3.x–4.x | SMB vulnerabilities common |
| 512/tcp | exec | netkit-rsh | Legacy remote execution |
| 513/tcp | login | — | Remote login service |
| 514/tcp | shell | rshd | No encryption, risky |
| 1099/tcp | java-rmi | GNU Classpath | RMI exploit possible |
| 1524/tcp | bindshell | Metasploitable root shell | Intentional backdoor |
| 2049/tcp | nfs | NFS v2–4 | Exported shares expected |
| 2121/tcp | ftp | ProFTPD 1.3.1 | Vulnerable version |
| 3306/tcp | mysql | MySQL 5.0 | Weak defaults likely |
| 5432/tcp | postgresql | PostgreSQL 8.3.x | Outdated |
| 5900/tcp | vnc | VNC protocol 3.3 | No encryption |
| 6000/tcp | X11 | Access denied | Still exposes X11 service |
| 6667/tcp | irc | UnrealIRCd | Famous backdoor vulnerability |
| 8009/tcp | ajp13 | Apache JServ | Used in Tomcat exploitation |
| 8180/tcp | http | Apache Tomcat/Coyote JSP 1.1 | Tomcat Manager exploitation possible |

---

# ## 3. Captured Banner

**:**  
-   
- irc.Metasploitable.LAN  

**OS:**  
- Unix / Linux  

### 🔎 Interpretation
- Confirms target is a Linux‑based machine  
- Hostnames reveal IRC + Apache services  
- Services match known Metasploitable vulnerabilities  

---

# ## 4. Key Findings

### 🔥 **High‑Risk Services Identified**
- vsftpd 2.3.4 → Backdoor exploit  
- UnrealIRCd → Remote command execution  
- Tomcat 8180 → Weak credentials + WAR deployment  
- NFS 2049 → Anonymous mounts  
- Samba 445/139 → SMB exploitation  
- ProFTPD 2121 → Remote exploit  

### ⚠️ **Weak / Outdated Services**
- Apache 2.2.8  
- BIND 9.4.2  
- MySQL 5.0.51a  
- PostgreSQL 8.3  
- Telnet (cleartext)  
- RSH services (512, 513, 514)  

---

