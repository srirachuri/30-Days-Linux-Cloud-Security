# 🌍 Real-World Scenario (Cloud Security Edition)
## Backup Before Server Maintenance

---

## 📌 Situation
A **Cloud Security / Linux Engineer**.

Your team informs you:
> “We’re going to update the server tonight.  
> Take a backup of configs and logs before we touch anything.”

If the update fails, **the backup saves your job**.

This is a **real, mandatory task** performed before:
- OS upgrades
- Security patching
- Application deployments
- Risky configuration changes

---

## 🎯 Objective
You must:

✅ Back up important server data  
✅ Compress the backup to save space  
✅ Verify the backup exists  
✅ Test restore to ensure integrity  

---

## 🧠 What We Protect (Real Servers)

| Folder | Why It Matters |
|------|---------------|
| `/etc` | Configuration files (SSH, Nginx, system) |
| `/var/log` | Logs (security, audit, errors) |
| App folder | Application & business data |

⚠️ Losing:
- Configs → downtime  
- Logs → no investigation  
- App data → business loss  

We simulate everything **safely** (no system damage).

---

## 🧩 STEP 1 — Simulate Critical Server Data
```bash
mkdir etc_backup var_log_backup app_data
Create sample configuration files
touch etc_backup/ssh_config
touch etc_backup/nginx.conf
Create sample log files
touch var_log_backup/auth.log
touch var_log_backup/syslog
Create application data
touch app_data/users.db
touch app_data/config.env
STEP 3 — Create a Compressed Backup
tar -czvf server_backup_$(date +%F).tar.gz \
etc_backup var_log_backup app_data
Command Breakdown
tar → archive tool
-c → create archive
-z → gzip compression (saves space)
-v → verbose (shows files being backed up)
-f → specify filename
STEP 4 — Verify Backup Exists
ls -lh server_backup_*.tar.gz
STEP 5 — TEST RESTORE (MOST IMPORTANT)
mkdir restore_test
Never restore directly over real data.
tar -xzvf server_backup_*.tar.gz -C restore_test
-x → extract
-z → decompress gzip
-v → show restored files
-f → backup file
-C restore_test → restore into safe directory
Verify:
ls restore_test
Expected:
etc_backup  var_log_backup  app_data
Cloud rule: Never trust a backup you didn’t restore-test.
Final Proof
echo "Day 19 Real-World Scenario Completed – Server Backup Secured!" > success_day19_realworld.txt && cat success_day19_realworld.txt
