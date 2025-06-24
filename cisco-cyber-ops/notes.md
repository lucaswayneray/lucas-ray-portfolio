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

## ✅ Screenshots and Visual References

!\[Filesystem Basics]\(sandbox:/mnt/data/Screenshot 2025-05-31 2.38.16 PM.png) !\[Permissions Reference]\(sandbox:/mnt/data/Screenshot 2025-05-31 7.49.41 PM.png) !\[Systemd View]\(sandbox:/mnt/data/Screenshot 2025-05-31 8.03.00 PM.png) !\[Process Table]\(sandbox:/mnt/data/Screenshot 2025-05-31 8.28.28 PM.png) !\[Chaining and Piping]\(sandbox:/mnt/data/Screenshot 2025-05-31 8.34.21 PM.png)

---

## ✅ Module 2 Complete

All shorthand and images have been compiled into a structured, clean doc. Ready for Module 3 or flashcard prep!

Viewing Basic Network Properties- Modern Linux implmnttions use automated ntwrk mgmt prcsses- to config and manage ntwrk interface states- these mgmt tools ship w/ GUI-based apps from whch you can view and edit ntwrk properties. A good idea to use the GUI based tools to edit ntwrk properties. Any chngs you make from the cmmnd line will be overwritten by background prcsses- that are responsible for maintaining ntwrk or when the host is restarted. If prefer to mnge ntwrk proprties from the cmmnd line, can disable or remove the ntwrk- mgmt tools that are ntvely shipped w/ your Linux distrbtion, and mnge your ntwrking prprties- manully from the cmmnd line. 

Note:\*\* ip - a\*\* rplcmnt for ifconfig cmmnd:\*\* ifconfig\*\* has been there a long time and still used to config, dsply, and Ctrl ntwrk intrfce- by many, but a new alternative now exists on Linux distrbtions which is more pwerful. Alternative is IP command from \*\*iproute2util \*\* pkge. Know that\*\* ip\*\* is not a drop-in rplcmnt for ipconfig. There are differences in the strctre of the cmmnds. Even w/ these diffs both cmmnds are used for similar prpses:


[https://www.linux.com/training-tutorials/replacing-ifconfig-ip/](https://www.linux.com/training-tutorials/replacing-ifconfig-ip/) and [https://www.redhat.com/sysadmin/ifconfig-vs-ip](https://www.redhat.com/sysadmin/ifconfig-vs-ip)  

One of most imprtnt cmmnds reltve to checking your ntwrk proprts is the ifconfig cmmnd. Gives you a lot of info about the state of your ntwrk intrfce- and their configs. The ifconfig cmmnd accpts many options, but w/ the syntax shown in fllwing ex, a lot of info is rtrved about the interfaces in the installation:

ifconfig -a

ens160 Link encap\:Ethernet HWaddr 00:0c:29\:dc\:fa\:a7&#x20;

inet addr:192.168.7.77 Bcast:192.168.7.255 Mask:255.255.255.0

&#x20;inet6 addr: fe80::20c:29ff\:fedc\:faa7/64 Scope\:Link&#x20;

UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1&#x20;

RX packets:5354 errors:0 dropped:1294 overruns:0 frame:0&#x20;

TX packets:294 errors:0 dropped:0 overruns:0 carrier:0&#x20;

collisions:0 txqueuelen:1000&#x20;

RX bytes:636648 (636.6 KB) TX bytes:44035 (44.0 KB)&#x20;

lo Link encap\:Local Loopback&#x20;

inet addr:127.0.0.1 Mask:255.0.0.0

&#x20;inet6 addr: ::1/128 Scope\:Host&#x20;

UP LOOPBACK RUNNING MTU:65536 Metric:1

&#x20;RX packets:1803 errors:0 dropped:0 overruns:0 frame:0&#x20;

TX packets:1803 errors:0 dropped:0 overruns:0 carrier:0&#x20;

collisions:0 txqueuelen:1&#x20;

RX bytes:184103 (184.1 KB) TX bytes:184103 (184.1 KB)

The -a option instructs the Systm to output info on all the interfaces even if they are down. Each entry begins w/ the name of the interface. In the ex, the first interface is called ens160, and second intrfce- is called lo, aka loopback interface. First line in details portion of the entry shows the hardware address (for ex, the MAC address) of the interface. the next lines show the IP address info that is assctd w/ the intrfce which includes the fllwing:

* IPv4 IP address
* Broadcast address
* Subnet mask
* IPv6 IP address

After the IP address info, displays info regarding the state of the interface. If you see the word UP at beginning of this section, the interface is able to send and rcv IP traffic. The remainder of the feedback gives you stats about packets that are rcvd and transmitted.

The if config cmmnd tells you a lot about the state of your ntwrk intrfce and their configs. Can get info on a spcfc intrfce- by specifying the intrfce name in the cmmnd. 

ifconfig ens160

ens160 Link encap\:Ethernet HWaddr 00:0c:29\:b7\:ed:0e

&#x20;inet addr:192.168.7.104 Bcast:192.168.7.255 Mask:255.255.255.0

&#x20;inet6 addr: fe80::3e06\:eb0f:2c50\:ec94/64 Scope\:Link

&#x20;UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1&#x20;

RX packets:898316 errors:0 dropped:2 overruns:0 frame:0&#x20;

TX packets:10199 errors:0 dropped:0 overruns:0 carrier:0

&#x20;collisions:0 txqueuelen:1000

&#x20;RX bytes:96750642 (96.7 MB) TX bytes:614795 (614.7 KB)

\\
