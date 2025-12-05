
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

# ## 2. Caputured Banner

```bash
nc 192.168.56.102 21    # FTP        220 (vsFTPd 2.3.4)
nc 192.168.56.102 22    # SSH        SSH-2.0-OpenSSH_4.7p1 Debian-8ubuntu1 
nc 192.168.56.102 23    # Telnet     ��▒�� ��#��'

```

# ## 3. What to look for

### 🔥 **Service version numbers**
- vsFTPd 2.3.4
- OpenSSH 4.7p1  

### ⚠️ **Weak / Outdated Services**
- Apache 2.2.8  
- BIND 9.4.2  
- MySQL 5.0.51a  
- PostgreSQL 8.3  
- Telnet (cleartext)  
- RSH services (512, 513, 514)  

---

