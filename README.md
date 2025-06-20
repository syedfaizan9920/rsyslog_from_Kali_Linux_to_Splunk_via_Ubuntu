# 🚀 Multi-Hop Log Forwarding with rsyslog: From Kali Linux to Splunk via Ubuntu

A complete guide to setting up **multi-hop log forwarding** using `rsyslog` — where logs from **Kali Linux** are forwarded to a **Splunk Enterprise Server**, passing through an intermediate **Ubuntu forwarder**. Ideal for **SOC environments**, **SIEM pipelines**, and **centralized monitoring**.

---

## 🧭 Architecture Overview

Kali Linux (Log Source)
↓
Ubuntu Server (Forwarder)
↓
Splunk Enterprise Server (Collector)


---

## 🎯 Project Goals

✅ Forward logs from Kali Linux to Ubuntu  
✅ Ubuntu forwards logs to Splunk Enterprise  
✅ Enable persistent monitoring of `/var/log/syslog`  
✅ Use Splunk Universal Forwarder (UF) for live forwarding  
✅ SOC-ready log pipeline with rsyslog

---

## ⚙️ Technologies Used

- 🐧 Kali Linux & Ubuntu Server  
- 🔁 rsyslog (multi-hop config)  
- 📡 Splunk Universal Forwarder (UF)  
- 📊 Splunk Enterprise Server  
- 🔐 TCP/UDP protocols (port 514 & 9997)

---

## 📦 Prerequisites

- Linux systems (Kali, Ubuntu)  
- Splunk Enterprise installed  
- Ports 514 (rsyslog) and 9997 (Splunk) open  
- `rsyslog` and Splunk UF installed

---

## 🚀 Step-by-Step Setup

### 🧱 Step 1: Install rsyslog

On Kali & Ubuntu:
```bash
sudo apt update
sudo apt install rsyslog -y

🔁 Step 2: Configure Splunk Server to Receive Logs

sudo nano /etc/rsyslog.conf
Enable TCP & UDP:
module(load="imudp")
input(type="imudp" port="514")

module(load="imtcp")
input(type="imtcp" port="514")

🌐 Step 3: Forward Logs from Ubuntu → Splunk
*.* @@<SPLUNK_SERVER_IP>:514

Restart:
sudo systemctl restart rsyslog

📥 Step 5: Install Splunk Universal Forwarder on Ubuntu

wget -O splunkforwarder.deb "https://download.splunk.com/products/universalforwarder/releases/9.2.0/linux/splunkforwarder-9.2.0-xxxxxxx.deb"
sudo dpkg -i splunkforwarder.deb
cd /opt/splunkforwarder/bin
sudo ./splunk start --accept-license
sudo ./splunk enable boot-start

🔗 Step 6: Add Forwarding & Monitoring

sudo ./splunk add forward-server <SPLUNK_IP>:9997
sudo ./splunk add monitor /var/log/syslog

🔍 Step 7: Validate Logs in Splunk
Log in to Splunk Web UI

Go to Search & Reporting

Run this query:
index=* host=<kali/ubuntu hostname>

✅ You should see logs forwarded from Kali → Ubuntu → Splunk

```

🔐 Use Cases
🔍 Threat Detection in SOCs

📡 Log Collection for SIEM Pipelines

💾 Centralized Monitoring in Hybrid Infrastructure

🛠️ Blue Team Lab Setup for Cybersecurity Training

---

📚 References
rsyslog.com

Splunk UF Docs

man rsyslog.conf

Splunk Docs

---

## 🧑‍💻 Author

**Faizanullah Syed**  
💼 SOC Analyst   |   🛡️ Cybersecurity Enthusiast  
🌐 (https://unmaskcyber.com)





