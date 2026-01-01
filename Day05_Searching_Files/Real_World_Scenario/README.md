# 🌍 Cloud Security Real-World Scenario  
## Investigating Suspicious SSH Login Attempts

You are a **Cloud Security Trainee** managing a Linux server on **AWS**.  
The system administrator suspects a **brute-force SSH attack**.

Your task is to analyze authentication logs, detect suspicious activity,
and prepare a basic security audit.

---

## 🎯 Objectives
- Detect failed SSH login attempts
- Identify attacking IP addresses
- Count attack frequency
- Detect successful logins
- Identify targeted usernames
- Save audit evidence

---

## 📁 Log File Location
- Ubuntu / Debian: `/var/log/auth.log`
- RedHat / CentOS: `/var/log/secure`

---

## 🧩 Step-by-Step Investigation

### 🔹 1. Locate the SSH Authentication Log
```bash
sudo cat /var/log/auth.log
2. Search for Failed SSH Login Attempts
sudo grep "Failed password" /var/log/auth.log
Explanation:
"Failed password" → logged for incorrect SSH passwords
auth.log → authentication activity log
🔹 3. Count Total Failed Login Attempts
sudo grep "Failed password" /var/log/auth.log | wc -l
✅ Displays total failed attempts.
🔹 4. Identify Attacking IP Addresses
sudo grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}' | sort | uniq -c | sort -nr | head
Explanation:
awk '{print $(NF-3)}' → extracts IP address
uniq -c → counts attempts per IP
sort -nr → highest frequency first
head → top attackers
Sample Output:
15 192.168.1.55
8  102.43.78.10
3  45.76.21.90
🔹 5. Search for Successful SSH Logins
sudo grep "Accepted password" /var/log/auth.log
Unknown IPs or users may indicate unauthorized access.
6. Identify Targeted Usernames
sudo grep "Failed password" /var/log/auth.log | awk '{print $(NF-5)}' | sort | uniq -c | sort -nr
Reveals commonly targeted usernames such as:
root
admin
user
7. Save Audit Findings
mkdir ssh_audit
cd ssh_audit
sudo grep "Failed password" /var/log/auth.log > failed_logins.txt
sudo grep "Accepted password" /var/log/auth.log > successful_logins.txt
8. Confirmation Message
echo "Cloud Security Audit - SSH Log Analysis Completed Successfully" > success_day5_cloud.txt && cat success_day5_cloud.txt
