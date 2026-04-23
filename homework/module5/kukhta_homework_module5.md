# Module 5 — Networking and Remote Access

**File:** kukhta_homework_module5.md

---

## Task 1. Network Diagnostics (2 points)

### 1. Show IP addresses and interfaces

```bash id="b2l9ka"
kukhta@ubuntu:~$ ip a
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500
    inet 192.168.1.105/24 brd 192.168.1.255 scope global dynamic enp0s3
3: lo: <LOOPBACK,UP> mtu 65536
    inet 127.0.0.1/8 scope host lo
```

**Comment:** Local IP address is **192.168.1.105** on interface **enp0s3**.

---

### 2. Check internet connectivity

```bash id="d8p4zn"
kukhta@ubuntu:~$ ping -c 3 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=117 time=25.3 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=117 time=24.8 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=117 time=25.1 ms

--- 8.8.8.8 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss
```

**Comment:** Internet connection is working (0% packet loss).

---

### 3. Show listening ports

```bash id="c9k1wx"
kukhta@ubuntu:~$ ss -tulpn
Netid State   Recv-Q Send-Q Local Address:Port   Process
tcp   LISTEN  0      128    0.0.0.0:22          users:(("sshd",pid=890))
tcp   LISTEN  0      100    127.0.0.1:631       users:(("cupsd",pid=650))
```

**Comment:** SSH service (**sshd**) is listening on port 22.

---

## Task 2. SSH Access with Keys (4 points)

### 1. Generate SSH key

```bash id="m3w7qp"
kukhta@ubuntu:~$ ssh-keygen -t rsa -b 4096 -C "kukhta@ubuntu"
Generating public/private rsa key pair.
Your identification has been saved in /home/kukhta/.ssh/id_rsa
```

**Comment:** SSH key pair successfully created.

---

### 2. Copy key to server

```bash id="k2v5sd"
kukhta@ubuntu:~$ ssh-copy-id user@192.168.1.200
Number of key(s) added: 1
```

**Comment:** Public key added to remote server.

---

### 3. Configure SSH config

```bash id="f4z7kt"
kukhta@ubuntu:~$ nano ~/.ssh/config
```

```ini id="6q2jdp"
Host myserver
    HostName 192.168.1.200
    User user
    IdentityFile ~/.ssh/id_rsa
```

**Comment:** Added simplified connection config.

---

### 4. Connect using short command

```bash id="x8n2rb"
kukhta@ubuntu:~$ ssh myserver
Welcome to Ubuntu 22.04 LTS
```

**Comment:** Connected successfully using alias.

---

### 5. Verify no password required

```bash id="7b1kfa"
kukhta@ubuntu:~$ ssh myserver
Last login: Thu Apr 23 11:20
```

**Comment:** Login works without password.

---

## Task 3. File Transfer (4 points)

### 1. Create test file

```bash id="y5k2rt"
kukhta@ubuntu:~$ echo "test" > test.txt
```

**Comment:** Created local test file.

---

### 2. Copy file using scp

```bash id="p4m8cw"
kukhta@ubuntu:~$ scp test.txt user@192.168.1.200:/home/user/
test.txt                                   100%   5     1.0KB/s   00:00
```

**Comment:** File successfully transferred to server.

---

### 3. Create directory on server

```bash id="v9t3qe"
kukhta@ubuntu:~$ ssh myserver
user@server:~$ mkdir sync_folder
```

**Comment:** Directory for synchronization created.

---

### 4. Sync folder using rsync

```bash id="w2r7lp"
kukhta@ubuntu:~$ rsync -av ~/Documents/ user@192.168.1.200:/home/user/sync_folder/
sending incremental file list
notes.txt
project.txt
```

**Comment:** Files synchronized to remote directory.

---

### 5. Verify files using sftp

```bash id="j6n1hz"
kukhta@ubuntu:~$ sftp myserver
sftp> ls
sync_folder  test.txt

sftp> ls sync_folder
notes.txt  project.txt
```

**Comment:** Files are present on server, verified via SFTP.

---

## Summary

* Local IP: **192.168.1.105**
* Internet: **Available**
* Listening service: **sshd (port 22)**
* SSH Host: **myserver**
* Passwordless login: **Working**
* Remote path: **/home/user/sync_folder/**
* Verification command: **sftp ls**
