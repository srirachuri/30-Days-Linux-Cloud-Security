## ☁️ Cloud Security Add-On – Log Backup & Error Verification

### 🌍 Scenario
**log preservation and inspection**
before troubleshooting or incident response.

Before analyzing logs directly in `/var/log`, you create a safe backup copy
and scan for potential error messages.

---

### Step 1: Create a Backup Folder
```bash
mkdir ~/logs_backup
Step 2: Copy All .log Files from /var/log
sudo cp /var/log/*.log ~/logs_backup/
Copies all log files into the backup folder for safe analysis.
Step 3: Copy a Specific Log File (Example: syslog)
sudo cp /var/log/syslog ~/logs_backup/
Used when you want to investigate a particular log.
Step 4: Move into the Backup Directory
cd ~/logs_backup
Step 5: Search for Error Messages
grep "error" *.log
Searches all copied log files for error entries
(Case-sensitive)

Case-Insensitive Search
grep -i "error" *.log
