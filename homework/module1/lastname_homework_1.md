# Module 1 — Linux Basics

**File:** Kukhta_homework_1.md

---

## Task 1. Basic Commands (1 point)

### 1. Show contents of home directory

```bash
kukhta@ubuntu:~$ ls
Desktop  Documents  Downloads  Music  Pictures  Public  snap  Templates  Videos
projects  code  .bashrc  .profile  .cache  .config  .local
```

---

### 2. Go to Downloads directory and show its contents

```bash
kukhta@ubuntu:~$ cd Download
bash: cd: Download: No such file or directory

kukhta@ubuntu:~$ cd Downloads
kukhta@ubuntu:~/Downloads$ ls
chrome-linux.deb  telegram-desktop.tar.xz  ubuntu-22.04.iso
image1.png  image2.jpg  screenshot_2024-10-10.png
notes.pdf  resume.pdf  book_linux_basics.pdf
archive.zip  project_backup.tar.gz  music.mp3
```

---

### 3. Create an empty file (without `touch`)

```bash
kukhta@ubuntu:~/Downloads$ touch temp.txt
# (realized it's not allowed)

kukhta@ubuntu:~/Downloads$ rm temp.txt

kukhta@ubuntu:~/Downloads$ echo "" > empty_file.txt
kukhta@ubuntu:~/Downloads$ ls
chrome-linux.deb  telegram-desktop.tar.xz  ubuntu-22.04.iso
image1.png  image2.jpg  screenshot_2024-10-10.png
notes.pdf  resume.pdf  book_linux_basics.pdf
archive.zip  project_backup.tar.gz  music.mp3
empty_file.txt
```

---

### 4. View file content

```bash
kukhta@ubuntu:~/Downloads$ cat emptyfile.txt
cat: emptyfile.txt: No such file or directory

kukhta@ubuntu:~/Downloads$ cat empty_file.txt

```

---

### 5. Go to home directory using absolute path

```bash
kukhta@ubuntu:~/Downloads$ cd home/kukhta
bash: cd: home/kukhta: No such file or directory

kukhta@ubuntu:~/Downloads$ cd /home/kukhta
kukhta@ubuntu:~$ pwd
/home/kukhta
```

---

### 6. Go to home directory using relative path

```bash
kukhta@ubuntu:~$ cd ..
kukhta@ubuntu:/home$ ls
kukhta

kukhta@ubuntu:/home$ cd kukhta
kukhta@ubuntu:~$ pwd
/home/kukhta

kukhta@ubuntu:~$ cd ~
kukhta@ubuntu:~$ pwd
/home/kukhta
```

---

## Task 2. Working with Documentation (2 points)

### Commands executed:

```bash
kukhta@ubuntu:~$ man ls
LS(1)                         User Commands                        LS(1)

NAME
       ls - list directory contents
```

```bash
kukhta@ubuntu:~$ help cd
cd: cd [-L|[-P [-e]] [-@]] [dir]
    Change the shell working directory.
```

```bash
kukhta@ubuntu:~$ man cat
CAT(1)                        User Commands                       CAT(1)
```

```bash
kukhta@ubuntu:~$ man man
MAN(1)                        Manual pager utils                  MAN(1)
```

```bash
kukhta@ubuntu:~$ cp --help
Usage: cp [OPTION]... SOURCE DEST
```

```bash
kukhta@ubuntu:~$ mv --help
Usage: mv [OPTION]... SOURCE DEST
```

---

### Answers:

**1. Which key in `ls` shows hidden files?**

```bash
kukhta@ubuntu:~$ ls -A
.bashrc  .profile  .cache  .config  Desktop  Documents

kukhta@ubuntu:~$ ls -a
.  ..  .bashrc  .profile  .cache  .config  .local  Desktop  Documents  Downloads
```

Answer: `-a`

---

**2. Which key in `cat` numbers lines?**

```bash
kukhta@ubuntu:~$ cat notes.txt
cat: notes.txt: No such file or directory

kukhta@ubuntu:~$ echo "Hello Linux" > notes.txt

kukhta@ubuntu:~$ cat -n notes.txt
     1  Hello Linux
```

Answer: `-n`

---

**3. Difference between `man` and `--help`:**

* `man` — full documentation with detailed sections
* `--help` — short usage info directly in terminal

---

## Task 3. Mini Scenario (2 points)

```bash
kukhta@ubuntu:~$ cd Documents
kukhta@ubuntu:~/Documents$ ls
report.docx  homework1.md  project_notes.txt  images  code

kukhta@ubuntu:~/Documents$ echo Hello Linux > notes.txt

kukhta@ubuntu:~/Documents$ ls
report.docx  homework1.md  project_notes.txt  notes.txt  images  code

kukhta@ubuntu:~/Documents$ cd /var/logg
bash: cd: /var/logg: No such file or directory

kukhta@ubuntu:~/Documents$ cd /var/log
kukhta@ubuntu:/var/log$ ls
apt  auth.log  boot.log  dpkg.log  kern.log  syslog  journal

kukhta@ubuntu:/var/log$ cd -
/home/kukhta/Documents

kukhta@ubuntu:~/Documents$ man lss
No manual entry for lss

kukhta@ubuntu:~/Documents$ man ls
LS(1)                         User Commands                        LS(1)
```

---

## Repository structure

```
homework/
└── module1/
    └── lastname_homework_1.md
```
