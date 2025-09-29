# Work-with-Splunk

Day 1 
Have to check everything and make some configurations after that going to creat some events on Windows pc to see if everything works fine on Ubuntu and i can read logs. Let's rock

Faced with a couple errors i guess the reason was my antivirus wich was blocked partly connect between two computers.Everything was solved after on my windows pc through the powershall i made a folder and txt document in spluk directory through this file o power shall command i can send different events on my host ubuntu VM. Sent 1 event first after 10 and 100 with different marks Error, Info etc.

Also created a txt file with all commands that i need to check and maintain Windows and Ubuntu when i start working with splunk.

<img width="1920" height="923" alt="Screenshot from 2025-09-27 12-38-36" src="https://github.com/user-attachments/assets/b0900b6f-81d7-430c-a73d-2fecbaaead8f" />
<img width="1025" height="910" alt="Screenshot from 2025-09-27 12-55-11" src="https://github.com/user-attachments/assets/d871db26-7ee2-4201-b39e-78f2623539d0" />
<img width="1920" height="923" alt="Screenshot from 2025-09-27 12-45-01" src="https://github.com/user-attachments/assets/59a0584b-834c-410b-a45b-f300433a3686" />


Day 2 

# 🖥️ Splunk Home Lab - Event Monitoring & Alerts

![Splunk Logo](https://upload.wikimedia.org/wikipedia/commons/5/55/Splunk_logo.png)

## 📖 Overview
This project is a personal home lab designed to practice Splunk monitoring, log analysis, and alerting.  
All work is done on Ubuntu VMs and multiple machines connected in a local network.  

The lab contains: logs, CSVs, screenshots, and documentation of exercises performed.

---

## 1️⃣ Machine Connectivity
- Connected multiple machines in a closed network.
- Verified that events are sent and received correctly between machines.
- Ensured proper data flow to Splunk indexes for monitoring.

---

## 2️⃣ Log Generation & Analysis
- Generated 3,000–4,000 simulated log events with levels INFO, WARN, ERROR.
- Logs uploaded to Splunk and each event verified.
- Extracted important fields using rex:

```spl
index=simulated_logs
| rex "(?<level>\w+)\s+(?<msg>.+)"
| stats count by level
