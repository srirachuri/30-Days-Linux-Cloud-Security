# 🌍 REAL-WORLD CLOUD SCENARIO
## Secure a RedHat-Based Cloud Server Using Package Management

---

## 🎯 Scenario (Real World)
A **Cloud Security Engineer** assigned a **new RedHat-based cloud server**
(RHEL / CentOS / Rocky Linux / AlmaLinux / Amazon Linux).

Before handing the server to developers, your responsibilities are to:
- Update package metadata
- Install only required tools
- Audit installed packages
- Remove unnecessary software
- Leave the server **clean, minimal, and secure**

This is **Day-1 hardening** performed in real cloud jobs.

---

## 🎯 Security Objectives
✔ Identify the operating system correctly  
✔ Refresh package metadata  
✔ Install a required monitoring tool  
✔ Audit package details and files  
✔ Remove unnecessary packages  
✔ Clean package cache  

---

## 🛠️ Step-by-Step Hardening (Production Safe)

---

### 🔹 STEP 1: Identify the Operating System (CRITICAL)
```bash
cat /etc/os-release
STEP 2: Refresh Package Metadata
sudo dnf makecache
STEP 3: Install a Required Monitoring Tool
We install htop, a safe and common monitoring tool.
sudo dnf install htop
Verify:
htop
Press q to exit.
STEP 4: Security Audit (VERY IMPORTANT)
🔍 4.1 Check if the Package Is Installed
rpm -q htop
🔍 4.2 View Package Details
rpm -qi htop
Check:
Name
Version
Vendor / Repository
Confirms the package came from a trusted source.
🔹 STEP 5: Check Installed Files (Security Check)
rpm -ql htop | head
🔹 STEP 6: Remove an Unnecessary Package
Assume monitoring is no longer required.
sudo dnf remove htop
🔹 STEP 7: Clean Package Cache (Hardening Step)
sudo dnf clean all
🔹 STEP 8: Final Verification
rpm -q htop
Expected:
package htop is not installed
Final Proof
echo "Completed Securing a RedHat-Based Cloud Server Successfully!" > success_redhat.txt
cat success_redhat.txt
