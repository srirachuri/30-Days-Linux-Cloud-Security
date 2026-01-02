# 🌍 REAL-WORLD SCENARIO (Cloud Security Edition)
## Securing a Newly Launched Cloud Server

---

## 📌 Situation
A **Cloud Security Engineer**.

Your company has just launched a **new Ubuntu server** for an application.
Before developers deploy anything, the server must be **hardened and secured**.

Your responsibility is to:
- Patch security vulnerabilities
- Install only essential tools
- Remove unnecessary software
- Ensure the server is clean and production-ready

This is **Day-1 hardening** for a cloud VM (AWS / Azure / GCP).

---

## 🎯 Security Objectives
✔ Update package index  
✔ Apply security patches  
✔ Install **only required tools**  
✔ Remove unused packages  
✔ Minimize attack surface  

---

## 🛠️ Step-by-Step Hardening (Follow in Order)

---

### 🔹 Step 1: Update Package List (MANDATORY)
```bash
sudo apt update
🔹 Step 2: Apply Security Updates
sudo apt upgrade
Step 3: Install Essential Tools (Minimum Only)
sudo apt install htop curl
Verify installation:
htop
curl --version
Step 4: Audit Installed Packages (Security Check)
apt list --installed
Filter specific packages:
dpkg -l | grep curl
dpkg -l | grep htop
🔹 Step 5: Remove Unnecessary Software
Assume curl is no longer required:
sudo apt purge curl
Clean leftovers:
sudo apt autoremove
sudo apt clean
Incident-Style Validation (Think Like Security)
Check for pending updates:
apt list --upgradable
Check disk usage:
df -h
✔ Disk space clean, no junk packages
Check package count:
dpkg -l | wc -l
✔ Controlled and expected package count
Final Proof
echo "Cloud Server Hardening Completed Successfully!" > success_realworld.txt && cat success_realworld.txt
