# Home-lab (step by step)

## 🏗️ Lab Overview
📘 This lab is for educational and ethical testing only, performed on my own isolated network.

My SOC lab consists of multiple systems connected in an isolated network:

- Proxmox Server: Core hypervisor running virtual machines  
- Kali Linux: Attack simulation system  
- Ubuntu Server (Splunk): Log collection & SIEM analysis  
- Raspberry Pi 4: Network packet capture node (tcpdump automation)  
- Windows Host: Analysis and documentation workstation  
- Wireshark: For traffic inspection and forensic packet analysis

## 🧰 Tools Used

- Splunk (SIEM)
- Wireshark (Packet Analysis)
- Tcpdump (Capture automation)
- Kali Linux (Attack simulation)
- Proxmox VE, VirtualBox (Virtualization)
- Raspberry Pi 4 (Network sensor)
- Nmap / Hydra / Netdiscover (Testing & scanning)
- Scp / SSH (File transfer & remote access)

## 🖥️ Hardware Setup (OLD)
 
 • Host Laptop: Intel i7 10th Gen, 4 cores, 16 GB DDR4, 1 TB SSD

 • Secondary PC: Intel i5 6th Gen, 4 cores, 16 GB DDR4, 120 GB SSD
 
 • Server: Intel i5 4th Gen, 4 cores, 16 GB DDR3, 250 GB SSD + 2 TB HDD

 • Router: Used to create an isolated lab network (no internet)
 
 • Additional Laptop: Dual-core CPU, 4 GB RAM — for quick checks or file sharing

## 🧠 Hardware Setup (NEW)
 
 • Host Laptop: Intel i7 10th Gen, 4 cores, 16 GB DDR4, 1 TB SSD
 
 • Server: Supermicro Xeon 8 cores, 128 GB RAM, 500 GB SSD + 2×2 TB HDD (running Proxmox)
 
 • Ubuntu System: Intel i5 6th Gen, 120 GB SSD
 
 • Raspberry Pi 4 8 GB Ram + sd card 64 GB

 • Switch: TP-Link 5-Port Gigabit
 
 • Additional Laptop: Dual-core CPU, 4 GB RAM — used for internet checks and file sharing

 • Router: Old router configured to isolate internal lab network


## 🚀 Day 0 — Cybersecurity.Start

Date: September 23, 2025
 
 • Installed a clean Windows 10, then upgraded to Windows 11 to avoid compatibility issues.
 
 • Installed VirtualBox and added Ubuntu as the first virtual machine, followed by full updates.
 
 • Created additional Windows 10 VMs and resolved minor setup issues (e.g., disabling the floppy controller and deleting unnecessary system files).
 
 • Installed and updated Kali Linux without issues.

Later, I spent several days troubleshooting Ubuntu 24.04 while trying to install Wazuh and Splunk.
After multiple attempts, I successfully reinstalled Splunk on the new Ubuntu version, configured it, and verified it works properly.

 • Configured Windows (PowerShell + CMD) and Ubuntu (Terminal) for event forwarding into Splunk.

 • Created a shared folder between Windows and Ubuntu to exchange scripts, screenshots, and logs efficiently.


## 🧩 Day 1 — Checking Connectivity and Functionality

 • Verified all network connections and system communication.
 
 • Tested Windows → Ubuntu log forwarding using PowerShell event generation.

 • Identified an initial issue caused by antivirus interference, which blocked event forwarding.
 
 • ✅ Solved by adjusting antivirus rules and reconfiguring permissions.
 
 • Successfully sent 1, 10, and 100 events with different log levels: Error, Info, Warning.
 
 • Created a command reference text file containing essential maintenance and diagnostic commands for both Windows and Ubuntu, useful when working in Splunk.


<img width="1920" height="923" alt="Screenshot from 2025-09-27 12-38-36" src="https://github.com/user-attachments/assets/b0900b6f-81d7-430c-a73d-2fecbaaead8f" />
<img width="1025" height="910" alt="Screenshot from 2025-09-27 12-55-11" src="https://github.com/user-attachments/assets/d871db26-7ee2-4201-b39e-78f2623539d0" />
<img width="1920" height="923" alt="Screenshot from 2025-09-27 12-45-01" src="https://github.com/user-attachments/assets/59a0584b-834c-410b-a45b-f300433a3686" />



## Day 2 - Splunk Home Lab - Event Monitoring & Alerts
Was testing around 4 hours how everything works. Learning how to work with Splunk web.

1️. Machine Connectivity
- Connected multiple machines in a closed network.
- Verified that events are sent and received correctly between machines.
- Ensured proper data flow to Splunk indexes for monitoring.

2️. Log Generation & Analysis
- Generated 3,000–4,000 simulated log events with levels INFO, WARN, ERROR.
- Logs uploaded to Splunk and each event verified.
- Extracted important fields using rex.

3. Created alerts and learned how to save cvs files


<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 123405" src="https://github.com/user-attachments/assets/2bea63a8-8a1e-4e7b-9128-5dea1bcccbf7" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 140459" src="https://github.com/user-attachments/assets/619071f7-cb32-4b24-b008-f78497a1b11f" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 140250" src="https://github.com/user-attachments/assets/4f30c3e5-ad4f-4e93-958d-9aa3306b7f98" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 125852" src="https://github.com/user-attachments/assets/db316be7-4213-4710-b737-5f6c21ea306b" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 124025" src="https://github.com/user-attachments/assets/8f363536-d402-49b3-923c-fd8cc9da1315" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 155801" src="https://github.com/user-attachments/assets/5450a37f-b098-4de9-8e21-7d7bdae49cec" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 155316" src="https://github.com/user-attachments/assets/44ea47af-0b7c-464d-9b15-f9dc780a8c47" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 154930" src="https://github.com/user-attachments/assets/6a502b2d-5397-4efe-b916-7624e8194afc" />


## Day 3 - Splunk Installation Failure on Windows

I thought that everything works fine but when i started practice on sending events the splunk connection got broken and events stop coming on me host pc. So i decided to take anothere pc and install everything on more time but on clean windows 10.

Goal: Install Splunk Universal Forwarder on Windows and connect it to my Splunk Enterprise instance.
Result: ❌ Unsuccessful — encountered repeated MSI installer errors and permission issues.

Steps Taken
 1. Downloaded the official Splunk Universal Forwarder .msi from Splunk’s website.
 2. Tried to install normally → No “Run as administrator” button available.
 3. Attempted installation via Command Prompt and PowerShell with:

→ Result: “No se puede abrir este paquete de instalación…” error.

 4. Verified the MSI file was not corrupted.
 5. Checked permissions — account had administrator rights.
 6. Tried extracting MSI to TEMP and running from there → same error.
 7. Attempted to enable logging and check Windows Installer service — error 2203 and 1402, Rollback\Scripts key missing.
 8. Even on a brand new Windows PC the same MSI error appeared.
 9. Disabled antivirus and firewalls — still failed.
 10. After 8+ hours of troubleshooting (MSI repair, permissions, logs) → no progress.

Errors Encountered
 • Windows Installer Error 2203 & 1402 (permissions & missing registry keys).
 • “No se puede abrir este paquete de instalación…” despite valid MSI.
 • No Rollback\Scripts registry keys present.
 • Installation fails before any UI appears.

Resolution

💡 Switched to Linux. Installed Splunk Forwarder on Ubuntu in minutes using .tgz, configured forwarding to Splunk Enterprise, and started generating and analyzing events successfully.

Lessons Learned
 • Windows MSI installers can fail even on fresh systems, and debugging is often time-consuming.
 • Linux installation is much more transparent (untar + run commands).
 • Always have a backup platform (Ubuntu) to continue practicing if one system blocks progress.
 • Network and permissions issues are easier to debug on Linux with standard tools (tar, ss, nc, ping, etc.).


 ![photo_2025-10-05_23-45-55](https://github.com/user-attachments/assets/bd539b81-e15c-4c36-b9b9-4adfe043eb92)
![photo_2025-10-05_23-46-03](https://github.com/user-attachments/assets/2aab05a9-65f2-42b9-ac05-3c1e7dd564c6)
![photo_2025-10-05_23-46-14](https://github.com/user-attachments/assets/731778df-ede0-479b-b2b2-72ea159929c6)



## Day 4 - Practice fully on Ubuntu

Today I set up my home lab but based on Linux to practice log ingestion, forwarding, and alerting in a fully offline environment. The lab consisted of:

 • Host machine: Ubuntu 24.04 VM running Splunk Enterprise
 
 • Secondary machine: Physical Ubuntu PC acting as a Splunk Universal Forwarder also 24.04

Key Steps Completed

 1. Clean Setup & Installation
 
 • Installed Splunk Universal Forwarder on Ubuntu2.
 
 • Configured forwarding to the host Splunk Enterprise instance.

 • Verified service status and active forwarders with splunk list forward-server.

 2. Log Ingestion Practice
 
 • Created custom log file /var/log/custom_test.log with multiple event types (INFO, WARN, ERROR) using bash loops.
 
 • Configured inputs.conf to monitor the custom log file and assigned index=main and sourcetype=custom_test.
 
 • Confirmed logs appeared in Splunk Web using searches like:

3. Forwarding & Connectivity Tests

 • Verified network connectivity between Ubuntu2 (forwarder) and host VM via ping and nc -vz <host_ip> 9997.
 
 • Observed forwarded events arriving correctly in the host Splunk instance.

4. Alerts & Testing
 
 • Practiced creating alerts on custom log events (INFO/WARN/ERROR).
 
 5. Lessons Learned
 
 • Linux permissions are crucial; most errors were caused by incorrect ownership or missing directories.

 • Forwarder configuration and network setup must match IPs and open ports.

 • Offline labs are fully functional for ingesting, searching, and alerting without needing internet.

<img width="1920" height="922" alt="Screenshot from 2025-10-02 13-53-51" src="https://github.com/user-attachments/assets/88f5ff00-c5a7-46da-ac2d-f79eea4ee57a" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 13-48-49" src="https://github.com/user-attachments/assets/4ad67967-89a1-4424-81a9-f99e0144c355" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 13-36-13" src="https://github.com/user-attachments/assets/b90f234a-8c03-48b8-8550-079310b60a06" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 13-31-13" src="https://github.com/user-attachments/assets/6462bec6-74a2-4b9c-941f-0b58e80c6ee2" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 13-09-39" src="https://github.com/user-attachments/assets/ba9b2614-651e-4b11-80d9-08b205b7b5b9" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 12-58-25" src="https://github.com/user-attachments/assets/c84740a9-50b3-4426-95c1-e61e38782163" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 12-47-40" src="https://github.com/user-attachments/assets/5d9a3e69-fed6-44bf-9c86-d96795aa2d35" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 12-44-59" src="https://github.com/user-attachments/assets/dfacacc0-3d2d-42b4-9bf0-fb7730ce9bae" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 12-35-49" src="https://github.com/user-attachments/assets/64536968-89a0-4a38-9b56-1d10000efd0c" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 12-20-43" src="https://github.com/user-attachments/assets/44b97a8d-625a-4ee7-8127-f242e8b5a503" />
<img width="1805" height="698" alt="Screenshot from 2025-10-02 14-58-41" src="https://github.com/user-attachments/assets/3cfa4a2f-82d5-4470-98a3-327e7fb9e130" />

## Day 5 - Splunk Log Forwarding and Dashboard Practice

### 🏗️ Goal
Continue developing hands-on Splunk skills by configuring log forwarding between my physical Ubuntu machine (forwarder) and Ubuntu VM (indexer), validating event flow, and creating dashboards for analysis.

### ⚙️ Setup
Systems Involved:
- Ubuntu physical machine — Splunk Universal Forwarder  
- Ubuntu VM (on Windows host) — Splunk Enterprise Indexer  
- Windows Host — used to monitor and manage configuration  

Configuration Steps:
- Verified network connectivity and open communication ports  
- Configured Splunk Forwarder → Indexer connection  
- Adjusted firewall settings to allow Splunk traffic  

### 🧩 Work Summary
- Generated multiple custom log events with severity levels:  
  - INFO – normal operations  
  - WARN – system warnings  
  - ERROR – simulated failures  
- Confirmed successful event ingestion and indexing in Splunk  
- Created alerts for specific event types to simulate real SOC monitoring  
- Designed dashboards for data visualization and pattern recognition  

### 🔍 Analysis
- Observed SSH connection logs and built alerts for failed login attempts  
- Visualized the frequency and timing of SSH errors in real time  
- Practiced event classification, alert tuning, and data correlation  

This session reinforced core SOC concepts:
> Log collection → Event categorization → Alerting → Visualization → Incident awareness.

<img width="1920" height="922" alt="Screenshot from 2025-10-02 12-20-43" src="https://github.com/user-attachments/assets/c10a84bf-cd62-46e0-b761-ad8727fc1147" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 12-47-40" src="https://github.com/user-attachments/assets/80aeeb0e-1698-4868-8832-a41dd7278376" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 13-31-13" src="https://github.com/user-attachments/assets/3c020aa0-3814-4412-90e6-fa0d9e9a595c" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 13-48-49" src="https://github.com/user-attachments/assets/70b8344c-1441-4cfd-b6c3-ba7212cd141f" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 13-53-51" src="https://github.com/user-attachments/assets/9b1011f7-8ab0-499e-b0e6-a5eddaf06198" />
<img width="1920" height="923" alt="Screenshot from 2025-10-06 15-01-07" src="https://github.com/user-attachments/assets/c73cfbde-483a-4e14-8d25-3fa846f88f35" />
<img width="1920" height="923" alt="Screenshot from 2025-10-06 15-30-52" src="https://github.com/user-attachments/assets/d92c9421-b811-4957-91ab-a0fb66e30862" />
<img width="1920" height="923" alt="Screenshot from 2025-10-06 15-36-10" src="https://github.com/user-attachments/assets/47be3a54-0c19-4410-bf81-62af176eb315" />

### 🧭 Next Steps
- Integrate Windows event logs into the same Splunk instance  
- Correlate SSH failures with Windows authentication logs  
- Expand dashboard automation for daily monitoring practice


## Day 6 - Events,Dashboards

What was done
 
 • Reviewed and analyzed previously generated test events (Error, Info, Warning, SSH).
 
 • Verified that events were correctly indexed and visible through the Search & Reporting app.
 
 • Created and customized a Classic Dashboard in Splunk:
 
 • Added multiple visualizations including pie charts, bar charts, and single value panels.
 
 • Grouped events by sourcetype and severity level.
 
 • Displayed SSH activity over time and error counts in real-time.
 
 • Practiced alerting concepts and reviewed email alert limitations in closed lab networks.
 
 • Fixed permission issues related to event generation and log file monitoring.
 
 • Sent and monitored over 100 SSH-related events to test dashboard responsiveness.

 Key Learnings
 
 • How to build and structure dashboards in Splunk using classic panels.
 
 • Importance of permissions when creating and writing to log files.
 
 • Understanding how different sourcetypes and event severities can be visualized together.

<img width="1920" height="923" alt="Screenshot from 2025-10-07 18-10-57" src="https://github.com/user-attachments/assets/2d8e66b2-7334-4423-8617-9ed680233edb" />

<img width="1920" height="923" alt="Screenshot from 2025-10-07 18-16-59" src="https://github.com/user-attachments/assets/0b2ce272-2e2b-42cd-9c01-af2127c9813d" />


Dashboard
<img width="1080" height="1795" alt="Screenshot from 2025-10-07 18-30-32" src="https://github.com/user-attachments/assets/ed3292bc-8d47-4f18-b265-4ba05de46044" />

<img width="1080" height="1795" alt="Screenshot from 2025-10-07 18-31-58" src="https://github.com/user-attachments/assets/cf1649f8-862a-4168-a2e9-9a979c728196" />

<img width="1080" height="1795" alt="Screenshot from 2025-10-07 18-45-09" src="https://github.com/user-attachments/assets/27b4f6ab-b4dc-4823-a60f-f359de8447ed" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-07 18-57-36" src="https://github.com/user-attachments/assets/bc91f61b-a593-499e-a159-8a25a92585b3" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-07 18-58-28" src="https://github.com/user-attachments/assets/8cb85e0d-e178-4198-a06d-218b1f7e09a4" />

## Day 7 - Splunk Log Monitoring & SOC Lab

Today I focused on building a hands-on log monitoring workflow using Splunk Enterprise and Splunk Forwarder. The main tasks completed were:
 1. Environment Setup: Verified connectivity between Ubuntu VMs, ensuring the forwarder sends logs to Splunk Enterprise successfully.
 2. Log Generation & Testing: Created synthetic logs including INFO, WARN, ERROR, and SSH failed login events. After starting the log generator, events were received in real time by Splunk.
 3. Live Event Dashboard: Built a SOC-style dashboard displaying event counts by type, top SSH attacker IPs, and recent events, with color-coded severity for easy visualization.
 4. Alerts Configuration: Set up real-time alerts for SSH failures, ERRORs, and WARNs, enabling immediate notification of anomalies.

Key Learnings:
 
• Handling unmatched events (NULL) and labeling them for better visualization.

• Creating real-time dashboards and alerts to simulate SOC monitoring.

• Practical experience with log generation, ingestion, and visualization in a controlled lab environment.

<img width="1080" height="1795" alt="Screenshot from 2025-10-13 09-39-06" src="https://github.com/user-attachments/assets/3050506c-cac4-4a75-83d4-348b78cec7d0" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-13 12-19-25" src="https://github.com/user-attachments/assets/653e3143-323d-4cc3-88ff-95fed222c042" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-13 12-21-25" src="https://github.com/user-attachments/assets/6e10c0a2-7df9-4ff6-b16e-30a847a6d619" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-13 13-05-45" src="https://github.com/user-attachments/assets/753a158b-f8fb-46f0-82f4-10b16664a89b" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-13 13-22-57" src="https://github.com/user-attachments/assets/e86f1437-e1b9-4cef-987d-9f6fe4090b5c" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-13 13-36-42" src="https://github.com/user-attachments/assets/22a61653-0e56-42e3-9eca-5e96ec8c1327" />
<img width="1920" height="1080" alt="Screenshot from 2025-10-13 11-35-20" src="https://github.com/user-attachments/assets/33d85491-c816-4356-a815-9e686c4cb9fa" />
<img width="1920" height="1080" alt="Screenshot from 2025-10-13 11-52-11" src="https://github.com/user-attachments/assets/c120cb57-8c85-4cbb-af1e-b6a3bdb6c8ac" />
<img width="1920" height="1080" alt="Screenshot from 2025-10-13 12-03-49" src="https://github.com/user-attachments/assets/be6a6619-40fe-4f56-8edd-6a0405d36d97" />
<img width="1920" height="1080" alt="Screenshot from 2025-10-13 14-16-13" src="https://github.com/user-attachments/assets/2b1569ae-f981-45cc-af60-7fbf58eb58c6" />
<img width="1920" height="1080" alt="Screenshot from 2025-10-13 15-43-12" src="https://github.com/user-attachments/assets/2978d4d5-ee7e-44b0-abef-d37beae3a55f" />

 

Next Steps: Extend the lab with correlation searches and more complex SOC scenarios for enhanced security monitoring practice.

## Day 8 - Splunk Lab: Real-Time Log Monitoring, Field Extraction, Dashboards & Alerts

Environment Setup
 
 • Host PC: Ubuntu with Splunk Enterprise
 
 • VM / Remote PC: Ubuntu with Splunk Universal Forwarder
 
 • Verified SSH connectivity between host and forwarder.
 
 • Splunk Forwarder installed and configured to send logs to Splunk Enterprise.

⸻

Log Preparation

 • Created a custom log file: /var/log/custom_test.log
 
 • Generated different log types:
 
 • INFO → normal events (e.g., User logged in, Page served)
 
 • WARN → warnings (e.g., Slow DB query, High memory usage)
 
 • ERROR → errors (e.g., Permission denied, Service crashed)
 
 • Simulated failed SSH login attempts with dynamic usernames, IPs, and ports.

 • Confirmed logs were ingested in real-time by Splunk after enabling the log generator.

⸻

Field Extraction

 • Used Field Extractor (rex) to extract:
 
 • username
 
 • src_ip
 
 • port
 
 • Verified fields appeared correctly in search results and in dashboard panels.
 
 • This allowed aggregation, visualization, and alerting.

⸻

Dashboard Creation
 
 • Created a new dashboard combining all extracted fields.
 
 • Panels included:
 
 • Top attacking IP addresses
 
 • Top targeted usernames
 
 • Recent failed login events
 
 • Set dashboard to refresh every 1 minute for real-time monitoring.
 
 • Tested PDF export functionality to practice report sharing.

⸻

Alerts
 
 • Created alerts for suspicious IPs based on thresholds (e.g., multiple failed logins).
 
 • Alerts were linked to extracted fields (src_ip) and could trigger notifications.

⸻

Observations
 
 • Real-time logs worked as expected 👍
 
 • NULL values appeared in some columns — caused by failed SSH login events, normal in this lab setup
 
 • Geolocation columns (Country/City) were empty because IPs were private lab addresses — expected behavior in a home lab
 
 • Dashboard visualization allowed quick identification of suspicious activity across multiple fields


<img width="1080" height="1795" alt="Screenshot from 2025-10-14 09-58-41" src="https://github.com/user-attachments/assets/ad9a2db7-ab87-423a-bf21-ce1455d7a42c" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-14 10-02-26" src="https://github.com/user-attachments/assets/9e3f466a-1079-4077-8fac-f7c25faebb7e" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-14 10-06-19" src="https://github.com/user-attachments/assets/e219c75e-6c11-44f2-9a2f-702b9adb351b" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-14 10-15-32" src="https://github.com/user-attachments/assets/d53995c3-c334-4c90-a265-b22e11838127" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-14 11-23-36" src="https://github.com/user-attachments/assets/823c745e-3c14-4820-8e0e-033fe275ac8f" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-14 11-24-00" src="https://github.com/user-attachments/assets/f21f8b95-53a4-4bcd-936b-c6d220661c11" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-14 11-43-46" src="https://github.com/user-attachments/assets/b33f2606-f4af-4b11-9687-651e57d40bbf" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-14 11-50-33" src="https://github.com/user-attachments/assets/b011348a-1eb7-4735-add1-9f9b18b8bc78" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-14 11-52-12" src="https://github.com/user-attachments/assets/f7599ca8-26de-4958-a3de-8e6b654e3282" />
<img width="1080" height="1795" alt="Screenshot from 2025-10-14 12-02-31" src="https://github.com/user-attachments/assets/fefca96e-9f11-467a-88c7-249483c7de47" />


Next Steps / To-Do
 
 • Extend dashboards for error/warn/info logs
 
 • Test alerts by generating more SSH failed login events
 
 • Explore additional SPL commands: timechart, top, where
 
 • Simulate public IPs to enable geolocation mapping in dashboards


## Day 9 – Home Lab expanded
Date: 2025-10-16

## Summary:
Today I expanded my home lab by integrating my new server (PC3) with the existing environment. The goal was to practice multi-device log forwarding, SSH management, and real-time monitoring in Splunk.

## Work Completed:

## 1. Hardware Integration:
 • Added PC3 (i5 4th Gen) to the lab.
 
 • Installed 2×1TB HDDs in PC3.
 
 • Connected PC3, PC2, and the host laptop to the new TL-SG105E switch.
 
 • Configured switch with basic settings:
 
 • Access to web interface.

 • Default QoS and VLAN settings for lab network.
 
## 2. Operating System & Network:

 • Installed Ubuntu Server 22.04 on PC3.
 
 • Configured static IP for PC3: 192.168.1.10/24 via netplan.
 
 • Gateway: 192.168.1.1 (router)
 
 • DNS: 192.168.1.1

 • Connected host laptop via WiFi, PC2 via Ethernet.
 
 • Ensured PC3 is reachable via SSH from PC2.

 • Note: If the router is turned off or devices reconnect, dynamically assigned IPs (DHCP) may change unless static IPs are set on all machines or reserved in the router.
 
## 3. Splunk Forwarder Setup:

 • Installed Splunk Universal Forwarder on PC3.

 • Configured forwarder to send logs to the Splunk host (host laptop).
 
 • Verified connectivity and forwarding using nc and splunk list forward-server.
 
## 4. Testing & Monitoring:
 
 • Confirmed active forwarders on the Splunk host.
 
 • Tested sending logs from PC3 through SSH-managed terminals.
 
 • Verified that the host receives logs correctly.

## Challenges:
 
 • Initial confusion with IP addressing and Splunk session login.
 
 • Minor troubleshooting required for firewall and forwarder configuration.

## Key Takeaways:

 • Multi-device lab setup allows practicing realistic SOC workflows.

 • SSH access to servers enables headless management.
 
 • Splunk forwarders can be configured on multiple machines, sending logs to a central host for monitoring.

 • Static IPs are important for consistency in lab environments to prevent connection issues.

## Next Steps:
 
 • Practice sending custom logs from PC3 and verifying them in Splunk.
 
 • Automate log generation and forwarding for real-time dashboard updates.

 • Continue expanding lab with more scenarios and alerts.


<img width="1920" height="922" alt="Screenshot from 2025-10-16 17-50-32" src="https://github.com/user-attachments/assets/65dd59e5-9051-4928-bb5c-5ea5a77b8270" />
<img width="1920" height="1080" alt="Screenshot from 2025-10-16 20-11-23" src="https://github.com/user-attachments/assets/c4781938-dbfd-4311-bd5c-3fdadf3e960d" />
<img width="1920" height="1080" alt="Screenshot from 2025-10-16 20-42-32" src="https://github.com/user-attachments/assets/a84843b5-34ef-474c-ac96-dd7f16f6891b" />
<img width="1920" height="1080" alt="Screenshot from 2025-10-16 21-01-02" src="https://github.com/user-attachments/assets/d61c1389-03e9-4300-add5-5e0424432609" />


## Day 10 – Home Lab Practice (Splunk + Server Management)

## What I did today:

 ## 1. Server Management via SSH

 • Managed PC3 (server) from PC2 using SSH.
 
 • Opened two terminals simultaneously:

 • One for monitoring logs.

 • One for server management and configuration.

 • This setup made managing the server more convenient without needing to use the host laptop directly.

 ## 2. Log Forwarding & Monitoring
 
 • Confirmed that PC2 and PC3 are sending logs to the Host Laptop (running Splunk Enterprise).

 • Tested sending custom logs from PC3 using:

echo "Hello Splunk! $(date)" | sudo tee -a /tmp/test_splunk.log

• Verified logs appear in real-time on Splunk.

 ## 3. Live Log Generator
 
 • Started automatic log generation on PC2 and PC3 (server) to simulate real-time events.

 • Observed logs from both PCs flowing into Splunk dashboards.

 ## 4. Switch Configuration

 • Renamed the switch to a friendly name.

 • Verified port mapping:
 
 • Port 1 → Router

 • Port 2 → PC2
 
 • Port 3 → PC3 (Server)

 • Port 4 → Host Laptop

## Notes & Insights:
 • Host Laptop is mainly receiving logs; PC2 acts as the control terminal for server management.
 • Multiple SSH sessions make it easy to monitor and manage the server at the same time.
 • Lab environment is now fully functional with 3 computers + switch + router, ready for further practice and log experimentation.

<img width="1920" height="1080" alt="Screenshot from 2025-10-17 15-47-43" src="https://github.com/user-attachments/assets/2bc034f0-3f8e-467d-b932-4ea68f936523" />
<img width="1920" height="1080" alt="Screenshot from 2025-10-17 16-05-05" src="https://github.com/user-attachments/assets/9068ff41-f283-48ab-a347-ecdc0e89e363" />
<img width="1920" height="922" alt="Screenshot from 2025-10-16 19-47-17" src="https://github.com/user-attachments/assets/2a8f0187-55bf-42a6-b2bf-a103553eb5c8" />
<img width="1920" height="922" alt="Screenshot from 2025-10-17 13-45-13" src="https://github.com/user-attachments/assets/5fae6cc5-da06-4ef1-a2cf-c5a7306f014e" />
<img width="1920" height="922" alt="Screenshot from 2025-10-17 13-47-44" src="https://github.com/user-attachments/assets/ed92a973-1aa2-4d18-be57-b3a5acdc5049" />
<img width="1920" height="922" alt="Screenshot from 2025-10-17 14-00-15" src="https://github.com/user-attachments/assets/21155882-5fd6-4f3c-8e24-bce6753a165c" />
<img width="1077" height="1914" alt="Captura de pantalla 2025-10-17 163636" src="https://github.com/user-attachments/assets/66db92af-07fc-440a-ae29-2de42fb9a5bd" />

## Next steps:
 1. Configure PC3 to forward specific logs needed for testing.
 2. Use more an automatic log generator on PC3 like on PC2.
 3. Practice more advanced Splunk dashboards and alerts with both forwarders.
 4. Explore additional switch features like VLANs or QoS if needed.


## Day 11 — Raspberry Pi Integration as Network Sensor

## Overview

Today I successfully integrated a Raspberry Pi 4 (8 GB) into my home cybersecurity lab.
The Pi now works as a network sensor, continuously capturing LAN traffic via the switch’s mirrored port.
Captured data is later analyzed on my host PC with Wireshark.

## Configuration Summary
 
 • Hardware: Raspberry Pi 4 (8 GB RAM / 64 GB SD Card / Ethernet)

 • Network: Connected through managed switch (TP-Link TL-SG105E) to mirror PC2 + PC3 ports
 
 • Installed and tested tcpdump for manual packet capture
 
 • Built auto-capture script that saves .pcap files every 15 minutes
 
 • Verified cron job activity using journalctl
 
 • Enabled SSH for remote file management and transfer
 
 • Transferred .pcap files to host and opened them in Wireshark

## Key Commands Used

ip a

sudo tcpdump -i eth0 -c 200 -w /home/admin/captures/test_$(date +%F_%H%M%S).pcap
ls -lh /home/admin/captures

sudo /usr/local/bin/autocapture.sh

sudo crontab -e

sudo journalctl -u cron -b

scp admin@192.-.-.-:/home/admin/captures/*.pcap ~/Desktop/

sudo systemctl enable ssh

## Results
 • Automatic packet captures confirmed working
 
 • Files transferred successfully and opened in Wireshark
 
 • Raspberry Pi operating fully headless via SSH
 
 • Network traffic from Splunk forwarders visible in live captures

<img width="1920" height="1080" alt="20251021_12h06m29s_grim" src="https://github.com/user-attachments/assets/f1d06230-8d5c-4adb-a2e6-5afdde1eb429" />
<img width="1920" height="1080" alt="20251021_14h34m53s_grim" src="https://github.com/user-attachments/assets/701487d9-fe80-43bc-b20f-d9e74f54b9ee" />
<img width="1920" height="1080" alt="20251021_16h34m45s_grim" src="https://github.com/user-attachments/assets/ef70ab32-c72a-48f3-8758-81c917fa78a5" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-10-21 201815" src="https://github.com/user-attachments/assets/d17bb0fa-5161-4893-84ed-c4c4d6533606" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-10-21 215811" src="https://github.com/user-attachments/assets/40f74bda-f7f0-42af-8e93-b6fb35989558" />
<img width="1920" height="922" alt="Screenshot from 2025-10-21 19-38-23" src="https://github.com/user-attachments/assets/778b1520-3cce-45d6-a69d-40cd2c5e7800" />
<img width="1920" height="922" alt="Screenshot from 2025-10-21 19-45-17" src="https://github.com/user-attachments/assets/a54c45c5-0bf3-47f8-bb9f-31b665d888ff" />


## Next Steps
 
 • Automate file transfer to host for daily review
 
 • Start filtering captures by protocol (DNS, HTTP, TCP, ICMP)
 
 • Identify attack signatures and anomalies in generated traffic

 • Integrate Wireshark filters + Splunk dashboards to correlate data


## Day 12 – Splunk Querying, Raspberry Pi Integration & Network Analysis

Date: October 22, 2025

Focus: Log correlation, Splunk dashboarding, alerts, and network packet analysis

## Main Accomplishments
 
 1. Checked connectivity and Splunk Forwarders:
 
 • Verified that all machines (PC2, PC3, Raspberry Pi, and host) are connected and forwarding logs to the Splunk indexer successfully.

 • Ensured communication between nodes via Ethernet and network ping tests.
 
 2. Raspberry Pi Integration:
 
 • Verified sensor functionality and log capture from Raspberry Pi.

 • Executed and validated network capture scripts.
 
 • Successfully transferred .pcap files to host via scp for offline analysis.
 
 3. SSH Remote Management:
 
 • Connected from PC2 to PC3 (server) via SSH.
 
 • Managed log generation scripts remotely to test real-time Splunk log forwarding.

 4. Splunk Analysis & Visualization:
 
 • Used multiple search queries to filter and analyze authentication and network logs.
 
 • Built a custom Splunk dashboard visualizing failed/successful login attempts.
 
 • Implemented visual panels for top IPs, top users, and login trends over time.
 
 5. Splunk Alert Configuration:
 
 • Created an alert trigger for failed login attempts (threshold: >2 attempts).
 
 • Configured alert action for monitoring brute-force activity simulation.
 
 6. Packet Capture Analysis in Wireshark:
 
 • Pulled last network captures from Raspberry Pi to host using SCP.
 
 • Imported captures into Wireshark.
 
 • Applied filters:
 
 • tcp
 
 • icmp
 
 • tcp.port == 9997 (Splunk traffic filter)
 
 • Observed traffic flow between forwarders and Splunk host.


## Tools Used
 
 • Splunk Enterprise (Indexer & Web Interface)
 
 • Splunk Universal Forwarder
 
 • Wireshark
 
 • Raspberry Pi 4 (as passive network sensor)

 • SSH (remote management)
 
 • SCP (secure copy)


## Key Learnings
 
 • Improved efficiency in Splunk query building and dashboard customization.
 
 • Understood data flow from system logs → Splunk index → visual dashboard.
 
 • Learned how to identify and analyze TCP flows and Splunk communication in Wireshark.
 
 • Practiced remote log management and network packet capture automation.


<img width="1920" height="922" alt="Screenshot from 2025-10-22 09-33-40" src="https://github.com/user-attachments/assets/df3e88bb-d5cb-4e67-b0ab-f55ac284e2d5" />
<img width="1920" height="922" alt="Screenshot from 2025-10-22 09-14-53" src="https://github.com/user-attachments/assets/de222ba6-3fe7-49b7-96cb-92fe5eb51f25" />
<img width="1920" height="922" alt="Screenshot from 2025-10-22 09-08-36" src="https://github.com/user-attachments/assets/b43ff784-4aba-4626-b80d-81747bb05494" />
<img width="1920" height="1080" alt="Screenshot from 2025-10-22 10-48-43" src="https://github.com/user-attachments/assets/f01ec5a6-e259-4082-ae7b-f5199151dc04" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-10-22 114108" src="https://github.com/user-attachments/assets/3145db29-327d-4205-9dcc-0c10e680660b" />


## Next Steps
 
 • Automate .pcap capture rotation on Raspberry Pi (with cleanup for older captures).
 
 • Configure Splunk to receive and index Raspberry Pi network logs.
 
 • Expand Splunk dashboard to include network flow analysis panels.
 
 • Practice more advanced Splunk search operators (e.g. eval, lookup, stats with conditions).

## Day 13 - Network Analysis, Splunk Correlation & SSH Traffic Capture

Date: October 23, 2025

## 🧩 Summary:

Today I focused on combining Splunk log monitoring with real network traffic analysis using my Raspberry Pi 4 as a network sensor.
 
 • Verified Splunk connectivity between all machines (host, PC2, and PC3).
 
 • Analyzed SSH brute-force simulation logs in Splunk Web — filtered and visualized failed password attempts, usernames, and IP sources.

 • Built new Splunk dashboard panels and refined search queries for security analysis.
 
 • Captured real network traffic on the Raspberry Pi and confirmed SSH communication packets between my PCs.

 • Learned to interpret TCP 3-way handshake (SYN, SYN/ACK, ACK) in Wireshark and matched it to Splunk logs for correlation.
 
 • Practiced packet filtering and analysis in Wireshark using expressions like tcp.port == 22.
 
 • Tested automatic log and packet capture scripts — confirmed correct operation.

 • Maintained static IP configuration across all systems and verified SSH access stability.

## 💻 Tools & Technologies:

 • Splunk Enterprise (log indexing & alerting)
 
 • Wireshark (network analysis)

 • Raspberry Pi 4 (8GB) as network sensor
 
 • Ubuntu Server + SSH Forwarders
 
 • Custom log generator & Splunk search filters

## 🧩 Extra Work:

 • Studied TryHackMe for ~3 hours (topics: Linux privilege escalation & network fundamentals).
 
 • Practiced threat analysis and basic attack detection logic.

## ✅ Achievements:
 
 • Successful end-to-end visibility: from simulated logs → network packets → dashboard visualization.

 • Confirmed live capture of TCP/SSH handshakes and Splunk correlation.

 • Raspberry Pi functioning as independent, passive monitoring node.

## 🔜 Next Steps:
 
 • Automate Wireshark/pcap export review workflow.
 
 • Explore Splunk correlation searches (match logs + packet timestamps).
 
 • Begin building a Security Events Overview dashboard in Splunk.

 • Continue THM labs focused on network-based attack detection and log correlation.

<img width="1920" height="1080" alt="Captura de pantalla 2025-10-23 192948" src="https://github.com/user-attachments/assets/3cc26e6e-d791-4c25-8338-85070cbff4b1" />

<img width="1920" height="1080" alt="Captura de pantalla 2025-10-23 191129" src="https://github.com/user-attachments/assets/5a8ac8da-d4fb-4ad2-872b-0c241c112dc3" />


## Day 14 - New "Toy"

## 🖥️ New Server Setup (Supermicro Xeon D-1541)

This week I expanded my cybersecurity and homelab environment with a Supermicro X10SDV-8C-TLN4F server (Intel Xeon D-1541, 128 GB ECC RAM, SSD + HDD storage).
The system was fully cleaned, inspected in BIOS, and successfully booted into Proxmox VE 8.4.

## Work completed so far
 
 • Verified all 128 GB RAM, CPU cores, and disks in BIOS and Proxmox.
 
 • Installed and configured Proxmox VE 8.4 on SSD (LVM + ZFS storage pools).
 
 • Created first VM (Ubuntu 24.04 LTS) and confirmed full functionality.
 
 • Tested system stability and temperature monitoring (~53–55 °C under load).
 
 • Prepared for network tuning and static IP configuration in Netplan.

## Next steps:
 
 • Configure static IP on Ubuntu VM.
 
 • Add additional VMs for Splunk Forwarder and Raspberry Pi network-sensor integration.
 
 • Begin documenting performance benchmarks and automation scripts.

<img width="1920" height="1080" alt="Captura de pantalla 2025-10-26 112548" src="https://github.com/user-attachments/assets/d82bb4bd-ec0a-450b-839f-442d329d6b8e" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-10-26 191212" src="https://github.com/user-attachments/assets/b943da35-c411-43d1-ae74-79881d99d625" />


## Day 15-17 - networking, automation, and observability

Date: October 28-30, 2025

Huge progress today across networking, automation, and observability in my home lab.

## ✅ What I accomplished

 • Proxmox & Networking

 • Installed and configured Kali on my Proxmox + UF + static ip
 
 • Installed and configured Windows 10 on my Proxmox + UF + static ip
 
 • Set static IP on my Proxmox Ubuntu VM (ens18) and verified persistence.

 • Integrated the new Supermicro Xeon server into my lab (router + TL-SG105E switch).
 
 • Splunk Forwarding

 • Installed Splunk Universal Forwarder on the Proxmox Ubuntu VM.

 • Configured inputs (syslog + custom file) and connected to my Splunk Enterprise indexer.

 • Deployed a log generator systemd service on the VM to simulate INFO/WARN/ERROR + SSH failed-login lines into /var/log/custom_test.log (ingested live into Splunk).

 • Raspberry Pi Network Sensor
 
 • Pi runs automatic packet captures and SCPs the newest .pcap to my Ubuntu host VM every 15 minutes.

 • Added cron heartbeats and logging; verified hands-off operation.

 
 • Ingested Pi sync logs into Splunk for visibility (source=/home/user/pi_sync.log).

 • Dashboards & Alerts

 • Built Splunk dashboards for syslog + simulated app logs (username, src_ip, port extractions).

 • Added alert: >2 failed SSH passwords within 5 minutes.

## 🔧 Key commands/config (high level)

 • UF install on VM: extract → /opt/splunkforwarder/bin/splunk enable boot-start → set outputs to indexer → add monitors.

 • VM log generator: systemd service writing to /var/log/custom_test.log at random intervals.

 • Pi automation: /usr/local/bin/autocapture.sh + sync_latest_capture.sh via cron (*/15 * * * *), SSH keys for passwordless copy, cleanup (find … -mtime +3 -delete).

## 📈 Results

 • End-to-end pipeline now continuous and automated:

 • VM → Splunk (UF) ✅
 
 • Pi → Host VM (SCP) → Wireshark + Splunk log of sync events ✅

 • Real-time visibility verified in Splunk dashboards; alerts firing as expected.

## ⏱️ Study time

~6 hours (plus troubleshooting)

## 🧠 Reflection

Today I connected all moving parts into a cohesive monitoring stack. I’m much more comfortable with netplan/static IPs, systemd services, cron, UF configuration, and Splunk field extraction/alerts. The lab now feels like a mini SOC where I can iterate faster on real data.

<img width="1911" height="1067" alt="Captura de pantalla 2025-10-28 135742" src="https://github.com/user-attachments/assets/56b7eb7f-fa90-438b-833b-f254c09b998e" />
<img width="1904" height="1069" alt="Captura de pantalla 2025-10-28 135223" src="https://github.com/user-attachments/assets/6d916c59-c7db-4557-86fa-b19c7ebffd0b" />
<img width="1915" height="1074" alt="Captura de pantalla 2025-10-28 124926" src="https://github.com/user-attachments/assets/7c4443f2-6dfa-4377-bca7-9c85b1e0f677" />
<img width="1917" height="1069" alt="Captura de pantalla 2025-10-28 183223" src="https://github.com/user-attachments/assets/a82c5573-f142-40d8-8020-b474863b9930" />
<img width="1919" height="1067" alt="Captura de pantalla 2025-10-29 154231" src="https://github.com/user-attachments/assets/f5e9b269-7b44-42f0-8e7b-ab4e7aa003bd" />
<img width="1925" height="2160" alt="Captura de pantalla 2025-10-31 135456" src="https://github.com/user-attachments/assets/19fe1e88-ff08-49ec-89b0-10923154fafc" />
<img width="1909" height="1068" alt="Captura de pantalla 2025-10-31 135515" src="https://github.com/user-attachments/assets/677bc69a-e7f5-4ea4-b407-832f0f8803e7" />


## Day 18 - Raspberry Pi network capture workflow
Date: November 1, 2025

Objective:  
Validate Raspberry Pi network capture workflow, verify Splunk log ingestion, and confirm visibility of attack events across the lab network.



### ✅ Accomplished
- Confirmed network topology and IP mapping
  - Windows host (192.168.1.69) running VirtualBox and Ubuntu VM (Splunk 192.168.1.123)  
  - Raspberry Pi (192.168.1.18) configured for periodic packet captures  
  - Kali (192.168.1.125) used for SSH brute-force simulations  
  - Additional Proxmox VMs: Ubuntu 192.168.1.133 + Win10 192.168.1.11  

- Verified Pi capture automation
  - autocapture.sh runs scheduled 1-minute captures via tcpdump
  - Files stored under /home/admin/captures/ with automatic cleanup (1 day)
  - sync_latest_capture.sh automatically transfers newest .pcap to Splunk VM (192.168.1.123)
  - Auto transfer verified: last capture successfully appeared on host without manual copy
  - Duplicated cron entries identified (`/usr/local/bin/` vs `/home/admin/`) — fix planned

- Validated data integrity
  - Downloaded .pcap (`auto_20251029_070001.pcap`) inspected in Wireshark  
  - Confirmed full SSH session visibility, packet retransmissions, and ACKs  
  - Splunk dashboard received and indexed “failed SSH login” events correctly



### ⚙️ Current State
- Raspberry Pi fully operational as a passive network sensor  
- Splunk Enterprise receives correlated host logs and synced captures  
- Automatic data pipeline working end-to-end  
- Environment stable and validated  



### 🚀 Next Steps
1. Remove duplicate cron references (`/usr/local/bin/autocapture.sh`)  
2. Confirm single active schedule at /home/admin/autocapture.sh  
3. Optionally adjust capture interval to every 5 min for higher granularity  
4. Start correlating packet data (Pi) with Splunk SSH auth logs  
5. Begin documenting detection rules for brute-force patterns  



Status: ✅ Stable & Verified   
Focus for Next Session: Cron cleanup + advanced capture scheduling + event correlation  

<img width="1920" height="955" alt="Screenshot from 2025-10-29 14-54-07" src="https://github.com/user-attachments/assets/a0edfc1c-54e6-4a72-8341-f829eb47177e" />
<img width="1920" height="955" alt="Screenshot from 2025-10-29 14-54-55" src="https://github.com/user-attachments/assets/983e2871-2427-4c57-8b5a-d466e0e7c48f" />
<img width="1920" height="923" alt="Screenshot from 2025-10-30 12-10-33" src="https://github.com/user-attachments/assets/86bc5385-bd68-41b8-9ecb-bbbaa524a8f4" />
<img width="1920" height="923" alt="Screenshot from 2025-11-01 12-28-21" src="https://github.com/user-attachments/assets/24385e12-556d-46e6-935e-233a57ae250a" />
<img width="1015" height="890" alt="Screenshot from 2025-11-01 14-09-08" src="https://github.com/user-attachments/assets/7c1ce20b-8c6e-4f6e-bce0-41395ca6f1fc" />



## Day 19 - Network Capture & Analysis Progress 
Date: November 3, 2025

## Main work done:

 • Verified that all systems in the lab (Windows, Kali, Ubuntu, and Raspberry Pi) are correctly connected and sending logs.
 
 • Confirmed Raspberry Pi automatic captures are running and sending .pcap files to the host machine successfully.
 
 • Analyzed several captures manually in Wireshark — including SSH and TCP sessions.
 
 • Learned how to interpret multiple packet types, including retransmissions, encrypted SSH data, and ARP exchanges between devices.
 
 • Practiced step-by-step packet interpretation and wrote down manual notes for deeper understanding.
 
 • Validated that the network remains isolated on a closed router (no WAN or external internet).
 
 • Checked and confirmed correct IP mapping for all devices in the local environment.

## Next focus:
 
 • Study TLS and SSH encryption patterns in detail.
 
 • Capture a full 1-minute encrypted session and analyze the handshake process.
 
 • Continue documenting each protocol behavior in personal notes.

## Result:

All systems are stable and functioning as intended. Packet captures and Splunk logs align correctly. The Raspberry Pi automation works as designed, making the lab fully ready for deeper security traffic analysis.

<img width="1918" height="1075" alt="Captura de pantalla 2025-11-03 122946" src="https://github.com/user-attachments/assets/106d3df0-3982-4711-98e8-9a7189a776f8" />
<img width="1919" height="1074" alt="Captura de pantalla 2025-11-03 155617" src="https://github.com/user-attachments/assets/46db7950-4be1-46e9-8274-7d05492e8109" />


## Day 20 - New day in my Cybersecurity Lab   
Date: Date: November 4, 2025  

Topic: Network Scanning & ARP Analysis

Environment:  
- Kali Linux (Attacker / Scanner)  
- Raspberry Pi (Sniffer running `tcpdump`)  
- Windows / Proxmox host network (.50 target)  
- Wireshark for analysis  



## 🎯 Objective
Simulate and analyze basic network reconnaissance techniques in a safe home lab.  
Today’s focus: detecting ARP sweeps and understanding how they appear in packet captures.



## 🧩 Tasks Performed

### 1. Raspberry Pi Packet Capture Setup
Configured tcpdump for rotating captures:sudo tcpdump -i eth0 -s 0 -U -n \
  -w "/home/admin/captures/test_$(date +%Y%m%d_%H%M%S).pcap" \
  -G 60 -W 60 'tcp[tcpflags] & tcp-syn != 0 or arp'
- Verified continuous rotation of .pcap files
- Confirmed correct timestamps and active interface  
- Checked disk usage and file sizes


### 2. Network Scanning from Kali
Performed local subnet discovery:sudo netdiscover -r 192.168.1.0/24
Observed typical ARP sweep behavior:
- Sequential Who has 192.168.1.x? Tell 192.168.1.125
- Source: Kali VM / Proxmox interface
- Dozens of ARP requests per second



### 3. Wireshark Analysis
Filter used:arp && eth.src == <scanner_mac>
Identified patterns:
- Source repeatedly probing IP range  
- Requests: “Who has 192.168.1.117 … 192.168.1.148”
- Confirms active host discovery  
- Recognized the difference between normal ARP cache traffic vs scanning bursts  


## 🧠 Key Learnings
- How ARP scanning appears in packet captures  
- Difference between broadcast and directed ARP traffic  
- Practical use of tcpdump filters for continuous network monitoring  
- Recognizing scanning behavior from timing and sequence patterns  



## 🧰 Tools Used
| Tool | Purpose |
|------|----------|
| tcpdump | Network capture on Raspberry Pi |
| Wireshark | Deep packet inspection |
| netdiscover | ARP-based host discovery |
| nmap *(planned next)* | TCP SYN & port scanning |


## ✅ Next Steps
- Simulate TCP SYN scan with nmap -sS 192.168.1.50 -p 1-1024  
- Capture and analyze SYN flood patterns  
- Compare ARP sweep vs TCP scan signatures  
- Document results in Day 2 report



📘 *This lab is for educational and ethical testing only, performed on my own isolated network.*

<img width="1919" height="1073" alt="Captura de pantalla 2025-11-04 130755" src="https://github.com/user-attachments/assets/e3e52740-5bf5-4cf3-89dd-fbb4b0c04631" />
<img width="1913" height="1071" alt="Captura de pantalla 2025-11-04 133220" src="https://github.com/user-attachments/assets/2802ffaf-fa76-408d-93ea-0af543f4a544" />
<img width="1919" height="1076" alt="Captura de pantalla 2025-11-04 143810" src="https://github.com/user-attachments/assets/b478009c-7f0d-48d1-a13a-857afae115eb" />
<img width="1913" height="1075" alt="Captura de pantalla 2025-11-04 202124" src="https://github.com/user-attachments/assets/43f77a1b-6ed6-4669-8bd6-711b7cfe32df" />
<img width="1919" height="1071" alt="Captura de pantalla 2025-11-04 223319" src="https://github.com/user-attachments/assets/3276e71e-2246-4d31-b1ce-9442ed809626" />


## Day 21 — Network Scanning & Troubleshooting Lab  

Date: November 5, 2025
  

## 🔧 Summary
Today’s session focused on end-to-end troubleshooting of my home lab connectivity, followed by network discovery, scanning, and traffic capture analysis.  
I confirmed my monitoring setup works correctly and successfully identified SYN scan and ARP broadcast patterns in Wireshark.

---

## 🧠 Main Activities
1. Troubleshooting network and repeater issue  
   - Server lost Internet connectivity (no ping to 8.8.8.8).  
   - Diagnosed issue using ip a, ip route, and ethtool.  
   - Found problem in my Wi-Fi repeater not passing wired traffic.  
   - Reset repeater → restored connectivity and verified with ping test.  

2. Verifying lab systems  
   - Started Proxmox server, Kali attacker VM, Raspberry Pi capture node, and Windows host.  
   - Checked communication between devices — confirmed all reachable via ping.  

3. Network discovery and scanning  
   Executed from Kali:  
   sudo netdiscover -r 192.168.1.0/24
   sudo nmap -sn 192.168.1.0/24
   nmap -sS -p 1-100 192.168.1.10
   sudo nmap -sV 192.168.1.50
     
   - Observed host discovery packets (ARP + ICMP).  
   - Detected SYN packets from my Kali to multiple hosts.  

4. Packet capture on Raspberry Pi  
   - Manual capture command:  
         sudo tcpdump -i eth0 -w "/home/admin/captures/test_$(date +%Y%m%d_%H%M%S).pcap" -G 60 -W 1
       
   - Transferred PCAPs to host using:  
         scp /home/admin/captures/*.pcap user@host:/path/to/store/
       

5. Wireshark analysis  
   - Opened captures from Pi and analyzed them using display filters:  
         tcp.flags.syn == 1 && tcp.flags.ack == 0
     tcp.flags.reset == 1
     icmp.type == 3
     arp.opcode == 1
       
   - Identified SYN scan activity and ARP broadcasts consistent with host discovery tools.  
   - Verified port scanning pattern from 192.168.1.125 (Kali) to 192.168.1.10, .12, .50.  
   - Observed RST,ACK replies → confirmed closed ports.  
   - Captured ICMP “Destination Unreachable” messages from the gateway during scanning.  


## 📁 Artifacts Collected
- PCAPs:  
  - scan_test2.pcap  
  - scan_test3.pcap  
  - auto_20250909_*.pcap  
- Screenshots:  
  - ARP flood sequence (`Who has 192.168.1.x Tell 192.168.1.1`).  
  - SYN/RST exchange pattern.  
  - ICMP unreachable alerts.  
  - Server interface outputs (`ip a`, ethtool, `ip route`).  

## 🧩 Interpretation
- Network discovery: Repeated ARP requests indicate local subnet enumeration.  
- SYN activity: High rate of SYNs from Kali shows active scanning (reconnaissance).  
- RST/ACK patterns: Closed ports on scanned hosts respond immediately.  
- Connectivity fix: Restoring repeater functionality returned full routing to the Internet.  


## 🧰 Useful Commands

# Show link state of all interfaces
ip a

# Display routing table
ip route

# Check if Ethernet link is detected
sudo ethtool eno2 | grep "Link detected"

# Start capture (rotate every 60s, 1 file)
sudo tcpdump -i eth0 -w "/home/admin/captures/test_$(date +%Y%m%d_%H%M%S).pcap" -G 60 -W 1

# Quick copy of captures to host
scp /home/admin/captures/*.pcap user@192.168.1.:/captures/


## 🧠 Lessons Learned
- Always verify physical links and repeater/switches first during connectivity issues.  
- Using Wireshark filters effectively narrows analysis to useful packets.  
- SYN scan behavior can be visually confirmed via RST/ACK sequences.  
- ARP bursts are normal during scanning but can flood the network under heavy discovery.  


## 🚀 Next Steps
1. Reproduce today’s scan and build a Suricata rule to detect multiple SYNs per second.  
2. Extend capture automation on Raspberry Pi with cron + rotation.  
3. Document a new lab for brute-force login detection using Hydra and Wireshark.  
4. Start preparing visual report templates for GitHub (screenshots + PCAP metadata).  

<img width="1914" height="1075" alt="Captura de pantalla 2025-11-05 133511" src="https://github.com/user-attachments/assets/00b12385-c26a-4f74-b1d2-6755d84df309" />
<img width="1913" height="1075" alt="Captura de pantalla 2025-11-05 133622" src="https://github.com/user-attachments/assets/ae4c0fad-1cd3-4249-9a14-117014d8025b" />
<img width="1911" height="1075" alt="Captura de pantalla 2025-11-05 134649" src="https://github.com/user-attachments/assets/3c9de903-9b4b-48f4-8898-8b7c68b8e79f" />
<img width="1911" height="1070" alt="Captura de pantalla 2025-11-06 111402" src="https://github.com/user-attachments/assets/7b9249e8-5432-484c-84c8-4930af8f72ec" />
<img width="1917" height="1077" alt="Captura de pantalla 2025-11-06 112504" src="https://github.com/user-attachments/assets/fffc566c-9117-45ff-b6b6-859774301ff9" />


### Day 22 — TryHackMe: Cyber Security 101 — Study log

Date: November 7, 2025

### Continued TryHackMe Cyber Security 101 learning path — focused on core SOC fundamentals, SIEM basics, and hands-on labs exploring event triage and log investigation.  
What I did:  
- Completed several THM rooms covering Splunk basics, alert triage, and log interpretation.  
- Practiced Splunk searches and basic triage workflows inside THM exercises.  
Artifacts / notes: No new captures taken today — focused on THM labs and review.  
Next steps: Return to home lab tomorrow, power up systems, and run controlled reconnaissance tests (nmap) to generate traffic for capture and analysis.

###  Day 23 — TryHackMe: Cyber Security 101 + quick Wireshark lab

Date: November 8, 2025
  
Activity: Continued THM SOC 101 path; ran quick attacker tests in my isolated home lab and performed packet analysis.  

## What I did in THM:  
- Completed additional SOC 101 rooms (incident prioritization, threat hunting fundamentals).  
What I did in lab:  
- Powered up lab: Proxmox, Kali (192.168.1.125), victim PC (192.168.1.50), Splunk host (192.168.1.123), Raspberry Pi capture (192.168.1.18).  
- Ran recon & credential tests from Kali: nmap -sS / -A and 7-8-10-1SSH attempts (controlled).  
- Saved the PCAP (`scan_test*.pcap`) from the Pi, copied it to the Splunk host, and spent ~1:15 analyzing packets in Wireshark (SYN scans, ARP sweeps, ICMP responses).  
Findings: Observed ARP sweeps, SYN scans (SYN→RST patterns), ICMP port unreachable (UDP probes) and repeated SSH attempts consistent with a brute-force test.  
Artifacts: screenshots (Wireshark), pcap files (saved on Splunk host).  
Next steps: Export filtered evidence pcaps, map detections to MITRE ATT&CK, and begin turning detections into Splunk saved searches.

###  Day 24 — TryHackMe: Cyber Security 101 — Study log

Date: 2025-11-10

### Started focused SOC 1 Analyst path work on TryHackMe; practiced more real-world detection and triage scenarios.  

## What I did:  
- Completed THM rooms specific to SOC analyst tasks: alert triage, basic threat hunting queries, and simple incident write-ups.  
- Re-read my recent Wireshark findings and matched packet evidence to THM lessons to strengthen understanding.  
Artifacts / notes: THM progress screenshot and notes added to my study log.  
Next steps: Plan a set of controlled attack scenarios in the lab (DNS tunneling & HTTP C2 simulation) and capture traffic for Splunk detection development.

###  Day 25 — TryHackMe: Cyber Security 101 — Certificate achieved + lab follow-up

Date: November 11, 2025
 
## Activity: Finished the TryHackMe Cyber Security 101 learning path (certificate achieved); continued lab work and documentation.  
What I did:  
- Completed final THM labs required for the Cyber Security 101 learning path and downloaded my certificate.  
- Continued analysis of lab captures and prepared evidence for GitHub (pcaps, Wireshark screenshots and prepared Splunk search snippets).  
Artifacts: TryHackMe Certificate saved (certificate image/PDF), Wireshark screenshots, scan_test*.pcap.  v 7-8-10-11 GitHUStart the planned attack simulations in the lab (DNS tunneling, HTTP C2) and develop Splunk alerts/dashboards to detect them. Add Wazuh agents next to correlate host telemetry with network detections.

## Day 26 — Network Traffic Analysis: DNS Tunneling, Port Scanning & C2 Investigation

Date: November 12, 2025

## Summary:
Today I focused on analyzing previously captured network traffic (pcap files) from my isolated SOC home lab. My goal was to identify different attacker behaviors that I executed earlier from my Kali machine and verify how they appear in Wireshark. I also checked why DNS tunneling traffic started failing and why the ICMP “Destination Unreachable” messages appeared.

## 🔍 1. DNS Tunneling Traffic Review

I analyzed the DNS packets generated during the iodine DNS tunneling test.
Findings:
 • Multiple DNS queries contained the same structure used by iodine, including:
 • Long encoded subdomain labels
 • Repetitive query patterns
 • High-frequency queries
 • Several responses were labeled as:
 • Unknown operation
 • Malformed Packet
 • This is expected when DNS tunneling tools encode data into DNS payloads.

## Observation:
Later in the capture, DNS queries suddenly triggered ICMP Type 3 Code 3: Port Unreachable from the target (192.168.1.125).
This means:
 • The DNS server port (UDP 53) stopped responding
 • or DNS listener closed
 • or iodine server side wasn’t running anymore

This explains why tunneling worked earlier but stopped afterwards.

## 🕵️ 2. Brute Force & Port Scanning Visibility

In another section of the capture, I reviewed:

✔️ Brute Force Attempts
 • Traffic targeting SSH service
 • Repeated and sequential login attempts from my Kali machine
 • Clear pattern of automated authentication failures
 • Matches expectations of a dictionary attack

✔️ Port Scan Traffic

Large number of SYN packets from 192.168.1.125 → 192.168.1.80 and other hosts:
 • SYN sweeping across hundreds of ports
 • No 3-way handshake (classic Nmap scan)
 • Very fast sequence timestamps → automated reconnaissance
 • Visible payload sizes (66 bytes) consistent with SYN packets

Conclusion:
Wireshark clearly shows traditional scanning behavior, great for demonstrating detection skills.

## 🌐 3. ARP Activity & Network Enumeration

I also analyzed ARP-related traffic:
 • Massive list of “Who has IP → Tell 192.168.1.125” messages
 • Even some messages showing “duplicate use of 192.168.1.1 detected!”
 • This happens during ARP scanning (ARP sweep)

This confirms that ARP-based host discovery works and is fully visible in the mirrored capture.

## 🧭 4. C2 (Command & Control) Investigation

I began checking how simulated C2 traffic appears:
 • The HTTP section of the capture showed many HTTP 303 See Other redirects
 • Interesting outbound HTTP requests from 192.168.1.69 (victim) to external-looking IP 4.3.2.1
 • This traffic is likely from the C2 simulation test I started

Next steps:
I will analyze:
 • Which domain resolves to 4.3.2.1
 • Whether this is beaconing, redirect abuse, or normal web behavior
 • Extract the HTTP stream for deeper analysis

## 📌 Overall Conclusion

Yesterday’s traffic review successfully confirmed visibility of:
 • ✔️ DNS tunneling
 • ✔️ Brute force patterns
 • ✔️ TCP SYN port scans
 • ✔️ ARP sweeping
 • ✔️ HTTP traffic useful for C2 simulation


Next steps:
 1. Build Splunk detection logic for DNS tunneling + brute force
 2. Continue HTTP-based C2 simulation
 3. Compare results in Wireshark vs. Splunk dashboards



## Day - 27 Home Lab – Network Attack Simulation & Traffic Analysis 

Date: 13 

Today I conducted four different offensive techniques in my isolated SOC home lab and captured all traffic using my Raspberry Pi (monitoring port-mirrored traffic via tp-link switch). My attacker was Kali Linux, the victim was Ubuntu, and all results were analyzed later in Wireshark.

## 1️⃣ Port Scanning

I performed a wide TCP SYN scan from Kali (192.168.1.125) against the victim Ubuntu machine (192.168.1.50).
Result in Wireshark:
 • Clear SYN flood patterns
 • Ports responding with RST or SYN/ACK
 • Many red packets → port closed
 • Normal behavior for Nmap SYN scan

This confirmed visibility of reconnaissance activity.

## 2️⃣ Brute-Force Attack

I simulated SSH brute force login attempts from Kali to the victim using Hydra.
Result in Wireshark:
 • High volume of SSH2 “Key Exchange Init”
 • Repeated encrypted packets
 • Login failures visible in /var/log/auth.log (Splunk indexed them)

This successfully created brute-force artifacts for SIEM detection.

## 3️⃣ DNS Tunneling

I simulated exfiltration-like DNS tunneling by sending a file from the victim to Kali’s DNS server.

Result in Wireshark:
 • Long, unusual DNS queries
 • Random-looking subdomains
 • “Malformed Packet” alerts
 • NXDOMAIN and unusual query sizes

Exactly the kind of strange DNS activity analysts detect when spotting tunneling.

## 4️⃣ HTTP C2 Beacon

I deployed a very simple custom HTTP Command & Control setup:
 • Kali runs the C2 python server
 • Ubuntu runs a beacon loop that checks for commands every 10 seconds

Result in Wireshark:
 • Clean HTTP GET → POST pattern
 • Text/plain commands
 • Visible heartbeat beaconing behavior
 • Easy to identify periodic callback traffic

This created realistic C2-like behavior for SOC investigations.

⸻

Final Notes

All traffic was captured via my Raspberry Pi sniffer, stored as .pcap files, and analyzed in Wireshark.
This session helped me understand how each attack type looks at the packet level and prepares me to build Splunk detections for recon, brute-force, DNS tunneling, and C2 activities.


14 November 

## Day  — Zeek + Splunk Integration Day

Today’s session was fully focused on integrating Zeek network monitoring with Splunk Enterprise inside my isolated SOC home lab. This was one of the most complex and technical days so far, involving troubleshooting, configuration, log ingestion tuning, and validation.

## 🔧 1. Zeek Installation & Troubleshooting on Raspberry Pi
 • Installed Zeek manually on Raspberry Pi 4B (8GB).
 • Fixed multiple issues related to:
 • zeekctl not starting
 • missing state.db
 • wrong permissions on /usr/local/zeek/logs/current
 • Created missing log directories and applied correct ownership/permissions.
 • Successfully ran Zeek in standalone mode:

Verified packet capture by generating ICMP traffic (ping tests).


## 📁 2. Zeek Log Generation Validation

After fixing the file structure and permissions, Zeek finally started generating logs:
 • conn.log
 • dns.log
 • http.log
 • weird.log
 • packet_filter.log
 • telemetry.log
 • and others…

These files appeared correctly inside:

This confirmed that Zeek was processing real traffic on the mirrored network port.


## 🔗 3. Splunk Universal Forwarder on Raspberry Pi
 • Verified that the Splunk Forwarder was running and connected to my Splunk indexer:

• Cleaned the configuration so only valid monitored files remained.
 • Added Zeek log directory to Forwarder monitoring:

 • Confirmed that Splunk Forwarder recognizes the monitored log paths.


## 📊 4. Zeek Logs Successfully Ingested Into Splunk

Finally, confirmed in Splunk Web that Zeek logs were arriving:

Received:
 • DNS events
 • Connection events
 • Telemetry events
 • Other Zeek logs

This proves the entire data pipeline from Raspberry Pi → Zeek → Splunk Forwarder → Splunk Indexer → Search was working.


## 🎯 5. End of Day Results

Today I achieved one of the biggest milestones in my SOC home lab:

✔️ Zeek fully functional on Raspberry Pi
✔️ Real-time packet analysis working
✔️ Splunk Forwarder correctly configured
✔️ Zeek logs forwarded into Splunk in real time
✔️ Validated multiple log sources (DNS, conn, telemetry, etc.)
✔️ Prepared to build Zeek dashboards and detections

This setup now allows me to perform:
 • Network forensics
 • Threat hunting
 • C2 traffic detection
 • DNS tunneling detection
 • HTTP anomaly analysis
 • And full packet-behavior investigation

A huge upgrade for my SOC learning environment.


### Day - X  — lab session
Date: November 15, 2025

## Summary:  
Today I focused on integrating Zeek on the Raspberry Pi with my Splunk indexer. I got Zeek running on eth0, added the Zeek log folder to the Splunk Universal Forwarder, and verified Zeek logs (conn, dns, http, telemetry, weird) are indexed in Splunk. I also simulated a few attacks (DNS-based exfil patterns and TCP/SSH scans) and verified they appear in both Zeek logs and Splunk searches.

## Issues / notes:
- Pi time was behind (NTP not reachable in offline lab). Fixed by enabling NTP (when network available) or manually setting clock.
- NIC checksum offloading triggers Zeek warnings; acceptable for now (can run zeek -C or disable offload to remove warnings).

## Next: add more monitors, run iodine DNS-tunnel and HTTP C2 simulations, build a Splunk dashboard for Zeek detections.
