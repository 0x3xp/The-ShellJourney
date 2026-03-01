# Basic Linux Commands

Linux terminal commands are the foundation of shell scripting. A script is essentially a sequence of Linux commands executed automatically. Understanding these commands deeply allows you to automate tasks, analyze systems, and manipulate data efficiently.

This module introduces essential commands grouped by purpose.

---

# Viewing and Reading File Content

## `cat` – Concatenate and Display Files

Displays the full contents of a file.

```bash
cat file.txt
```

It can also combine multiple files:

```bash
cat file1.txt file2.txt
```

⚠️ Not ideal for very large files.

---

## `more` – Paginated Viewing

Displays file content one screen at a time.

```bash
more largefile.txt
```

Press:
- `Space` → Next page
- `q` → Quit

---

## `less` – Advanced Pager

Improved version of `more`.

```bash
less largefile.txt
```

Features:
- Scroll forward and backward
- Search using `/keyword`
- Exit using `q`

Preferred for large log files.

---

## `head` – View Beginning of File

```bash
head file.txt
head -n 5 file.txt
```

Useful for quickly inspecting file headers.

---

## `tail` – View End of File

```bash
tail file.txt
tail -n 10 file.txt
```

Monitor logs in real-time:

```bash
tail -f /var/log/syslog
```

Very important in monitoring and security analysis.

---

# File and Directory Operations

## `ls` – List Directory Contents

```bash
ls
ls -l
ls -a
ls -lh
```

Common flags:
- `-l` → Long format
- `-a` → Show hidden files
- `-h` → Human-readable sizes

---

## `cd` – Change Directory

```bash
cd Documents
cd ..
cd ~
```

- `..` → Move up one directory
- `~` → Home directory

---

## `pwd` – Print Working Directory

```bash
pwd
```

Displays current path.

---

## `mkdir` – Create Directory

```bash
mkdir newfolder
mkdir -p parent/child
```

`-p` creates nested directories if needed.

---

## `rmdir` – Remove Empty Directory

```bash
rmdir foldername
```

Directory must be empty.

---

## `rm` – Remove Files or Directories

```bash
rm file.txt
rm -r folder
rm -rf folder
```

⚠️ `-rf` permanently deletes recursively. Use carefully.

---

## `cp` – Copy Files or Directories

```bash
cp file.txt backup.txt
cp -r folder1 folder2
```

---

## `mv` – Move or Rename

```bash
mv old.txt new.txt
mv file.txt /tmp/
```

---

## `touch` – Create File or Update Timestamp

```bash
touch newfile.txt
```

---

# Searching and Filtering Data

These commands are extremely powerful in scripting.

## `grep` – Search for Patterns

```bash
grep "error" logfile.txt
grep -i "admin" users.txt
grep -r "password" /home
```

Flags:
- `-i` → Case insensitive
- `-r` → Recursive search

Common in log analysis.

---

## `sort` – Sort File Content

```bash
sort file.txt
sort -n numbers.txt
```

`-n` → Numeric sort

---

## `wc` – Word Count

```bash
wc file.txt
wc -l file.txt
```

Counts:
- Lines
- Words
- Characters

---

## `cut` – Extract Columns

```bash
cut -d"," -f1 file.csv
```

- `-d` → Delimiter
- `-f` → Field number

Very useful for parsing structured text.

---

## `awk` – Pattern Scanning and Processing

```bash
awk '{print $1}' file.txt
```

Prints first column of each line.

Powerful text processing tool often used in automation.

---

## `sed` – Stream Editor

```bash
sed 's/admin/user/g' file.txt
```

Replaces all occurrences of "admin" with "user".

Used for:
- Editing text streams
- Modifying configuration files

---

# Disk and System Information

## `du` – Disk Usage

```bash
du -h
du -sh folder
```

Shows space used by files/directories.

---

## `df` – Disk Free Space

```bash
df -h
```

Displays filesystem storage usage.

---

## `free` – Memory Usage

```bash
free -h
```

Shows RAM usage.

---

## `uptime` – System Running Time

```bash
uptime
```

Displays how long system has been running.

---

## `whoami` – Current User

```bash
whoami
```

---

## `id` – User Identity Information

```bash
id
```

Shows:
- UID
- GID
- Group memberships

Important in permission auditing.

---

# File Permissions and Ownership

## `chmod` – Change Permissions

Symbolic mode:

```bash
chmod u+x script.sh
```

Numeric mode:

```bash
chmod 755 script.sh
```

Permission breakdown:
- 7 = read + write + execute
- 5 = read + execute
- 4 = read only

---

## `chown` – Change Owner

```bash
chown user file.txt
chown user:group file.txt
```

---

## `chgrp` – Change Group

```bash
chgrp developers file.txt
```

---

# Linking Files

## `ln` – Create Links

Hard link:

```bash
ln source.txt hardlink.txt
```

Symbolic link:

```bash
ln -s source.txt symlink.txt
```

Symbolic links are commonly used in configuration management.

---

# Archiving and Compression

## `tar` – Archive Files

Create archive:

```bash
tar -cvf archive.tar folder/
```

Extract archive:

```bash
tar -xvf archive.tar
```

Compressed archive:

```bash
tar -czvf archive.tar.gz folder/
```

---

# Finding Files

## `locate` – Fast File Search

```bash
locate file.txt
```

May require database update:

```bash
sudo updatedb
```

---

## `find` – Advanced Search

```bash
find /home -name "file.txt"
find . -type f -size +10M
```

Powerful for automation and forensic analysis.

---

# Manual Pages

## `man` – Command Documentation

```bash
man ls
```

Every serious Linux user must know how to read manual pages.

---

# Output and Redirection Basics

## `echo` – Print Text

```bash
echo "Hello"
```

Redirect output:

```bash
echo "Log entry" >> logfile.txt
```

---

# Why These Commands Matter in Shell Scripting

Shell scripts combine these commands to:

- Automate backups
- Monitor logs
- Process data
- Manage users
- Analyze system state
- Perform administrative tasks

Mastering these commands is essential before moving to advanced scripting logic.

---

# Summary

In this module, you learned:

- How to view and manipulate files
- How to navigate directories
- How to search and filter text
- How to manage permissions
- How to inspect system resources
- How to archive and compress data
- How to combine commands for automation

These tools form the operational toolkit of any Linux user and are the backbone of effective shell scripting.
