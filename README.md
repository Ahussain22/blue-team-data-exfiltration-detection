# 🔍 Blue Team Lab: Detecting Data Exfiltration via File Access Logs

## 📌 Objective
This lab demonstrates how to detect potential data exfiltration activity by monitoring file access events using Windows Event Viewer.

---

## 🧠 Scenario
An attacker or insider attempts to copy sensitive data from a system to another location. The goal is to detect this behaviour using system logs.

---

## 🧪 Steps Performed

### 1. Created a Sensitive File
A file named `secret.txt` was created on the Desktop containing confidential information.

---

### 2. Enabled File Auditing

File system auditing was enabled using:

```powershell
auditpol /set /subcategory:"File System" /success:enable
```

Auditing was then configured on the file to monitor read/write access via:

- Right-click file → Properties  
- Security → Advanced → Auditing  
- Add → Select “Everyone”  
- Tick Read & Write  

---

### 3. Simulated Data Exfiltration

The file was copied to another directory:

```powershell
Copy-Item "C:\Users\vboxuser\Desktop\secret.txt.txt" -Destination "C:\Temp\stolen.txt"
```

---

### 4. Log Analysis

Event Viewer was used to identify suspicious activity:

```
Event Viewer → Windows Logs → Security
```

Filtered for:

```
Event ID: 4663
```

---

## 🔍 Key Findings

- Event ID **4663** was generated  
- The file `secret.txt.txt` was accessed  
- The user `vboxuser` performed the action  
- The activity occurred at the time of the file copy  

---

## 🚨 Detection Insight

A sequence of file access events involving sensitive data may indicate potential data exfiltration activity, especially when files are copied to new locations.

---

## 💡 Real-World Relevance

Attackers and malicious insiders often copy sensitive files before exfiltrating them. Monitoring file access logs provides visibility into this behaviour.

---

## 🛡️ Mitigation Strategies

- Enable file auditing on sensitive directories  
- Monitor Event ID **4663** regularly  
- Restrict access to critical files  
- Implement Data Loss Prevention (DLP) solutions  

---

## ✅ Conclusion

This lab demonstrates how enabling file auditing and analysing security logs can help detect early signs of data exfiltration.
