
# Phase 1 – Lab Verification

Before starting reconnaissance or vulnerability assessment, it is essential to verify that the **Kali Linux attacker machine** and **Metasploitable 2 target machine** are correctly configured and reachable in the same network.  
This phase ensures correct IP configuration, routing, and ARP table entries.

---

## 1. IP Address Verification – Using `ip a`

### **Why This Tool Is Used**
The `ip a` command is used to check:
- Active network interfaces  
- Assigned IP addresses  
- Host-Only network configuration  
- Whether Kali and Metasploitable can communicate  

This confirms the network setup before running any scans.

---

### **Command**

    ip a

