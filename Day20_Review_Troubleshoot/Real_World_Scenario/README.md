# 🌍 Real-World Linux Troubleshooting  
## (Cloud / Security Engineer Mode)

---

## 📌 Situation (Very Realistic)
A **Junior Cloud Engineer** working on a cloud VM (AWS / Azure / GCP).

Your team reports:
> “The server is slow, and a monitoring tool stopped working.  
> Also, take a backup before touching anything.”

This is a **real-world production scenario** that cloud and security engineers face daily.

---

## 🎯 Objectives
- Check system health safely
- Identify problematic processes
- Fix stuck or unwanted processes
- Troubleshoot failed services
- Install missing tools
- Take backups before changes
- Check disk usage and clean safely
- Close the incident with proof

---

## 🧩 TASK 1 — Check System Health (FIRST RULE)
```bash
top
Exit top:
q
Rule: Observe first, act later.
 TASK 2 — Identify the Heavy Process (Evidence First)
ps aux --sort=-%cpu | head
ASK 3 — Fix a Stuck / Unwanted Process
Assume PID = 2345 (example).
Try graceful stop:
kill 2345
If it does not stop:
kill -9 2345
Verify:
ps aux | grep 2345
✔ If the process is gone → problem resolved
TASK 4 — Service Not Responding (Very Common)
Example service: cron (could also be SSH / nginx).
Check service status:
sudo systemctl status cron
If inactive or failed:
sudo systemctl restart cron
Check logs:
sudo journalctl -u cron -xe
 This is incident troubleshooting, not just command practice.
TASK 5 — Tool Missing (Production Readiness)
Your lead asks:
“Install a small tool for checking folders.”
Update packages:
sudo apt update
Install tool:
sudo apt install tree
Verify:
tree
Check installation proof:
dpkg -l | grep tree
TASK 6 — TAKE A BACKUP (VERY IMPORTANT)
Before making big changes, always back up.
tar -cvf day20_backup.tar day16_services day17_package_management
Verify backup:
ls -lh day20_backup.tar
TASK 7 — Disk Usage Check (Cloud Cost + Security)
df -h
If disk space is low:
sudo apt autoremove
sudo apt clean
Incident Closure Proof
echo "Day 20 Completed – Real World Linux Troubleshooting Done" > success_day20.txt && cat success_day20.txt
