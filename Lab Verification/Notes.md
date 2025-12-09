
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

## Output
    1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
        link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
        valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
    2: wlan0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
        link/ether f4:d1:08:05:09:38 brd ff:ff:ff:ff:ff:ff
    inet 10.66.221.19/24 brd 10.66.221.255 scope global dynamic noprefixroute wlan0
       valid_lft 3339sec preferred_lft 3339sec
    inet6 2409:40f4:a1:e1ba:bed8:6adb:c555:c494/64 scope global temporary dynamic 
       valid_lft 6942sec preferred_lft 6942sec
    inet6 2409:40f4:a1:e1ba:f6d1:8ff:fe05:938/64 scope global dynamic mngtmpaddr noprefixroute 
       valid_lft 6942sec preferred_lft 6942sec
    inet6 fe80::f6d1:8ff:fe05:938/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
    3: vboxnet0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
       link/ether 0a:00:27:00:00:00 brd ff:ff:ff:ff:ff:ff
    inet 192.168.56.1/24 brd 192.168.56.255 scope global vboxnet0
       valid_lft forever preferred_lft forever
    inet6 fe80::800:27ff:fe00:0/64 scope link proto kernel_ll 
       valid_lft forever preferred_lft forever

## Findings
- Kali's Host-Only Adapter (vboxnet0) is using IP: 192.168.56.1/24
- This confirms that Metasploitable 2 should fall within the same subnet: 192.168.56.0/24
- Wireless interface (wlan0) is unrelated to the lab network.

## Interpretation
- ✔ Kali Linux is correctly connected to a VirtualBox Host-Only network.
- ✔ Metasploitable will also receive an IP from the same 192.168.56.x range.


