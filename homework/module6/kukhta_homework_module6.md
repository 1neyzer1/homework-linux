# Module 6 — Bash Scripting

**File:** kukhta_homework_module6.md

---

## Task — Backup Script

### 1. Script code (`backup.sh`)

```bash
#!/bin/bash

# Check arguments count
if [ "$#" -ne 2 ]; then
  echo "Usage: ./backup.sh <log_dir> <backup_dir>"
  exit 1
fi

LOG_DIR="$1"
BACKUP_DIR="$2"

# Check if directories exist
if [ ! -d "$LOG_DIR" ] || [ ! -d "$BACKUP_DIR" ]; then
  echo "Usage: ./backup.sh <log_dir> <backup_dir>"
  exit 1
fi

LOCK_FILE="/tmp/backup.lock"

# Check lock file
if [ -f "$LOCK_FILE" ]; then
  echo "Backup already running"
  exit 1
fi

# Create lock file
touch "$LOCK_FILE"

# Generate archive name with date
DATE=$(date +"%Y-%m-%d_%H-%M")
ARCHIVE_NAME="logs_backup_$DATE.tar.gz"
ARCHIVE_PATH="$BACKUP_DIR/$ARCHIVE_NAME"

# Create archive
tar -czf "$ARCHIVE_PATH" "$LOG_DIR" 2>/dev/null

# Check result
if [ "$?" -ne 0 ]; then
  echo "Backup failed"
  rm -f "$LOCK_FILE"
  exit 2
fi

echo "Backup created: $ARCHIVE_PATH"

# Remove lock file
rm -f "$LOCK_FILE"
```

---

## 2. Script execution examples

### Make script executable

```bash
kukhta@ubuntu:~$ chmod +x backup.sh
```

---

### Run with correct arguments

```bash
kukhta@ubuntu:~$ ./backup.sh /var/log /home/kukhta/backups
Backup created: /home/kukhta/backups/logs_backup_2026-04-23_12-30.tar.gz
```

---

### Run with wrong arguments

```bash
kukhta@ubuntu:~$ ./backup.sh
Usage: ./backup.sh <log_dir> <backup_dir>
```

---

### Run when lock file exists

```bash
kukhta@ubuntu:~$ touch /tmp/backup.lock
kukhta@ubuntu:~$ ./backup.sh /var/log /home/kukhta/backups
Backup already running
```

---

## 3. Description

This script creates a compressed backup of log files from a specified directory.

* It validates input arguments and checks directories.
* Uses a lock file to prevent parallel execution.
* Generates a timestamped archive in the backup directory.
* Verifies success of the operation and outputs the result.
