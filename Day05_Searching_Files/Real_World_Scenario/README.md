# Cloud Security Real-World Scenario – SSH Log Analysis

## 🌍 Scenario: Investigating Suspicious SSH Login Attempts

You are a **Cloud Security Trainee** managing a Linux server on **AWS**.  
The system administrator suspects that an attacker is attempting to
**brute-force SSH passwords**.

Your responsibility is to investigate authentication logs, identify
failed and successful login attempts, and trace suspicious IP addresses.

This simulates **real-world security monitoring and incident investigation**.

---

## 🎯 Goals
- Detect failed SSH login attempts
- Identify source IP addresses
- Count frequency of attacks
- Detect successful logins
- Identify targeted usernames
- Prepare a basic audit report

---

## 📁 Log File Locations
- **Debian / Ubuntu:** `/var/log/auth.log`
- **RedHat / CentOS:** `/var/log/secure`

---
## 🧩 Step-by-Step Investigation
### 1. Locate the SSH Authentication Log
sudo cat /var/log/auth.log
2. Search for Failed SSH Login Attempts
sudo grep "Failed password" /var/log/auth.log
📘 Explanation:
"Failed password" → logged when an incorrect password is entered
/var/log/auth.log → authentication event log
🧮 3. Count Total Failed Login Attempts
sudo grep "Failed password" /var/log/auth.log | wc -l
✅ Displays the total number of failed SSH attempts.
🌍 4. Identify Attacking IP Addresses
sudo grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}' | sort | uniq -c | sort -nr | head
📘 Explanation:
awk '{print $(NF-3)}' → extracts IP addresses
uniq -c → counts attempts per IP
sort -nr → sorts by frequency (highest first)
head → shows top attackers
✅ Sample Output:
15 192.168.1.55
8  102.43.78.10
3  45.76.21.90
🔒 5. Search for Successful SSH Logins
sudo grep "Accepted password" /var/log/auth.log
⚠️ Unknown users or IPs here may indicate unauthorized access.
⚙️ 6. Identify Targeted Usernames
sudo grep "Failed password" /var/log/auth.log | awk '{print $(NF-5)}' | sort | uniq -c | sort -nr
This reveals commonly attacked usernames such as:
root
admin
user
🧰 7. Save Audit Findings
mkdir ssh_audit
cd ssh_audit
sudo grep "Failed password" /var/log/auth.log > failed_logins.txt
sudo grep "Accepted password" /var/log/auth.log > successful_logins.txt
📁 Audit files created:
failed_logins.txt
successful_logins.txt
✅ 8. Confirmation Message
echo "Cloud Security Audit - SSH Log Analysis Completed Successfully" > success_day5_cloud.txt && cat success_day5_cloud.txt
