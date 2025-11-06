Wireshark 

📘 *This lab is for educational and ethical testing only, performed on my own isolated network.*

# 🧠 Wireshark Network Analysis – SOC Practice Lab

## 📌 Overview
This repository documents my Wireshark packet analysis practice performed in my isolated home SOC lab.  
The goal is to learn how to detect malicious or abnormal network behavior using packet captures (pcaps) generated during lab exercises with Kali Linux, Raspberry Pi, and Proxmox servers.


## 🔹 Capture 1 — TCP SYN Scan (Port Scanning Phase)

File: scan-test
Filter: tcp.flag.syn == 1 && tcp.flag.ack == 0

# 🧠 Wireshark Network Analysis –
### 🔍 Description
Captured traffic from a TCP SYN scan using Nmap from the attacker machine (Kali) to the target server (192.168.1.10).  
This shows repeated SYN packets to multiple ports, probing for open TCP services.

### 🧩 Analysis
- Source: 192.168.1.150 (attacker)
- Destination: 192.168.1.10 (target)
- Pattern: Continuous SYN packets without completing the handshake (`SYN,ACK` → no ACK response)
- Purpose: Identify open ports without full connection (stealth scan)

### 🧠 SOC Interpretation
This traffic is typical of Nmap SYN scan (`nmap -sS`).  
In a live SOC environment, such traffic would indicate host reconnaissance orreshark 

---

## 🔹 Capture 2 — ARP Sweep / Network Discovery

File: scan-test
Filter: arp

### 🔍 Description
The source host 192.168.1.125 performs an ARP sweep asking:Who has 192.168.1.x? Tell 192.168.1.125
This covers many IPs in sequence (.1.16, .1.17, .1.18, … .1.57).

### 🧩 Analysis
- Source: 192.168.1.125 (attacker/scanner)
- Destination: Broadcast (ff:ff:ff:ff:ff:ff)
- Tool likely used: netdiscover -r 192.168.1.0/24
- Function: Maps all active IPs in the subnet using ARP requests.

### 🧠 SOC Interpretation
This is a layer-2 network discovery attack (reconnaissance).  
Attackers use ARP sweeps to find live hosts and their MAC addresses before port scanning.

---

## 🔹 Capture 3 — TCP Connection Refused / Port Closed

File: scan-test
Filter: ip.addr == 192.168....(Kali)

# 🧠 Wireshark Networ
### 🔍 Description
This capture shows multiple RST,ACK packets — the server responds to connection attempts with TCP reset packets, meaning the target ports were closed.

### 🧩 Analysis
- Source: 192.168.1.125 (scanner)
- Destination: 192.168.1.50
- Protocol: TCP
- Info field: [RST, ACK]  
  → Server refused connection attempt; port closed or filtered.

### 🧠 SOC Interpretation
This traffic pattern appears when an attacker scans many closed ports.  
It’s consistent with Nmap version detection (-sV) orreshark 

# 🧠 Wireshark Network Analysis

---

## 🔹 Capture 4 — Hydra SSH Brute-Force Attack

File: scan-test
Filter: tcp.port == 22 && ip.addr == 192.168...(Kali)

# 🧠 Wireshark Network Analysis – SOC P
### 🔍 Description
This capture shows massive simultaneous SSH connection attempts fromshark 

# 🧠 Wire(Kali) to the SSH server 192.168.1.50.  
All events occur at the same timestamp — typical of Hydra password brute-force.

### 🧩 Key Signs
- Dozens of SYN packets at 13:15:03 to port 22  
- Client uses libssh-0.11.3 (not OpenSSH → automation)  
- Each attempt initiates handshake but resets before authentication completes  
- Eventually some “Encrypted packet” lines appear → successful handshake(s)

### 🧠 SOC Interpretation
This is a brute-force attack:
- Many rapid SSH attempts from one IP  
- Short-lived connections, often reset quickly  
- Server may start dropping or RSTing under load  
- Auth logs will show “Failed password” repeatedly

---

## 🧠 Key Learning Outcomes
- Recognize distinct patterns for ARP scan, SYN scan, brute-force, and normal SSH traffic
- Understand TCP flags and their meaning (`SYN`, ACK, `RST`)
- Use Wireshark filters effectively for focused analysis

---

### 🏁 Next Steps
- Import pcap files into Splunk usinghark 
- Build dashboards to visualize SYN count,Wireshark 
- Continue daily lab exercises by simulating real-world SOC scenarios.

---

Lab Environment: Proxmox + Kali Linux + Raspberry Pi + Wireshark  
Focus: SOC Tier 1–2 training, network attack detection & packet analysis  
Date: *06 November 2025*
