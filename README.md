# 🛡️ Home SOC Lab: Threat Detection & Incident Response using Wazuh SIEM

## 📌 Executive Summary
This project demonstrates the deployment of a virtual Security Operations Center (SOC) home lab designed to detect, analyze, and respond to simulated cyber threats in real-time. Using **Wazuh SIEM** integrated with **Windows Sysmon**, the environment actively logs, correlates, and alerts on malicious activities generated from a **Kali Linux** attacker machine.

---

## 📐 Network Architecture
The environment is configured within an isolated virtual network (NAT Network):

* **SIEM Server:** Wazuh Manager & Dashboard (Ubuntu) — `192.168.1.10`
* **Victim Endpoint:** Windows 10 with Wazuh Agent & Sysmon — `192.168.1.15`
* **Attacker Machine:** Kali Linux — `192.168.1.20`

---

## 🛠️ Tools & Technologies Used
* **SIEM & XDR:** Wazuh Dashboard, Wazuh Indexer
* **Endpoint Telemetry:** Microsoft Sysmon, Windows Event Logs
* **Attack Simulation:** Kali Linux (Hydra, Nmap)
* **Virtualization:** Oracle VirtualBox

---

## 🚀 Lab Implementation Steps

### Phase 1: Infrastructure Setup
1. Configured an isolated NAT network on VirtualBox.
2. Deployed the Wazuh OVA appliance and verified dashboard connectivity.
3. Installed and connected the Wazuh Agent on the Windows 10 target.

### Phase 2: Telemetry Enrichment (Sysmon Integration)
1. Deployed Microsoft Sysmon on Windows 10 using SwiftOnSecurity's configuration.
2. Updated `ossec.conf` on the agent to collect Sysmon event logs (Process Creation, Network Connections).

### Phase 3: Attack Simulation & Detection
1. Executed an RDP Brute Force attack from Kali Linux using `Hydra`:
   ```bash
   hydra -l Administrator -P /usr/share/wordlists/rockyou.txt rdp://192.168.1.15
