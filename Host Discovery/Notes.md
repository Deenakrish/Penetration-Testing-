
# Phase 3 – Semi-Passive Recon
## 3.1 ARP Scanning & Live Host Discovery

Network discovery helps identify **active hosts** inside the local subnet before any detailed scanning begins.  
This phase uses **ARP-based** and **ICMP-based** host detection.

---

# 🛠 Tool 1: `netdiscover`
### **Purpose**
- Passive & active ARP scanning  
- Quickly enumerate live hosts on the LAN  
- Detect devices even if they block ICMP/ping  

---

## **Command**
    netdiscover

## Output

Currently scanning: Finished!   |   Screen View: Unique Hosts

3 Captured ARP Req/Rep packets, from 1 hosts. Total size: 126
_____________________________________________________________________________
   IP               At MAC Address        Count     Len     MAC Vendor / Hostname
-----------------------------------------------------------------------------
 10.66.221.98       a6:cf:87:05:68:68        3      126     Unknown vendor

## Findings 

- Only one active host was detected in this ARP scan: 10.66.221.98.
- The MAC vendor could not be identified.
- This network appears to be a NAT or different interface network.

## Imterpretation 

- ✔ ARP scanning works only on the local broadcast domain.
- ✔ The system detected only 1 device on that particular interface.
- ✔ For our Metasploitable network (192.168.56.0/24), we must use ICMP sweep next.

---

# 🛠 Tool 2: Bash ICMP Sweep
### **Purpose**
- Identify live hosts inside a specific subnet
- Quick and effective for internal lab networks
- Helps verify the presence of Metasploitable 2 and other VMs

---
## **Command**
    for i in {1..254}; do ping -c 1 192.168.56.$i | grep "64 bytes"; done

## Output

    64 bytes from 192.168.56.1: icmp_seq=1 ttl=64 time=0.019 ms
    64 bytes from 192.168.56.100: icmp_seq=1 ttl=255 time=0.287 ms
    64 bytes from 192.168.56.102: icmp_seq=1 ttl=64 time=0.870 ms

## Findings 

Three Live Hosts Responded:


