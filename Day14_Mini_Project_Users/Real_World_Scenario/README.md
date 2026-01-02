# 🌍 REAL-WORLD SCENARIO (Cloud Security Edition)
## Create a Secure Admin-Only Workspace on a Cloud Server

---

## 🎯 Situation
A **Cloud Security Engineer** managing a Linux server.

Your company has two roles:

- **admin14** → Cloud Administrator  
- **user14** → Normal employee (developer / analyst)

The administrator must store highly sensitive data such as:
- Audit notes  
- Security reports  
- Root-cause analysis  
- Credentials or configuration backups  

These files must be **100% private**.

❌ The normal user must NOT be able to:
- See the folder  
- Enter the folder  
- List files  
- Read or edit files  
- Delete anything  

This setup mirrors real secure directories such as:
- `/root`
- `/var/secure`
- `/etc/audit`
- `/srv/admin_data`

---

## ✅ Objectives
You must:

✔ Create two users: `admin14` and `user14`  
✔ Create a secure folder `/srv/admin_data`  
✔ Allow **only admin14** to read and write  
✔ Deny **all access** to user14  
✔ Show proof of **Permission denied**  
✔ Follow cloud security best practices (`700`, correct ownership, least privilege)

---

## 🚀 Step-by-Step Implementation (Real-World Setup)

### 🔹 Step 1: Create Users
```bash
sudo useradd -m admin14
sudo useradd -m user14
Step 2: Set Passwords
sudo passwd admin14
sudo passwd user14
🔹 Step 3: Create an Admin-Only Folder
sudo mkdir -p /srv/admin_data
📌 Why /srv/admin_data?
/srv is used on real servers for service and administrative data
Common secure locations include:
/srv/admin_data
/srv/secure_backups
/srv/internal_reports
This follows real cloud server directory standards.
🔹 Step 4: Assign Ownership to admin14
sudo chown admin14:admin14 /srv/admin_data
✔ Owner → admin14
✔ Group → admin14 (primary group)
This ensures only the admin controls the folder.
Step 5: Apply Strict Permissions (700)
sudo chmod 700 /srv/admin_data
Step 6: Create a Confidential File
Login as admin:
su - admin14
Create a secret file:
touch /srv/admin_data/secret_report.txt
echo "Confidential: Admin14 Only" > /srv/admin_data/secret_report.txt
exit
Step 7: Test Forbidden Access (Critical Validation)
Login as normal user:
su - user14
🔹 Try listing the folder
ls /srv/admin_data
Expected:
ls: cannot open directory '/srv/admin_data': Permission denied
🔹 Try entering the folder
cd /srv/admin_data
Expected:
bash: cd: /srv/admin_data: Permission denied
🔹 Try reading the file
cat /srv/admin_data/secret_report.txt
 Expected:
cat: /srv/admin_data/secret_report.txt: Permission denied
🎉 If all actions fail, the workspace is perfectly secured.
Final Confirmation
echo "Completed – Admin-Only Access Control Implemented Successfully!" > success_workspace.txt && cat success_workspace.txt
