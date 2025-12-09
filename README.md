# 🛰️ Reconnaissance Phase – README  
The Reconnaissance phase is the **first and most crucial stage** in a penetration test.  
Its purpose is to **collect information** about the target **without interacting with it too aggressively** (passive) and then **confirm and enumerate the target’s presence** (active).

This README covers all tasks performed in **Recon Phase** of your Metasploitable 2 lab.

---

# 📌 Objectives of Reconnaissance
- Identify the target’s network range  
- Gather public or non-intrusive information  
- Discover live hosts  
- Validate the lab environment  
- Map the attack surface before scanning ports or services  

Recon is divided into:

1. **Passive Reconnaissance** – No direct interaction with target  
2. **Active Reconnaissance** – Direct interaction to confirm host availability  

---

# 🧩 Reconnaissance Structure
This phase includes the following steps:

### **1. Lab Environment Verification**
- Confirm Kali + Metasploitable are connected in Host-Only or Internal network
- Verify VM IP address
- Ensure no external internet exposure

### **2. Passive Recon**
Performed *without sending direct packets*.

Includes:
- **WHOIS lookup**  
- **DNS Lookup / Reverse Lookup**
- Understanding architecture & default services of Metasploitable 2

### **3. Network Discovery (Passive + Semi-passive)**
- ARP monitoring  
- Network sweep using Bash one-liner ping loop

### **4. Active Recon**
- Host discovery using `nmap -sn`
- Confirming the target host is up

---

# 🛠 Tools Used in Recon Phase
| Tool | Purpose | Type |
|------|---------|------|
| **WHOIS** | Check public ownership of IP ranges | Passive |
| **nslookup / dig** | DNS lookup / reverse lookup | Passive |
| **arp-scan / ARP capture** | Identify hosts in local subnet | Passive/Semi-active |
| **ping sweep** | Identify live hosts | Active |
| **Nmap -sn** | Host discovery (no port scan) | Active |

---

# 📂 Steps Included in Recon README

---

## **STEP 1 – Lab Verification**
Purpose: Ensure Metasploitable is running in a safe isolated network.

Includes:
- Identifying network range  
- Confirming VM bridging/host-only  
- Basic understanding of vulnerable VM architecture  

**Why:**  
To ensure the test is done safely in a controlled lab environment.

---

## **STEP 2 – Passive Recon (WHOIS + DNS Enumeration)**

### **Why Used**
To identify:
- Ownership of IP  
- Type of IP (private/public)  
- DNS records or PTR records  
- Validate that the target is within a local lab environment  

---

## **STEP 3 – Host Discovery (Passive/Semi-Passive)**

- ARP capture to detect active local hosts  
- Bash ping sweep to identify live hosts in the subnet  

**Why:**  
To know which machines are active in the target network before scanning ports.

---

## **STEP 4 – Active Recon using Nmap Ping Scan**

`nmap -sn <target>` directly checks if a host is reachable.

**Why:**  
To confirm the target VM is up before moving into Port Scanning (next phase).

---

# 📌 Recon Phase Summary

| Step | Description | Status |
|------|-------------|--------|
| Step 1 | Lab Environment + IP Verification | ✔ Completed |
| Step 2 | Passive Recon (WHOIS, DNS lookup) | ✔ Completed |
| Step 3 | Network Discovery (ARP + Ping Sweep) | ✔ Completed |
| Step 4 | Active Recon (Nmap Ping Scan) | ✔ Completed |

At the end of Reconnaissance, you now know:

- The target IP is **192.168.56.102**  
- The host is **Alive**  
- It runs on a **VirtualBox NIC**  
- Network has **3 active hosts**  
- It belongs to a **private IP range**  
- No DNS PTR records exist  
- Metasploitable is correctly configured  

---

# 🚀 Next Phase
After completing Reconnaissance, move to:

# **Phase 2 – Vulnerability Scanning & Enumeration**
(Nmap port scan → version scan → script scan → enumeration)

---

# Scanning & Enumeration Phase

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
