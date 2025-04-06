# 🛡️ Building a Cloud Honeynet + SOC in Azure (Single Windows VM, Live Traffic)

This project demonstrates how I created a lightweight honeynet using a **single Windows virtual machine** in **Microsoft Azure**, integrated logs into **Microsoft Sentinel**, and analyzed real-world attack traffic. I monitored the environment before and after applying security controls to highlight the effectiveness of basic hardening techniques.

---

## 📄 Overview

- Deployed a single public-facing **Windows Server VM** to act as a honeypot.
- Forwarded Windows Event Logs to **Microsoft Sentinel** via **Log Analytics Workspace**.
- Captured and analyzed malicious activity for 24 hours.
- Hardened the environment and continued monitoring for another 24 hours.
- Compared results before and after implementing security controls.

---

## ☁️ Architecture

### 📝 Before Hardening

- Windows Server VM exposed to the internet.
- All ports open (including RDP, SMB, etc.).
- No NSG restrictions or built-in firewall enabled.
- Logs collected using **Azure Monitor Agent** into **Log Analytics**.
- Microsoft Sentinel connected for alerting and incident management.

### 🔒 After Hardening

- NSG configured to allow **only my admin IP** over RDP.
- Windows Firewall enabled and locked down.
- Logging and alerting continued post-hardening.
- RDP brute-force and other traffic dropped at the network edge.

---

## 🧰 Components Used

- Microsoft Azure
- Microsoft Sentinel
- Log Analytics Workspace
- Windows Server Virtual Machine
- Network Security Group (NSG)
- Azure Storage Account (for diagnostics)

---

## 📊 Metrics

### 📅 Before Security Controls (24 Hours)

> **Start:** 2025-03-17 14:51:07  
> **End:** 2025-03-18 14:51:07

| Metric                     | Count   |
|---------------------------|---------|
| `SecurityEvent` (Event Log)       | 21,923  |
| `SecurityAlert` (Sentinel)       | 4       |
| `SecurityIncident` (Sentinel)    | 279     |
| `AzureNetworkAnalytics_CL` (NSG Logs) | 1,360   |

---

### 📅 After Security Controls (24 Hours)

> **Start:** 2025-03-23 02:15:29  
> **End:** 2025-03-24 02:15:29

| Metric                     | Count   |
|---------------------------|---------|
| `SecurityEvent`           | 9,186   |
| `SecurityAlert`           | 0       |
| `SecurityIncident`        | 0       |
| `AzureNetworkAnalytics_CL`| 0       |

---

## 🗺️ Attack Visualizations

**Before Hardening:**

- Brute-force RDP attempts detected via `Event ID 4625` (failed logins).
- Numerous authentication failures on port 3389 (RDP).
- NSG logs showed repeated access attempts from malicious IPs.

**After Hardening:**

- All suspicious traffic was blocked by NSG/firewall.
- No successful authentication or active threats detected.

---

## ✅ Conclusion

This project shows that **even one publicly exposed VM** can be a target for attackers. After enabling just a few basic controls—NSG rules, firewall, and access restrictions—the volume of malicious traffic and generated incidents dropped to zero.

I used Microsoft Sentinel's detection capabilities, custom KQL queries, and Azure monitoring tools to:
- Detect and respond to real-world threats
- Analyze login attempts and traffic patterns
- Visualize impact of hardening steps

---

## 🧠 Key Learnings

- How to create a honeypot using a single Windows VM
- Configuring NSGs and Windows Firewall for basic security
- Collecting and analyzing logs using Log Analytics and Sentinel
- Real-world attack data is easy to capture, even in test environments

---

## ⏳ Next Steps

- Add PowerShell monitoring for lateral movement or privilege escalation
- Automate response with Sentinel Playbooks
- Expand honeynet with additional fake services or traps (like port 21/80/445)
- Try using third-party threat intelligence in Sentinel rules

---

## 📸 Screenshots *(Optional)*

- Sentinel dashboard with RDP brute-force alerts
- Event Viewer logs (ID 4625 and 4624)
- NSG Flow Logs showing dropped/allowed traffic
- Pre/post hardening attack maps

---

## 📁 Repo Structure *(Optional)*


