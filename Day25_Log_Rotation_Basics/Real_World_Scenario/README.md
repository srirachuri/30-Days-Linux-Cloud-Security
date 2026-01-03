# 🌍 Real-World Scenario (Cloud Security Edition)
## 🚨 Server Disk Full Alert – Security Logs Growing Uncontrollably

---

## 📌 Situation
You are a **Cloud Security / Linux Engineer** on call.

🚨 Monitoring alert reports:
> “Root partition is 92% full on production server.”

This is **critical**, because if disk usage reaches 100%:
- SSH access may stop
- Services can fail
- Logging stops → **security blind spot**

This scenario is very common in **AWS, Azure, and GCP production servers**.

---

## 🎯 Objective
- Confirm disk usage
- Identify which directory is consuming space
- Detect abnormal log growth
- Fix log rotation safely
- Prevent future disk exhaustion
- Document the incident clearly

---

## 🔎 Incident Response – Step by Step

---

### 🔹 Step 1: Confirm Disk Usage
```bash
df -h
Step 2: Identify Log Growth
sudo du -sh /var/log/*
📌 Example result:
12G  /var/log/auth.log
🚩 Red Flag
auth.log growing uncontrollably
Indicates log rotation problem
Security logs are filling the disk
🔹 Step 3: Inspect Logrotate Configuration
Check global configuration:
cat /etc/logrotate.conf
Verify:
Rotation frequency
Retention count
Compression settings
Check service-specific configs:
ls /etc/logrotate.d
cat /etc/logrotate.d/rsyslog
Step 4: Fix the Issue (Safe Configuration Change)
Edit logrotate configuration:
sudo nano /etc/logrotate.d/syslog
Update configuration:
/var/log/auth.log {
    weekly
    rotate 8
    compress
    missingok
    notifempty
}
🧪 Step 5: Validate Safely (NO BREAKAGE)
Dry run (no changes applied):
sudo logrotate -d /etc/logrotate.conf
✔ Confirms:
Logs will rotate correctly
Old logs will be compressed
Disk usage will reduce
(force run – only with approval):
sudo logrotate -f /etc/logrotate.conf
Step 6: Fix the Issue (Safe Configuration Change)
Edit logrotate configuration:
sudo nano /etc/logrotate.d/syslog
Update configuration:
/var/log/auth.log {
    weekly
    rotate 8
    compress
    missingok
    notifempty
}
Step 7 — Document the fix (VERY IMPORTANT)
You update the incident report:
Root Cause:
Auth logs are not rotating frequently and are not compressed.
Action Taken:
Updated logrotate rules for auth.log.
Result:
Disk usage stabilised.
Security logs are retained safely.
Step 8 — Write an Incident Note
echo "I Completed Logrotate configuration updated. Auth logs rotate weekly with compression enabled. Disk usage stabilized" > success_logrotate && cat success_logrotate
