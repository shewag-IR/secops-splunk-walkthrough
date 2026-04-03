# 🛡️ Getting Started with SIEM — Splunk Enterprise for Beginners

> **A complete beginner's guide to understanding SIEM, choosing Splunk, and setting it up on your local machine or VirtualBox — for free.**

---

## 📚 Table of Contents

1. [Module 1 — What is SIEM?](#module-1--what-is-siem)
2. [Module 2 — Why Do We Need SIEM?](#module-2--why-do-we-need-siem)
3. [Module 3 — Popular SIEM Platforms](#module-3--popular-siem-platforms)
4. [Module 4 — What is Splunk & Why Splunk?](#module-4--what-is-splunk--why-splunk)
5. [Module 5 — Prerequisites](#module-5--prerequisites)
6. [Module 6 — Installation Guide (Local Machine)](#module-6--installation-guide-local-machine)
7. [Module 7 — Installation Guide (VirtualBox)](#module-7--installation-guide-virtualbox)
8. [Module 8 — First Login & Basic Configuration](#module-8--first-login--basic-configuration)
9. [Module 9 — What to Practice Next](#module-9--what-to-practice-next)
10. [Useful Resources & Links](#useful-resources--links)

---

## Module 1 — What is SIEM?

**SIEM** stands for **Security Information and Event Management**.

Think of SIEM as the **central nervous system of a cybersecurity team**. It collects logs and events from every corner of an IT environment — servers, firewalls, endpoints, applications, cloud services — and brings them all into one place where security analysts can monitor, search, correlate, and alert on suspicious activity.

SIEM combines two older concepts:

| Concept | What it does |
|---|---|
| **SIM** (Security Information Management) | Long-term storage and analysis of log data |
| **SEM** (Security Event Management) | Real-time monitoring and correlation of events |

Together, SIEM gives security teams **visibility** — the ability to see what is happening across the entire environment at any given time.

### 🔍 A Simple Analogy

> Imagine your organization's IT infrastructure is a large airport. Each gate, terminal, and baggage claim generates events — people arriving, bags being scanned, alarms going off. A SIEM is the **airport control tower**: it collects all of that information, spots unusual patterns (someone entering a restricted area), and alerts the security team immediately.

---

## Module 2 — Why Do We Need SIEM?

### The Problem

Modern organizations generate **millions of log events every day**. A single Windows server can generate thousands of events per hour. Manually reviewing all of them is impossible.

Meanwhile, attackers are patient. They may spend **days or weeks** inside a network before being noticed. The average time to detect a breach, according to IBM's Cost of a Data Breach Report, is over **200 days**. That's too long.

### What SIEM Solves

| Challenge | How SIEM Helps |
|---|---|
| Too many logs to read manually | Aggregates and normalizes data from all sources |
| Threats spread across multiple systems | Correlates events across devices to find patterns |
| Slow detection | Real-time alerting and dashboards |
| No audit trail | Centralized log retention for compliance |
| Hard to investigate incidents | Search and timeline tools for forensic analysis |

### Real-World Use Cases

- 🔴 Detecting a **brute-force login attack** across multiple servers
- 🟠 Identifying **data exfiltration** (large amounts of data leaving the network at odd hours)
- 🟡 Spotting **lateral movement** (an attacker moving from one machine to another)
- 🟢 Compliance reporting for **PCI-DSS, HIPAA, ISO 27001, SOC 2**

> **As a SOC Analyst, SIEM is the tool you will spend the majority of your day working in. Learning SIEM is non-negotiable for a career in cybersecurity.**

---

## Module 3 — Popular SIEM Platforms

There are many SIEM tools in the industry. Here's an overview so you understand the landscape before committing to one:

| SIEM Platform | Developer | Best Known For | Cost |
|---|---|---|---|
| **Splunk Enterprise** | Splunk (Cisco) | Powerful search, massive ecosystem, industry standard | Paid (Free tier available) |
| **Microsoft Sentinel** | Microsoft | Native Azure integration, cloud-native SIEM | Pay-as-you-go |
| **IBM QRadar** | IBM | Enterprise-grade, strong compliance features | Paid |
| **Elastic SIEM (ELK Stack)** | Elastic | Open-source, highly customizable | Free (Open Source) |
| **LogRhythm** | LogRhythm | Threat detection automation, NextGen SIEM | Paid |
| **Wazuh** | Wazuh Inc. | Open-source, great for home labs | Free |
| **AlienVault OSSIM** | AT&T Cybersecurity | Open-source, includes threat intelligence | Free (Community) |
| **Chronicle** | Google | Cloud-native, uses Google's infrastructure | Paid |

### Which should a beginner learn?

While open-source tools like **Wazuh** and **ELK Stack** are great for home labs, **Splunk is the industry standard** that appears most frequently in job descriptions for SOC Analyst, Security Engineer, and Threat Hunter roles.

> ✅ **Recommendation for beginners**: Start with Splunk. Its free tier gives you enough to learn deeply, and the skills are directly transferable to paid jobs.

---

## Module 4 — What is Splunk & Why Splunk?

### What is Splunk?

**Splunk** is a data platform that specializes in **ingesting, indexing, searching, and visualizing machine-generated data** — primarily log files and events. Founded in 2003 and now part of Cisco, Splunk has become the dominant SIEM tool in enterprise environments worldwide.

Splunk works by:
1. **Collecting** data from agents (Universal Forwarders), APIs, syslog, files, etc.
2. **Indexing** the data so it can be searched incredibly fast
3. **Searching** using **SPL** (Splunk Processing Language) — Splunk's own query language
4. **Visualizing** data through dashboards, charts, and alerts

### Why Splunk for Beginners?

| Reason | Details |
|---|---|
| 🏆 **Industry Standard** | Splunk appears in the majority of SOC Analyst job postings globally |
| 🆓 **Free for Learning** | Splunk offers a free license for up to 500MB/day of data ingestion |
| 📖 **Excellent Documentation** | Splunk Docs are beginner-friendly and thorough |
| 🎓 **Free Training** | Splunk offers free official courses on Splunk Education |
| 🏅 **Certifications** | Splunk Core Certified User is a respected entry-level cert |
| 🌍 **Massive Community** | Large community on Splunk Answers, Reddit, and Discord |
| 🔬 **Great for Lab Work** | Easy to ingest sample datasets and practice detection |

### Splunk's Key Components

```
┌─────────────────────────────────────────────┐
│              Splunk Architecture             │
│                                             │
│  Data Sources → Universal Forwarder         │
│                      ↓                      │
│              Indexer (stores data)          │
│                      ↓                      │
│         Search Head (where you query)       │
│                      ↓                      │
│    Dashboards / Alerts / Reports            │
└─────────────────────────────────────────────┘
```

For a **single-instance local install** (which is what beginners use), all of these components run together on one machine.

---

## Module 5 — Prerequisites

Before you begin installation, make sure you have the following:

### 💻 System Requirements

#### For Local Machine (Direct Install)

| Component | Minimum | Recommended |
|---|---|---|
| **OS** | Windows 10/11, macOS 10.14+, Ubuntu 18.04+ | Ubuntu 22.04 LTS or Windows 11 |
| **CPU** | 4 cores | 8 cores |
| **RAM** | 4 GB | 8–16 GB |
| **Disk Space** | 20 GB free | 50+ GB free |
| **Architecture** | x86_64 only | x86_64 |

#### For VirtualBox (VM Install)

| Component | Minimum | Recommended |
|---|---|---|
| **Host RAM** | 8 GB | 16 GB |
| **Allocated VM RAM** | 4 GB | 6–8 GB |
| **VM Disk** | 30 GB (dynamically allocated) | 50 GB |
| **Host OS** | Windows, macOS, or Linux | Any |

### 🔑 Accounts You'll Need

- ✅ A **free Splunk account** — [Create one here](https://www.splunk.com/en_us/sign-up.html)
- ✅ (Optional) A **Splunk Education account** for free training — [education.splunk.com](https://education.splunk.com)

### 📦 Software to Download in Advance

| Software | Purpose | Link |
|---|---|---|
| Splunk Enterprise | The SIEM itself | [splunk.com/download](https://www.splunk.com/en_us/download/splunk-enterprise.html) |
| VirtualBox (if using VM) | Free virtualization software | [virtualbox.org](https://www.virtualbox.org/wiki/Downloads) |
| Ubuntu 22.04 ISO (if using VM) | Guest OS for the VM | [ubuntu.com/download](https://ubuntu.com/download/server) |
| 7-Zip or similar | Extracting files | [7-zip.org](https://www.7-zip.org/) |

> ⚠️ **Important Note**: Splunk Enterprise's **free license** allows ingestion of up to **500 MB of data per day**. This is more than enough for learning and lab purposes. You do **NOT** need to purchase anything.

---

## Module 6 — Installation Guide (Local Machine)

### 🐧 Option A: Linux (Ubuntu 22.04 LTS) — Recommended

Linux is the preferred environment for Splunk in both learning and production. It's more stable, and most real-world Splunk deployments are on Linux.

#### Step 1 — Update Your System

```bash
sudo apt update && sudo apt upgrade -y
```

#### Step 2 — Create a Splunk Account & Download

1. Go to 👉 [https://www.splunk.com/en_us/download/splunk-enterprise.html](https://www.splunk.com/en_us/download/splunk-enterprise.html)
2. Log in with your Splunk account (or create one — it's free)
3. Select **Linux** → Choose the **.deb** package (for Ubuntu/Debian) or **.tgz** (universal)
4. Copy the **wget** command provided on the download page

It will look something like this:
```bash
wget -O splunk-9.x.x-linux-2.6-amd64.deb "https://download.splunk.com/products/splunk/releases/..."
```

> 💡 **Tip**: Always download the latest stable version from the official site. The version number in the command above will differ from what's current.

#### Step 3 — Install Splunk

```bash
sudo dpkg -i splunk-9.x.x-linux-2.6-amd64.deb
```

This installs Splunk to `/opt/splunk/` by default.

#### Step 4 — Start Splunk & Accept License

```bash
sudo /opt/splunk/bin/splunk start --accept-license
```

You'll be prompted to:
- Set an **admin username** (default: `admin`)
- Set an **admin password** (choose something you'll remember)

#### Step 5 — Enable Splunk to Start on Boot

```bash
sudo /opt/splunk/bin/splunk enable boot-start
```

#### Step 6 — Open the Web Interface

Open your browser and go to:
```
http://localhost:8000
```

Log in with the admin credentials you created. 🎉 **You're in!**

---

### 🪟 Option B: Windows 10/11

#### Step 1 — Download the Installer

1. Go to 👉 [https://www.splunk.com/en_us/download/splunk-enterprise.html](https://www.splunk.com/en_us/download/splunk-enterprise.html)
2. Select **Windows** → Download the **.msi** installer

#### Step 2 — Run the Installer

1. Double-click the downloaded `.msi` file
2. Accept the License Agreement
3. Choose **"Splunk Enterprise Free Trial"** when asked about license type
4. Select installation directory (default: `C:\Program Files\Splunk`)
5. Set your **admin username and password**
6. Click **Install**

#### Step 3 — Access the Web Interface

After installation, Splunk should launch automatically. If not, open:
```
http://localhost:8000
```

> ⚠️ **Windows Firewall Note**: Windows may ask if you want to allow Splunk through the firewall. Click **Allow** to enable web interface access.

---

### 🍎 Option C: macOS

#### Step 1 — Download the DMG

1. Go to 👉 [https://www.splunk.com/en_us/download/splunk-enterprise.html](https://www.splunk.com/en_us/download/splunk-enterprise.html)
2. Select **Mac OS X** → Download the **.dmg** file

#### Step 2 — Install

1. Open the `.dmg` file
2. Drag Splunk to your Applications folder
3. Open Terminal and run:

```bash
sudo /Applications/Splunk/bin/splunk start --accept-license
```

#### Step 3 — Access the Web Interface

```
http://localhost:8000
```

---

## Module 7 — Installation Guide (VirtualBox)

Using VirtualBox is ideal if you want to **keep your main machine clean**, practice on Linux without dual-booting, or **create snapshots** (save states you can revert to — very useful for labs).

### Step 1 — Install VirtualBox

1. Download VirtualBox from 👉 [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)
2. Choose your **host OS** (the OS your physical machine runs)
3. Run the installer and follow the prompts
4. Also download and install the **VirtualBox Extension Pack** from the same page (adds USB and other features)

### Step 2 — Download Ubuntu 22.04 LTS ISO

Download from 👉 [https://ubuntu.com/download/server](https://ubuntu.com/download/server)

> 💡 **Tip**: Ubuntu Server is lighter than Desktop. However, if you prefer a graphical desktop inside the VM, download [Ubuntu Desktop](https://ubuntu.com/download/desktop) instead. For Splunk, Server is sufficient since you'll use the web browser on your host machine.

### Step 3 — Create a New Virtual Machine

1. Open VirtualBox → Click **"New"**
2. Fill in:
   - **Name**: `Splunk-Lab`
   - **Type**: Linux
   - **Version**: Ubuntu (64-bit)
3. **Memory (RAM)**: Allocate at least **4096 MB** (4 GB). More is better.
4. **Hard Disk**: Create a new virtual hard disk
   - Type: **VDI**
   - Storage: **Dynamically allocated**
   - Size: **50 GB** minimum

### Step 4 — Configure the VM

Before starting the VM, adjust these settings:

**System → Processor**: Assign at least **2 CPUs** (4 recommended)

**Network**:
- Adapter 1: **NAT** (for internet access)
- Adapter 2 (optional): **Host-Only Adapter** (to access Splunk's web UI from your host browser)

> 💡 **Why Host-Only Adapter?** It lets your host machine's browser reach `http://<VM_IP>:8000` directly. Without it, you'd need to set up port forwarding.

**Storage**: Click the empty CD drive icon → Choose a disk file → Select your downloaded **Ubuntu ISO**

### Step 5 — Install Ubuntu in the VM

1. Start the VM
2. Follow the Ubuntu installation wizard
3. Set a username and password you'll remember
4. After installation, the VM will reboot — remove the ISO from the virtual drive

### Step 6 — Take a Snapshot (Highly Recommended!)

Before installing Splunk, save a clean snapshot:

```
VirtualBox → Machine → Take Snapshot → Name it "Clean Ubuntu Install"
```

This lets you **reset to a clean state** anytime something goes wrong.

### Step 7 — Install Splunk in the VM

SSH into your VM or use the VM's terminal, then follow the exact same steps as **[Option A: Linux](#-option-a-linux-ubuntu-2204-lts--recommended)** above.

### Step 8 — Access Splunk from Your Host Browser

If you configured a Host-Only Adapter:
1. In the VM terminal, find the VM's IP address:
   ```bash
   ip addr show
   ```
2. On your **host machine's browser**, go to:
   ```
   http://<VM_IP_ADDRESS>:8000
   ```

If using only NAT, set up **Port Forwarding** in VirtualBox:
```
VM Settings → Network → Adapter 1 (NAT) → Advanced → Port Forwarding
Add rule: Host Port 8000 → Guest Port 8000
```
Then access via `http://localhost:8000` on your host.

---

## Module 8 — First Login & Basic Configuration

### Logging In

1. Open browser → go to `http://localhost:8000` (or VM IP)
2. Username: `admin`
3. Password: whatever you set during installation

### Activating the Free License

On first login, Splunk may ask about licensing:
- Select **"Use the free license"** / **"Start a 60-day trial"** then downgrade to free
- The free license gives you **500 MB/day** — plenty for learning

> ⚠️ **Important**: The trial license gives you all Enterprise features for 60 days. After 60 days, it downgrades to the free tier. No payment is ever required for the free tier.

### Ingesting Your First Data

Splunk is useless without data. Here's how to get some in quickly:

#### Option 1 — Upload a Sample Log File

1. In Splunk Web → Click **"Add Data"** (on the home screen)
2. Select **"Upload"**
3. Choose a log file from your machine (e.g., a Windows Event Log `.evtx` or a `.log` file)

#### Option 2 — Use Splunk's Tutorial Dataset

Splunk provides a sample dataset called **"tutorialdata.zip"**:
- Download it from 👉 [Splunk Tutorial Data](https://docs.splunk.com/Documentation/Splunk/latest/SearchTutorial/GetthetutorialdataintoSplunk)
- Upload it via **Add Data → Upload**

#### Option 3 — Monitor System Logs (Linux)

```bash
# In Splunk Web → Settings → Data Inputs → Files & Directories
# Add: /var/log/syslog or /var/log/auth.log
```

### Your First Search

Once data is in, go to the **Search & Reporting** app and try:

```spl
index=* 
| head 20
```

This shows the 20 most recent events across all indexes. Welcome to SPL! 🎉

---

## Module 9 — What to Practice Next

Now that Splunk is running, here's a structured learning path:

### 🥇 Beginner (Week 1–2)
- [ ] Learn basic **SPL (Splunk Processing Language)** — `search`, `stats`, `table`, `sort`, `rex`
- [ ] Understand **indexes, sourcetypes, and hosts**
- [ ] Ingest sample data and explore the Search interface
- [ ] Create a simple **dashboard**

### 🥈 Intermediate (Week 3–4)
- [ ] Set up **Splunk Universal Forwarder** to ship logs from another machine
- [ ] Build **correlation searches** and alerts
- [ ] Ingest **Windows Event Logs** and **Syslog**
- [ ] Install and explore the **Splunk Security Essentials** app

### 🥉 Advanced Practice (Month 2+)
- [ ] Install **Boss of the SOC (BOTS)** dataset for realistic attack scenarios
- [ ] Practice on **TryHackMe's Splunk rooms** ([tryhackme.com](https://tryhackme.com))
- [ ] Work through **Splunk's Attack Range** for simulated attacks
- [ ] Study for the **Splunk Core Certified User** exam

### 📦 Recommended Splunk Apps to Install

| App | Purpose | Link |
|---|---|---|
| Splunk Security Essentials | Pre-built detections | [Splunkbase](https://splunkbase.splunk.com/app/3435) |
| Splunk Add-on for Windows | Windows event normalization | [Splunkbase](https://splunkbase.splunk.com/app/742) |
| Splunk Add-on for Unix/Linux | Linux log normalization | [Splunkbase](https://splunkbase.splunk.com/app/833) |
| CIM (Common Information Model) | Data normalization framework | [Splunkbase](https://splunkbase.splunk.com/app/1621) |
| MITRE ATT&CK App | Map detections to MITRE | [Splunkbase](https://splunkbase.splunk.com/app/4617) |

---

## Useful Resources & Links

### 📖 Official Splunk Resources

| Resource | Link |
|---|---|
| Splunk Documentation | [docs.splunk.com](https://docs.splunk.com) |
| Splunk Free Training | [education.splunk.com](https://education.splunk.com) |
| Splunk Search Tutorial | [Splunk Search Tutorial](https://docs.splunk.com/Documentation/Splunk/latest/SearchTutorial/WelcometotheSearchTutorial) |
| Splunk Community / Answers | [community.splunk.com](https://community.splunk.com) |
| Splunkbase (Apps) | [splunkbase.splunk.com](https://splunkbase.splunk.com) |
| Splunk Certifications | [Splunk Cert Path](https://www.splunk.com/en_us/training/certification-track/splunk-core-certified-user.html) |

### 🎯 Practice Platforms

| Platform | What You Get | Link |
|---|---|---|
| TryHackMe | Splunk rooms, SOC Level 1 path | [tryhackme.com](https://tryhackme.com) |
| LetsDefend | Blue team SOC simulation | [letsdefend.io](https://letsdefend.io) |
| CyberDefenders | DFIR and SIEM challenges | [cyberdefenders.org](https://cyberdefenders.org) |
| Boss of the SOC (BOTS) | Splunk CTF-style dataset | [BOTS Dataset](https://github.com/splunk/botsv3) |
| Splunk Attack Range | Simulate attacks in a lab | [Attack Range](https://github.com/splunk/attack_range) |

### 📺 Video Learning

| Resource | Link |
|---|---|
| Splunk YouTube Channel | [youtube.com/@SplunkHowTo](https://www.youtube.com/@SplunkHowTo) |
| John Hubbard (SANS Blue Team) | Search on YouTube |
| MyDFIR (SOC Analyst content) | [youtube.com/@MyDFIR](https://www.youtube.com/@MyDFIR) |

### 📚 Books & Study Guides

- *Splunk Operational Intelligence Cookbook* — available on Amazon
- *SOC Analyst Study Guide* — various authors on Amazon
- [Paul Jerimy's Security Certification Roadmap](https://pauljerimy.com/security-certification-roadmap/) — to plan your cert journey

---

## ⚠️ Common Issues & Troubleshooting

| Problem | Likely Cause | Fix |
|---|---|---|
| Can't access `localhost:8000` | Splunk not running | Run `sudo /opt/splunk/bin/splunk status` and start if stopped |
| Splunk starts but page won't load | Port conflict or firewall | Check firewall rules, try `http://127.0.0.1:8000` |
| "License expired" message | Trial ended | Go to Settings → Licensing → Switch to Free License |
| VM is slow | Not enough RAM allocated | Allocate more RAM in VirtualBox settings (shut down VM first) |
| Data not appearing in search | Wrong index or time range | Set time range to "All Time" and check your index name |
| Forgot admin password | — | Run: `sudo /opt/splunk/bin/splunk edit user admin -password NEW_PASSWORD -auth admin:OLD_PASSWORD` |

---

## 🤝 Contributing

Found an error or want to add content? PRs are welcome! Please open an issue first to discuss what you'd like to change.

---

## 📄 License

This guide is open for educational use. Feel free to share, adapt, and build on it — just give credit.

---

<div align="center">

**Happy Learning! 🚀**

*The best SOC analyst you'll ever be starts with a home lab and curiosity.*

⭐ Star this repo if it helped you — it helps others find it too!

</div>
