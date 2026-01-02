# 🌍 Real-World Scenario (Cloud Security Edition)
## Secure Admin Access on a Cloud Server

---

## 🔐 Situation
You are a **Cloud Security Engineer** managing an **Ubuntu server on AWS**.

Three users work on the system, each with different responsibilities:

- **devops** → needs full administrative access  
- **developer** → needs to install/update packages only  
- **auditor** → must read logs but never modify the system  

Your task is to configure **secure sudo access** following the
**principle of least privilege**.

This mirrors how real teams operate in AWS, Azure, and GCP.

---

## 🎯 Objective
Configure sudo rules so that:

✔ **devops**
- Full admin (root-level) access  

✔ **developer**
- Can run `apt update` / `apt install`
- ❌ Cannot restart services
- ❌ Cannot edit system files

✔ **auditor**
- Can read logs using `journalctl` and `tail`
- ❌ Cannot run any other sudo commands

---

## 🛠️ Step-by-Step Solution

### 🔹 Step 1: Create Users
```bash
sudo useradd -m devops1
sudo useradd -m developer1
sudo useradd -m auditor1
Set passwords:
sudo passwd devops1
sudo passwd developer1
sudo passwd auditor1
🔹 Step 2: Give devops1 Full Sudo Access
sudo usermod -aG sudo devops1
Safest method (uses default sudo group).
Now devops1 can run:
sudo systemctl restart ssh
sudo cat /etc/shadow
sudo apt upgrade
🔹 Step 3: Give developer1 LIMITED Sudo Access
Open sudo configuration safely:
sudo visudo
Add:
developer1 ALL=(ALL) NOPASSWD: /usr/bin/apt, /usr/bin/apt-get
🔹 Step 4: Give auditor1 Read-Only Log Access
Open visudo again:
sudo visudo
Add:
auditor1 ALL=(ALL:ALL) NOPASSWD: /usr/bin/journalctl, /usr/bin/tail
🔍 Step 5: Test Like a Real Security Engineer
🧪 Test as developer1
su - developer1
sudo apt update                # ✔ Works
sudo systemctl restart ssh     # ❌ Permission denied
🧪 Test as auditor1
su - auditor1
sudo journalctl -xe             # ✔ Works
sudo tail /var/log/syslog       # ✔ Works
sudo apt install nginx          # ❌ Not allowed
🧪 Test as devops1
su - devops1
sudo systemctl restart nginx    # ✔ Works
Final Confirmation
echo "Real-World Scenario Completed Successfully!" > success_sudo.txt && cat success_sudo.txt
