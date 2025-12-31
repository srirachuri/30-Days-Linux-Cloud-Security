# Day 14: Mini Project - User Access Control 🔐

## 🎯 Goal
Simulate a real-world onboarding of two different employee roles with strictly defined access levels.

## 🏆 Project: Admin vs. Standard User
**Scenario:** Setting up an environment for a **SysAdmin** (Full Access) and a **Contractor** (Limited Access).

**Steps Taken:**
1. Created users `admin_user` and `contractor`.
2. Added `admin_user` to the `sudo` group.
3. Created a `sensitive_data` folder owned by root (700 permissions).
4. Verified `admin_user` could access it via sudo.
5. Verified `contractor` was denied access.

**Commands Used:**
```bash
sudo useradd -m admin_user
sudo usermod -aG sudo admin_user
sudo useradd -m contractor
mkdir /opt/sensitive_data
sudo chmod 700 /opt/sensitive_data
