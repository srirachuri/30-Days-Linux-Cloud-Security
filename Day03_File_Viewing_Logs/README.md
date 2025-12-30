# Day 03 – File Viewing & Reading Logs

## 🎯 Goal
Learn how to view file contents and monitor system logs without opening files in an editor.

---

## 🛠 Key Commands

- `cat` → Display full file content
- `less` → Scroll through files (↑ ↓, press `q` to quit)
- `more` → View files page by page
- `head` → Show first 10 lines
- `tail` → Show last 10 lines
- `tail -f` → Follow live log updates
- `sudo` → Run commands with administrator privileges

---

## 🧪 Step-by-Step Practice

### 1️⃣ Create workspace
```bash
mkdir day3_viewing
cd day3_viewing
echo "Linux Day 3 practice" > file1.txt
echo "Learning cat, less, head and tail" >> file1.txt
cat file1.txt
head file1.txt
tail file1.txt
less file1.txt
sudo tail -f /var/log/syslog


mkdir project3
cd project3
echo "This is file one about Linux commands." > file1.txt
echo "This is file two about system logs." > file2.txt
echo "This is file three about scripting practice." > file3.txt
cat file1.txt
head file2.txt
tail file3.txt
less /var/log/syslog
echo "I completed Linux Day 3" > success_day3.txt && cat success_day3.txt
