# 🌍 Real-World Scenario (Cloud Security Edition)
## Fix Security Misconfigurations in a Production Log Folder

---

## 📌 Situation
You are a **Cloud Security Engineer** responsible for a Linux server used by three teams:

- **webteam** → Developers  
- **ops** → Operations team  
- **audit** → Compliance & Security team  

All teams store logs and reports in:

A security issue is reported in production:

❌ Anyone can delete anyone’s files  
❌ Non-team users can read confidential logs  
❌ Files belong to incorrect users  
❌ Folder permissions are dangerously set to `777`  
❌ New files are created with insecure permissions (`666`)  

This is a **real-world cloud incident** seen in AWS EC2, Azure VMs, and GCP Compute.

---

## 🎯 Objective
Fix ownership and permissions so that:

- Only authorized teams can access logs
- No one can delete files they don’t own
- Logs are protected from tampering
- New files are created securely
- Running services are NOT affected

---

## 🧩 Step-by-Step Remediation

### 🔹 Step 1: Create the Broken Production Folder (Simulation)
```bash
sudo mkdir -p /srv/app_logs
tep 2: Simulate Insecure Permissions
sudo chmod 777 /srv/app_logs
sudo chown nobody:nogroup /srv/app_logs
Step 3: Investigate the Folder (Security Audit)
sudo ls -ld /srv/app_logs
Observed:
drwxrwxrwx 3 nobody nogroup ...
Problems Identified
Issue	Risk
777 permissions	Anyone can delete or modify logs
nobody:nogroup ownership	No accountability
No sticky bit	Files can be deleted by others
No team group	Broken access structure
No umask	New files created as 666
Step 4: Create a Proper Security Group
sudo groupadd appsec
Add all teams:
sudo usermod -aG appsec webteam
sudo usermod -aG appsec ops
sudo usermod -aG appsec audit
Verify:
grep appsec /etc/group
Step 5: Fix Folder Ownership
sudo chown root:appsec /srv/app_logs
Meaning:
root → administrator control
appsec → authorized team access
Step 6: Apply Strong Permissions (Cloud Standard)
sudo chmod 770 /srv/app_logs
Result:
drwxrwx---  root appsec
Owner → full access
Group → full access
Others → blocked
Step 7: Enable Sticky Bit (CRITICAL)
sudo chmod +t /srv/app_logs
Now:
drwxrwx--t
Sticky bit prevents users from deleting files they don’t own
This is how /tmp and secure cloud log directories work.
Step 8: Fix All Existing Files
sudo chown -R root:appsec /srv/app_logs
Ensures consistent ownership across the folder.
🛡 Step 9: Set Secure Umask (Temporary Test)
umask 007
Test file creation:
sudo touch /srv/app_logs/test_log.txt
sudo ls -l /srv/app_logs
Expected:
-rw-rw----
✔ Owner & group can read/write
Others blocked
Step 10: Validate Access (Production Test)
As webteam:
su - webteam
touch /srv/app_logs/web_log.txt
exit
As ops:
su - ops
touch /srv/app_logs/ops_log.txt
exit
As audit:
su - audit
rm /srv/app_logs/web_log.txt
Expected:
rm: cannot remove 'web_log.txt': Operation not permitted
Sticky bit protection confirmed.
Security Report Summary
Control	Status
Folder ownership	✔ root:appsec
Permissions	✔ 770 + sticky bit
Team access	✔ Restricted
Deletion protection	✔ Enabled
Secure file creation	✔ umask 007
Misconfigurations	✔ Fixed
Final Confirmation
echo "Real-World Scenario Completed Successfully – Cloud Log Security Fixed!" > success_fix_security_misconfigurations.txt
cat success_fix_security_misconfigurations.txt
