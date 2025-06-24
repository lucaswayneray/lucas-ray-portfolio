# Cisco SOC Course Study Guide

> This document is a structured, expandable study guide based on the Cisco SOC specialization track. Notes are derived from shorthand entries and cleaned for clarity. It will grow to include material from Courses 2 and 3.

---

## Module 1: Roles in a Security Operations Center (SOC)

### SOC Analysts

* **Tier 1 Analyst:** Triage alerts, basic investigation, escalate as needed.
* **Tier 2 Analyst:** Deep dive analysis, threat hunting, containment support.
* **Tier 3 Analyst:** Incident Response (IR), forensics, malware analysis.

### Other Roles

* **Security Engineer:** Develops, integrates, and maintains SOC tools. Defines requirements.
* **SOC Manager:** Leads team operations, oversees policy adherence.
* **CTI Analyst (Cyber Threat Intelligence):** Tracks threat actors, provides indicators of compromise (IOCs).
* **Digital Forensic Analyst:** Investigates digital evidence post-incident.

---

## Module 2: Threat Intelligence

### Sources

* Open Source Intelligence (OSINT)
* Commercial threat intel feeds
* Government sources (e.g., US-CERT)

### Formats

* IOCs: hashes, IPs, domains, URLs
* TTPs: Tactics, Techniques, Procedures

### Tools

* MISP, ThreatConnect, Anomali

---

## Module 3: Common Security Tools

### Key Tools

* **SIEM (Security Information and Event Management):** Aggregates and analyzes log data (e.g., Splunk, QRadar)
* **Endpoint Detection and Response (EDR):** Monitors and collects activity from endpoints (e.g., CrowdStrike)
* **Packet Capture (PCAP):** Records network traffic (e.g., Wireshark)
* **Firewall/NGFW:** Controls network traffic
* **IDS/IPS:** Detects/prevents intrusions

---

## Module 4: Log Management & Analysis

### Log Types

* Authentication logs
* DNS logs
* Network traffic logs
* Application logs

### Analysis Techniques

* Log correlation
* Timeline analysis
* Anomaly detection

---

## Module 5: Incident Detection & Response

### Detection

* Based on log anomalies, alerts, threat intel
* Use of SIEM rules, correlation, and thresholds

### Response Phases

1. **Preparation**
2. **Identification**
3. **Containment**
4. **Eradication**
5. **Recovery**
6. **Lessons Learned**

### Incident Types

* Malware infection
* Unauthorized access
* DDoS attacks
* Insider threats

---

## Module 6: Network Fundamentals for SOC

### Protocols

* TCP, UDP
* HTTP, HTTPS
* DNS, DHCP
* ICMP

### Concepts

* Ports (well-known: 0–1023)
* IP Addressing (IPv4/IPv6)
* Subnetting, NAT, VLANs

### Network Devices

* Router, Switch, Firewall
* Load Balancer, Proxy

---

## Module 7: SIEM & Correlation Rules

### SIEM Capabilities

* Central log collection
* Alert generation
* Visualization

### Correlation Rules

* Rule logic to match event patterns
* Can use thresholds, time windows
* Examples:

  * 5 failed logins in 10 minutes from same IP
  * Outbound traffic to known malicious IPs

### SIEM Deployment Considerations

* Use cases defined by business needs
* Custom parsers may be needed
* Prioritize high-value data sources

---

## Module 8: Workflow Management and SOC Automation

### Workflow Management System (WMS)

* WMS is software used to coordinate and automate security incident response from detection to mitigation to ticket closure.
* Also known as SOAR (Security Orchestration, Automation, and Response) in many contexts.
* Vendors may use unique names (e.g., Swimlane calls it a Security Operations Orchestration and Automation platform).
* A WMS typically comes into play after a SIEM (e.g., Splunk, LogRhythm, AlienVault) detects a security event.

### Workflow Types

1. **Sequential Workflow** – Flowchart-style; proceeds linearly through steps without returning.
2. **State Machine Workflow** – More complex; can return to previous states if needed.
3. **Rules-Driven Workflow** – Based on predefined rules that dictate progression (a variation of sequential workflows).

### Benefits of WMS

* Coordinates efforts between multiple team members and systems.
* Automates repeatable tasks, freeing analysts for more complex duties.
* Increases consistency and accuracy.

### Example Tasks WMS Can Automate:

| **Task**                          | **Description**                                          |
| --------------------------------- | -------------------------------------------------------- |
| Audit Log Collection & Enrichment | Retrieves and enriches logs across devices               |
| User/Device Lookup                | Pulls user info from directories; resolves hostnames/IPs |
| Alerts & Notifications            | Generates alerts from defined conditions                 |
| Threat Intelligence Integration   | Uses external feeds for contextual threat awareness      |
| Ticket Management                 | Creates, validates, and resolves tickets                 |
| Escalations                       | Initiates contact or legal procedures when needed        |

### Integration Approaches

* **RESTful API** – Uses HTTP requests to exchange data with tools (e.g., ticketing systems)
* **Command-Line API** – Executes commands directly from the shell
* **TAXII** – Standardized transport protocol for threat intel sharing

### SIEM & WMS Integration

* SIEM captures logs and raises alerts.
* WMS responds by generating tasks, executing remediation, and creating cases.
* Ensures consistent and automated responses.

### Incident Response Workflow

* Ensures all incident severities have defined response processes.
* Severity may change during handling; workflows adapt accordingly.
* WMS can automate reporting reminders and SLA tracking.

### SOC Roles in Workflow

| **Role**                  | **Responsibilities**                            |
| ------------------------- | ----------------------------------------------- |
| Tier 1 Analyst            | Alert triage, data collection                   |
| Tier 2 Analyst            | Deep analysis, endpoint forensics               |
| Incident Response Handler | Orchestrates containment/remediation            |
| Forensics Specialist      | Collects and preserves evidence                 |
| Malware Reverse Engineer  | Analyzes and develops IOCs/signatures           |
| SOC Management            | Oversees resources, strategy, and communication |
| Executive Leadership      | Sets strategic direction                        |

### Automation & Orchestration Benefits

* Reduces human error and labor costs
* Improves speed and consistency of detection and response
* Allows SOCs to evolve playbooks and handle high volumes of alerts
* Automates Tier 1+2 workflows, allowing analysts to focus on high-level tasks

### SOC Workflow Automation Example

* Tier 1 receives alert → opens ticket → collects user and IP info → queries threat intel → assigns severity → escalates.
* Tier 2 confirms exploit, queries endpoint, collects logs, executes containment.
* Tier 3 performs forensics, extracts indicators, updates threat intel.
* Management reviews metrics (time to detect, contain, resolve).

### Notable WMS/SOAR Vendors

* Cisco SecureX
* Cisco CloudCenter Action Orchestrator
* IBM Resilient Systems
* Proofpoint Threat Response
* Swimlane
* CyberSponse

---

*End of Course 1 Study Guide — Ready for upload to GitHub. Next up: Course 2 and supplemental notes.*
# Cisco Cybersecurity Certificate - Course 2 Notes

## Overview

**Course Title:** Cisco Networking Academy – CyberOps Associate, Course 2
**Focus:** Linux OS functionality, file systems, boot and process control, system recovery, GUI vs CLI operation, user management, and secure system administration — foundational skills for SOC analysts.

---

## Module 2: Linux OS Fundamentals for Cybersecurity

This module explores Linux's structure and role in cybersecurity. Topics include permissions, process control, recovery procedures, GUI and CLI administration, boot structure, and core shell concepts.

---

### 🔹 Linux Basics

* **Linux**: UNIX-like, open-source operating system.
* **Key advantages**: stability, flexibility, transparency.
* **Kernel vs. User space**:

  * Kernel handles hardware, memory, devices.
  * User space runs applications and interfaces.

---

### 🔹 Linux Filesystem Structure

* **Single root hierarchy** starting at `/`.
* Common directories:

  * `/bin`, `/sbin`: Essential commands
  * `/etc`: Config files
  * `/home`: User directories
  * `/var`: Logs, dynamic files
  * `/dev`: Device files
  * `/mnt`, `/media`: Mount points

#### Filesystem Commands

```bash
pwd      # Show current path
cd ..    # Move up
ls -l    # List files in long format
```

---

### 🔹 File Permissions

* Each file has **owner**, **group**, **others**.
* Access: `r` (read), `w` (write), `x` (execute)

#### Symbolic Permissions Example

```
-rwxr-xr--
```

* User: rwx
* Group: r-x
* Others: r--

#### Octal Representation

| Binary | Octal | Meaning |
| ------ | ----- | ------- |
| 111    | 7     | rwx     |
| 110    | 6     | rw-     |
| 100    | 4     | r--     |

#### Chmod Examples

```bash
chmod 755 file
chmod u+x script.sh
chmod go-w config.cfg
```

---

### 🔹 Sudo and Root

* `sudo`: temporary privilege elevation.
* `root`: superuser account with full access.

```bash
sudo nano /etc/fstab
```

---

### 🔹 Disks and Mounting

* **Device files**: `/dev/sda`, `/dev/sda1`
* **Partitioning**: MBR (legacy), GPT (modern)
* **File Systems**: ext4, xfs, FAT32, NTFS

#### Useful Tools

```bash
lsblk       # List block devices
df -h       # Disk space usage
blkid       # List partitions and UUIDs
mount       # Mount a device
umount      # Unmount a device
```

#### /etc/fstab Example

```
UUID=1234-5678 / ext4 defaults 0 1
```

---

### 🔹 Boot Process

* BIOS/UEFI → GRUB → Kernel → Init system (systemd)

#### System Initialization

* `init` (SysVInit) and `systemd` (modern)
* Systemd uses unit files and targets (e.g., `multi-user.target`, `graphical.target`)

#### Systemd

* Modern init system
* Uses `.target` files instead of runlevels
* `systemctl` controls services

```bash
systemctl list-units
systemctl reboot
```

#### SysV Init (legacy)

| Runlevel | Purpose          |
| -------- | ---------------- |
| 0        | Halt             |
| 1        | Single-user mode |
| 3        | Multi-user (CLI) |
| 5        | Multi-user (GUI) |
| 6        | Reboot           |

---

### 🔹 Emergency Modes

* **Single-user mode**: root shell, minimal services.
* **Live CD/USB**: For recovery without using internal OS.

---

### 🔹 Shutdown and Reboot

```bash
shutdown -h now
shutdown -r +5 "Rebooting"
reboot
poweroff
```

---

### 🔹 Shell vs GUI

| Feature  | CLI (Shell)       | GUI               |
| -------- | ----------------- | ----------------- |
| Speed    | Fast & scriptable | Visual navigation |
| Learning | Steep curve       | Intuitive         |
| Access   | Remote via SSH    | Local/logged in   |

Common shells: `bash`, `sh`, `zsh`, `fish`

---

### 🔹 Shell Basics

* **Environment variables**: `$USER`, `$HOME`, `$PATH`
* **Redirection**: `>`, `>>`, `2>`, `<`
* **Pipes**: `|` to chain commands

```bash
ls -l | grep config
cat file.txt > output.txt
```

---

### 🔹 Processes

* **Fork()**: duplicates a process
* **Exec()**: replaces current process image

#### Monitoring Tools

```bash
ps aux
ps -ef
top
kill -9 <PID>
```

---

### 🔹 Command Chains

* Use `&&` to chain conditional execution

```bash
apt update && apt upgrade
```

* Use `|` to pass output

```bash
ps aux | grep ssh
```

---

### 🔹 Viewing Network Properties in Linux

Modern Linux implementations often include **automated network management services** that:

* Configure and manage network interface states automatically.
* Are often tied to GUI-based tools.

> ⚠️ If you make changes via the command line while network management services are running, those changes may be **overwritten** either by the background processes or upon reboot.

#### Managing Network Properties via CLI

If you prefer CLI:

* You must **disable or remove** the built-in network management services from your distribution.
* You can then manually configure network interfaces and settings.

---

### 🔹 `ifconfig` vs `ip`

* `ifconfig` has been around a long time and is still widely used.
* However, it is deprecated in many distros and replaced by the more powerful `ip` command, part of the `iproute2` utilities.
* `ip` is **not a direct replacement**; syntax and capabilities differ.

🔗 Resources:

* [Linux.com - Replacing ifconfig with ip](https://www.linux.com/training-tutorials/replacing-ifconfig-ip/)
* [Red Hat - ifconfig vs ip](https://www.redhat.com/sysadmin/ifconfig-vs-ip)

---

### 🔹 `ifconfig -a` Output Example

This command displays **all interfaces**, even if they’re down.

```bash
ifconfig -a
```

Example output:

```
ens160 Link encap:Ethernet  HWaddr 00:0c:29:dc:fa:a7
inet addr:192.168.7.77  Bcast:192.168.7.255  Mask:255.255.255.0
inet6 addr: fe80::20c:29ff:fedc:faa7/64  Scope:Link
UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
RX packets:5354  TX packets:294
RX bytes:636648  TX bytes:44035

lo Link encap:Local Loopback
inet addr:127.0.0.1  Mask:255.0.0.0
inet6 addr: ::1/128  Scope:Host
UP LOOPBACK RUNNING  MTU:65536  Metric:1
RX packets:1803  TX packets:1803
RX bytes:184103  TX bytes:184103
```

* **ens160**: Main Ethernet interface
* **lo**: Loopback interface
* Look for `UP` to confirm it's active
* Displays both IPv4 and IPv6 addresses
* Shows packet transmission stats

---

### 🔹 `ifconfig [interface]` Example

To inspect a single interface:

```bash
ifconfig ens160
```

Example output:

```
ens160 Link encap:Ethernet  HWaddr 00:0c:29:b7:ed:0e
inet addr:192.168.7.104  Bcast:192.168.7.255  Mask:255.255.255.0
inet6 addr: fe80::3e06:eb0f:2c50:ec94/64  Scope:Link
UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
RX packets:898316  TX packets:10199
RX bytes:96.7 MB  TX bytes:614.7 KB
```

---

## ✅ Module 2 Complete

All shorthand and images have been compiled into a structured, clean doc. Ready for Module 3 or flashcard prep!

## ✅ Screenshots and Visual References

!\[Filesystem Basics]\(sandbox:/mnt/data/Screenshot 2025-05-31 2.38.16 PM.png)
!\[Permissions Reference]\(sandbox:/mnt/data/Screenshot 2025-05-31 7.49.41 PM.png)
!\[Systemd View]\(sandbox:/mnt/data/Screenshot 2025-05-31 8.03.00 PM.png)
!\[Process Table]\(sandbox:/mnt/data/Screenshot 2025-05-31 8.28.28 PM.png)
!\[Chaining and Piping]\(sandbox:/mnt/data/Screenshot 2025-05-31 8.34.21 PM.png)
