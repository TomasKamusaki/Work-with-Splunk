# Work-with-Splunk

## Day 1 - Checked all connections and functionality 
Have to check everything and make some configurations after that going to creat some events on Windows pc to see if everything works fine on Ubuntu and i can read logs. Let's rock

Faced with a couple errors i guess the reason was my antivirus wich was blocked partly connection between two computers.Everything was solved after on my windows pc through the powershall i made a folder and txt document in spluk directory through this file o power shall command i can send different events on my host ubuntu VM. Sent 1 event first after 10 and 100 with different marks Error, Info, Warn.

Also created a txt file with all commands that i need to check and maintain Windows and Ubuntu when i start working with splunk.

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

## Day 5 - SSH,events, more practice

During today’s session, I continued practicing with Splunk by setting up a functional lab environment using my physical Ubuntu machine as the forwarder and my Ubuntu VM (hosted on Windows) as the Splunk indexer. I verified network connectivity, configured ports and firewalls, and ensured proper forwarding between the two systems.

I generated different types of custom log events (INFO, WARN, and ERROR) and sent them to Splunk for indexing. After confirming their ingestion, I set up alerts based on specific event types to simulate security monitoring scenarios. Additionally, I began working with Dashboards, creating visual representations of the data to improve analysis capabilities.

I also explored sending SSH connection logs, alerting on connection errors, and visualizing this data in real time. This helped reinforce essential SOC skills like log collection, event classification, alerting, and visualization — all crucial for incident detection and response workflows.

<img width="1920" height="922" alt="Screenshot from 2025-10-02 12-20-43" src="https://github.com/user-attachments/assets/c10a84bf-cd62-46e0-b761-ad8727fc1147" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 12-47-40" src="https://github.com/user-attachments/assets/80aeeb0e-1698-4868-8832-a41dd7278376" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 13-31-13" src="https://github.com/user-attachments/assets/3c020aa0-3814-4412-90e6-fa0d9e9a595c" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 13-48-49" src="https://github.com/user-attachments/assets/70b8344c-1441-4cfd-b6c3-ba7212cd141f" />
<img width="1920" height="922" alt="Screenshot from 2025-10-02 13-53-51" src="https://github.com/user-attachments/assets/9b1011f7-8ab0-499e-b0e6-a5eddaf06198" />
<img width="1920" height="923" alt="Screenshot from 2025-10-06 15-01-07" src="https://github.com/user-attachments/assets/c73cfbde-483a-4e14-8d25-3fa846f88f35" />
<img width="1920" height="923" alt="Screenshot from 2025-10-06 15-30-52" src="https://github.com/user-attachments/assets/d92c9421-b811-4957-91ab-a0fb66e30862" />
<img width="1920" height="923" alt="Screenshot from 2025-10-06 15-36-10" src="https://github.com/user-attachments/assets/47be3a54-0c19-4410-bf81-62af176eb315" />


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

⸻

Next Steps / To-Do
 • Extend dashboards for error/warn/info logs
 • Test alerts by generating more SSH failed login events
 • Explore additional SPL commands: timechart, top, where
 • Simulate public IPs to enable geolocation mapping in dashboards
