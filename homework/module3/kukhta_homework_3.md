# Module 3 — Processes and System Monitoring

**File:** kukhta_homework_3.md

---

## Task 1. Active Processes Overview (2 points)

### 1. Show all processes using ps

```bash id="p1k3d9"
kukhta@ubuntu:~$ ps aux | head
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.1 169456  1132 ?        Ss   10:00   0:01 /sbin/init
root       523  0.0  0.3  50000  3500 ?        Ss   10:00   0:02 /usr/lib/systemd/systemd-journald
kukhta    1023  0.1  1.2 275000 12000 ?        Sl   10:05   0:05 gnome-terminal
kukhta    1102  0.0  0.2  21000  2200 pts/0    Ss   10:06   0:00 bash
```

---

### 2. Run top and find process using most RAM

```bash id="o8q7lv"
kukhta@ubuntu:~$ top
top - 10:15:32 up  2:10,  1 user,  load average: 0.15, 0.10, 0.08

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
 1500 kukhta    20   0  350000  20000  15000 S   0.5  2.0   0:03.11 chrome
 1023 kukhta    20   0  275000  12000   9000 S   1.0  1.2   0:05.32 gnome-terminal
```

Process using most RAM: **chrome (PID 1500)**

---

### 3. Find PID of current shell

```bash id="2yfs6c"
kukhta@ubuntu:~$ echo $$
1102
```

---

## Task 2. Background Jobs and Process Control (2 points)

```bash id="0sdz7p"
kukhta@ubuntu:~$ sleep 1000 &
[1] 2001

kukhta@ubuntu:~$ jobs
[1]+  Running                 sleep 1000 &

kukhta@ubuntu:~$ fg %1
sleep 1000
^Z
[1]+  Stopped                 sleep 1000

kukhta@ubuntu:~$ kill %1
[1]+  Terminated              sleep 1000
```

---

### nohup example

```bash id="1w5kqt"
kukhta@ubuntu:~$ nohup sleep 500 &
[1] 2100
nohup: ignoring input and appending output to 'nohup.out'
```

---

## Task 3. Priorities and Limits (4 points)

### 1. Run command with lower priority

```bash id="3x7cve"
kukhta@ubuntu:~$ nice -n 10 sleep 300 &
[1] 2200
```

---

### 2. Change priority of running process

```bash id="2snk7q"
kukhta@ubuntu:~$ renice 5 -p 2200
2200 (process ID) old priority 10, new priority 5
```

---

### 3. Show user limits

```bash id="8bpm3a"
kukhta@ubuntu:~$ ulimit -a
core file size          (blocks, -c) 0
data seg size           (kbytes, -d) unlimited
file size               (blocks, -f) unlimited
max user processes              (-u) 30922
open files                      (-n) 1024
stack size              (kbytes, -s) 8192
```

---

## Task 4. Resource Monitoring (2 points)

### 1. Disk usage

```bash id="1h5y4k"
kukhta@ubuntu:~$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G   20G   28G  42% /
tmpfs           2.0G  1.2M  2.0G   1% /run
```

---

### 2. RAM usage

```bash id="zv3r1p"
kukhta@ubuntu:~$ free -h
              total        used        free      shared  buff/cache   available
Mem:           7.7G        2.1G        3.5G        200M        2.1G        5.0G
Swap:          2.0G          0B        2.0G
```
