# 🌟 Day 29 — Final Project  
## SSH into EC2 → Check Logs → Fix Permissions → Install a Package

---

## 📌 Project Overview
This final project simulates a **real production task** performed by a **Cloud Security / Linux Engineer**.

### Scenario
> “The EC2 server is running, but something feels off.  
> SSH in, check logs, fix unsafe permissions, and install a required package.”

This project demonstrates **end-to-end server access, security checks, system hardening, and service installation** on a live cloud VM.

---

## 🎯 Skills Demonstrated
- Secure SSH access to EC2
- Log inspection with a security mindset
- Fixing unsafe file permissions
- Correct ownership assignment
- Installing and validating services
- Production-style verification

This is **interview-level, real-job work**.

---

## 🧩 PART 1 — SSH into EC2 (Secure Access)

### Requirements
- EC2 Public IP
- `.pem` key file
- Correct username:
  - `ubuntu` → Ubuntu
  - `ec2-user` → Amazon Linux

### SSH Command
```bash
ssh -i mykey.pem ubuntu@<EC2_PUBLIC_IP>
PART 2 — Log Inspection (Security Mindset)
Check System Logs
sudo journalctl -xe
Check SSH & Authentication Logs
sudo cat /var/log/auth.log
PART 3 — Fix Unsafe Permissions (CRITICAL 🔐)
Simulate Bad Permissions
mkdir test_app
chmod 777 test_app
ls -ld test_app
Secure the Directory
chmod 755 test_app
sudo chown ubuntu:ubuntu test_app
ls -ld test_app
🧩 PART 3 — Fix Unsafe Permissions (CRITICAL 🔐)
Simulate Bad Permissions
mkdir test_app
chmod 777 test_app
ls -ld test_app
🧩 PART 4 — Install a Required Package
Update System Packages
sudo apt update
Install Nginx (Example Package)
sudo apt install nginx -y
Verify Service Status
sudo systemctl status nginx
PART 5 — Final Verification Checklist
Run and understand these commands:
whoami
pwd
ls -l
systemctl list-units --type=service --state=running
## Final Success Proof
echo "Day 29 Final Project completed successfully" > day29_success.txt
cat day29_success.txt
