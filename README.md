# Work-with-Splunk

## Day 1 Checked all connection and functionality 
Have to check everything and make some configurations after that going to creat some events on Windows pc to see if everything works fine on Ubuntu and i can read logs. Let's rock

Faced with a couple errors i guess the reason was my antivirus wich was blocked partly connect between two computers.Everything was solved after on my windows pc through the powershall i made a folder and txt document in spluk directory through this file o power shall command i can send different events on my host ubuntu VM. Sent 1 event first after 10 and 100 with different marks Error, Info etc.

Also created a txt file with all commands that i need to check and maintain Windows and Ubuntu when i start working with splunk.

<img width="1920" height="923" alt="Screenshot from 2025-09-27 12-38-36" src="https://github.com/user-attachments/assets/b0900b6f-81d7-430c-a73d-2fecbaaead8f" />
<img width="1025" height="910" alt="Screenshot from 2025-09-27 12-55-11" src="https://github.com/user-attachments/assets/d871db26-7ee2-4201-b39e-78f2623539d0" />
<img width="1920" height="923" alt="Screenshot from 2025-09-27 12-45-01" src="https://github.com/user-attachments/assets/59a0584b-834c-410b-a45b-f300433a3686" />



## Day 2  Splunk Home Lab - Event Monitoring & Alerts
Was testing around 4 hours how everything works. Learning how to work with Splunk web.

1️ Machine Connectivity
- Connected multiple machines in a closed network.
- Verified that events are sent and received correctly between machines.
- Ensured proper data flow to Splunk indexes for monitoring.

2️ Log Generation & Analysis
- Generated 3,000–4,000 simulated log events with levels INFO, WARN, ERROR.
- Logs uploaded to Splunk and each event verified.
- Extracted important fields using rex.

3 Created alerts and learned how to save cvs files


<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 123405" src="https://github.com/user-attachments/assets/2bea63a8-8a1e-4e7b-9128-5dea1bcccbf7" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 140459" src="https://github.com/user-attachments/assets/619071f7-cb32-4b24-b008-f78497a1b11f" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 140250" src="https://github.com/user-attachments/assets/4f30c3e5-ad4f-4e93-958d-9aa3306b7f98" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 125852" src="https://github.com/user-attachments/assets/db316be7-4213-4710-b737-5f6c21ea306b" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 124025" src="https://github.com/user-attachments/assets/8f363536-d402-49b3-923c-fd8cc9da1315" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 155801" src="https://github.com/user-attachments/assets/5450a37f-b098-4de9-8e21-7d7bdae49cec" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 155316" src="https://github.com/user-attachments/assets/44ea47af-0b7c-464d-9b15-f9dc780a8c47" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 154930" src="https://github.com/user-attachments/assets/6a502b2d-5397-4efe-b916-7624e8194afc" />


## Day 3 Splunk Installation Failure on Windows

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



## Day 4 Practice fully on Ubuntu

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

