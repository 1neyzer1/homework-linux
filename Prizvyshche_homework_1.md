# Module 1 — Linux Basics

**File:** Kukhta_homework_1.md

---

## Task 1. Basic Commands (1 point)

### 1. Show contents of home directory

```bash
student@ubuntu:~$ ls
Desktop  Documents  Downloads  Music  Pictures  Public  snap  Templates  Videos
projects  code  .bashrc  .profile  .cache  .config  .local
```

---

### 2. Go to Downloads directory and show its contents

```bash
student@ubuntu:~$ cd Download
bash: cd: Download: No such file or directory

student@ubuntu:~$ cd Downloads
student@ubuntu:~/Downloads$ ls
chrome-linux.deb  telegram-desktop.tar.xz  ubuntu-22.04.iso
image1.png  image2.jpg  screenshot_2024-10-10.png
notes.pdf  resume.pdf  book_linux_basics.pdf
archive.zip  project_backup.tar.gz  music.mp3
```

---

### 3. Create an empty file (without `touch`)

```bash
student@ubuntu:~/Downloads$ touch temp.txt
# (realized it's not allowed)

student@ubuntu:~/Downloads$ rm temp.txt

student@ubuntu:~/Downloads$ echo "" > empty_file.txt
student@ubuntu:~/Downloads$ ls
chrome-linux.deb  telegram-desktop.tar.xz  ubuntu-22.04.iso
image1.png  image2.jpg  screenshot_2024-10-10.png
notes.pdf  resume.pdf  book_linux_basics.pdf
archive.zip  project_backup.tar.gz  music.mp3
empty_file.txt
```

---

### 4. View file content

```bash
student@ubuntu:~/Downloads$ cat emptyfile.txt
cat: emptyfile.txt: No such file or directory

student@ubuntu:~/Downloads$ cat empty_file.txt

```

---

### 5. Go to home directory using absolute path

```bash
student@ubuntu:~/Downloads$ cd home/student
bash: cd: home/student: No such file or directory

student@ubuntu:~/Downloads$ cd /home/student
student@ubuntu:~$ pwd
/home/student
```

---

### 6. Go to home directory using relative path

```bash
student@ubuntu:~$ cd ..
student@ubuntu:/home$ ls
student

student@ubuntu:/home$ cd student
student@ubuntu:~$ pwd
/home/student

student@ubuntu:~$ cd ~
student@ubuntu:~$ pwd
/home/student
```

---

## Task 2. Working with Documentation (2 points)

### Commands executed:

```bash
student@ubuntu:~$ man ls
LS(1)                         User Commands                        LS(1)

NAME
       ls - list directory contents
```

```bash
student@ubuntu:~$ help cd
cd: cd [-L|[-P [-e]] [-@]] [dir]
    Change the shell working directory.
```

```bash
student@ubuntu:~$ man cat
CAT(1)                        User Commands                       CAT(1)
```

```bash
student@ubuntu:~$ man man
MAN(1)                        Manual pager utils                  MAN(1)
```

```bash
student@ubuntu:~$ cp --help
Usage: cp [OPTION]... SOURCE DEST
```

```bash
student@ubuntu:~$ mv --help
Usage: mv [OPTION]... SOURCE DEST
```

---

### Answers:

**1. Which key in `ls` shows hidden files?**

```bash
student@ubuntu:~$ ls -A
.bashrc  .profile  .cache  .config  Desktop  Documents

student@ubuntu:~$ ls -a
.  ..  .bashrc  .profile  .cache  .config  .local  Desktop  Documents  Downloads
```

Answer: `-a`

---

**2. Which key in `cat` numbers lines?**

```bash
student@ubuntu:~$ cat notes.txt
cat: notes.txt: No such file or directory

student@ubuntu:~$ echo "Hello Linux" > notes.txt

student@ubuntu:~$ cat -n notes.txt
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
student@ubuntu:~$ cd Documents
student@ubuntu:~/Documents$ ls
report.docx  homework1.md  project_notes.txt  images  code

student@ubuntu:~/Documents$ echo Hello Linux > notes.txt

student@ubuntu:~/Documents$ ls
report.docx  homework1.md  project_notes.txt  notes.txt  images  code

student@ubuntu:~/Documents$ cd /var/logg
bash: cd: /var/logg: No such file or directory

student@ubuntu:~/Documents$ cd /var/log
student@ubuntu:/var/log$ ls
apt  auth.log  boot.log  dpkg.log  kern.log  syslog  journal

student@ubuntu:/var/log$ cd -
/home/student/Documents

student@ubuntu:~/Documents$ man lss
No manual entry for lss

student@ubuntu:~/Documents$ man ls
LS(1)                         User Commands                        LS(1)
```

---

## Repository structure

```
homework/
└── module1/
    └── lastname_homework_1.md
```
