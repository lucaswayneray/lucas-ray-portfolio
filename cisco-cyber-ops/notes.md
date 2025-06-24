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
