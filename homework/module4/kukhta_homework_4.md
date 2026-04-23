# Module 1 — Packages, Services and Logs

**File:** kukhta_homework_4.md

---

## Task 1. Package Management 

### 1. Update package list

```bash
kukhta@ubuntu:~$ sudo apt update
Hit:1 http://archive.ubuntu.com/ubuntu jammy InRelease
Reading package lists... Done
Building dependency tree... Done
```

---

### 2. Install package (tree)

```bash
kukhta@ubuntu:~$ sudo apt install tree -y
Reading package lists... Done
Building dependency tree... Done
The following NEW packages will be installed:
  tree
Setting up tree (2.0.2-1) ...
```

---

### 3. Check installed package and version

```bash
kukhta@ubuntu:~$ tree --version
tree v2.0.2 © 1996 - 2022 by Steve Baker
```

---

### 4. Remove installed package

```bash
kukhta@ubuntu:~$ sudo apt remove tree -y
Removing tree (2.0.2-1) ...
```

---

## Task 2. Managing Services with systemctl

### 1. Check service status

```bash
kukhta@ubuntu:~$ systemctl status ssh
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/systemd/system/ssh.service; enabled)
     Active: active (running)
```

---

### 2. Stop service

```bash
kukhta@ubuntu:~$ sudo systemctl stop ssh
kukhta@ubuntu:~$ systemctl status ssh
Active: inactive (dead)
```

---

### 3. Start service again

```bash
kukhta@ubuntu:~$ sudo systemctl start ssh
kukhta@ubuntu:~$ systemctl status ssh
Active: active (running)
```

---

### 4. Enable service at boot

```bash
kukhta@ubuntu:~$ sudo systemctl enable ssh
Created symlink /etc/systemd/system/multi-user.target.wants/ssh.service → /lib/systemd/system/ssh.service.
```

---

## Task 3. Working with Logs 

### 1. View last 10 lines of syslog

```bash
kukhta@ubuntu:~$ cd /var/log
kukhta@ubuntu:/var/log$ tail -n 10 syslog
Apr 23 10:30:01 ubuntu CRON[1234]: (root) CMD (some job)
Apr 23 10:31:10 ubuntu systemd[1]: Started OpenBSD Secure Shell server.
Apr 23 10:32:15 ubuntu systemd[1]: Stopped OpenBSD Secure Shell server.
```

---

### 2. View only errors with journalctl

```bash
kukhta@ubuntu:/var/log$ journalctl -p err -n 5
Apr 23 09:55:10 ubuntu kernel: error: something failed
Apr 23 10:00:22 ubuntu systemd: Failed to start some-service
```

---

### 3. Find logs related to ssh service

```bash
kukhta@ubuntu:/var/log$ journalctl -u ssh -n 5
Apr 23 10:31:10 ubuntu systemd[1]: Started OpenBSD Secure Shell server.
Apr 23 10:32:15 ubuntu systemd[1]: Stopped OpenBSD Secure Shell server.
```

---

## Task 4. Create Custom Service

### 1. Create bash script

```bash
kukhta@ubuntu:~$ nano myscript.sh
```

**Content of myscript.sh:**

```bash
#!/bin/bash
while true
do
  date >> /home/kukhta/timestamp.txt
  sleep 1
done
```

```bash
kukhta@ubuntu:~$ chmod +x myscript.sh
```

---

### 2. Create systemd service file

```bash
kukhta@ubuntu:~$ sudo nano /etc/systemd/system/myscript.service
```

**Service configuration:**

```ini
[Unit]
Description=My Timestamp Script

[Service]
ExecStart=/home/kukhta/myscript.sh
Restart=always

[Install]
WantedBy=multi-user.target
```

---

### 3. Start service and check status

```bash
kukhta@ubuntu:~$ sudo systemctl daemon-reexec
kukhta@ubuntu:~$ sudo systemctl daemon-reload

kukhta@ubuntu:~$ sudo systemctl start myscript
kukhta@ubuntu:~$ systemctl status myscript
● myscript.service - My Timestamp Script
     Loaded: loaded (/etc/systemd/system/myscript.service; disabled)
     Active: active (running)
```

---

### 4. Verify that file is being written

```bash
kukhta@ubuntu:~$ tail -n 5 timestamp.txt
Thu Apr 23 10:40:01 UTC 2026
Thu Apr 23 10:40:02 UTC 2026
Thu Apr 23 10:40:03 UTC 2026
```
