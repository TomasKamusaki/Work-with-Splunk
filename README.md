# Work-with-Splunk

Day 1 
Have to check everything and make some configurations after that going to creat some events on Windows pc to see if everything works fine on Ubuntu and i can read logs. Let's rock

Faced with a couple errors i guess the reason was my antivirus wich was blocked partly connect between two computers.Everything was solved after on my windows pc through the powershall i made a folder and txt document in spluk directory through this file o power shall command i can send different events on my host ubuntu VM. Sent 1 event first after 10 and 100 with different marks Error, Info etc.

Also created a txt file with all commands that i need to check and maintain Windows and Ubuntu when i start working with splunk.

<img width="1920" height="923" alt="Screenshot from 2025-09-27 12-38-36" src="https://github.com/user-attachments/assets/b0900b6f-81d7-430c-a73d-2fecbaaead8f" />
<img width="1025" height="910" alt="Screenshot from 2025-09-27 12-55-11" src="https://github.com/user-attachments/assets/d871db26-7ee2-4201-b39e-78f2623539d0" />
<img width="1920" height="923" alt="Screenshot from 2025-09-27 12-45-01" src="https://github.com/user-attachments/assets/59a0584b-834c-410b-a45b-f300433a3686" />


Day 2  Splunk Home Lab - Event Monitoring & Alerts

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

<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 140459" src="https://github.com/user-attachments/assets/308ffac9-54dd-43cf-911f-4b1dc0036a61" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 140250" src="https://github.com/user-attachments/assets/18c4c670-ecaa-4b69-9a5f-af00f2679b13" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 125852" src="https://github.com/user-attachments/assets/0a1afd7c-7ae7-4130-9e9c-4be5a0d0e508" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 124025" src="https://github.com/user-attachments/assets/8e7f91e6-ce47-4981-9188-a2626fdf178b" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 123405" src="https://github.com/user-attachments/assets/91376a7c-95f9-4b36-aa34-fcd258f1ed30" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 155801" src="https://github.com/user-attachments/assets/1d001f44-7002-4cc8-a1ad-e5eb1aed7ca3" />
<img width="1920" height="1080" alt="Captura de pantalla 2025-09-29 155316" src="https://github.com/user-attachments/assets/9c4f3eb3-d5a1-4047-a95a-20b0b8ad4e82" />
