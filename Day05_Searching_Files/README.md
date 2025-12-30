# Day 05 – Searching Files & Logs 🔍

## 🎯 Goal
Learn how to search for files and find specific words inside them — a critical skill for Linux and cloud troubleshooting.

---

## 🛠 Commands Practiced

- `grep` → Search for text patterns inside files
- `find` → Search files by name, type, or size (real-time)
- `locate` → Quickly find files using a database
- `updatedb` → Update the locate database

---

## 🔍 grep Examples

```bash
grep "Linux" *.txt
grep -i "linux" *.txt        # Case-insensitive
grep -n "linux" *.txt        # Show line numbers
grep -r "linux" /etc         # Recursive search
find . -name "*.txt"
find / -type f -name "sshd_config" 2>/dev/null
find /var/log -size +1M
sudo apt install plocate
sudo updatedb
locate sshd_config
sudo grep "Failed password" /var/log/auth.log
grep -i "error" /var/log/syslog

mkdir project5
cd project5
touch report1.txt report2.txt report3.txt
echo "security" > report1.txt
echo "cloud" > report2.txt
grep "cloud" *.txt
find . -name "*.txt"
echo "I completed Linux Day 5" > success_day5.txt && cat success_day5.txt
