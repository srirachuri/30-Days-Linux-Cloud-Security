# 🌍 Cloud Security Real-World Scenario  
## Security Team Setup & Account Control

A **Cloud Security Trainee** setting up access control on a Linux server.
As part of IAM (Identity and Access Management), you must create a security team,
assign users, and control account access safely.

This simulates **real-world user and group management** in cloud environments.

---

## 🎯 Objectives
- Create a dedicated security group
- Create analyst and auditor user accounts
- Assign users to the security group
- Verify group membership
- Lock and unlock user access when required

---

## 🧩 Step-by-Step Implementation

### 🔹 1. Create a Group Called `security`
```bash
sudo groupadd security
🔹 2. Create Two Users: analyst and auditor
sudo useradd -m -s /bin/bash analyst
sudo useradd -m -s /bin/bash auditor
✅ Explanation:
-m → creates home directories (/home/analyst, /home/auditor)
-s /bin/bash → assigns Bash as the default shell
🔹 3. Add Both Users to the security Group
sudo usermod -aG security analyst
sudo usermod -aG security auditor
✅ Purpose:
Adds users to the group without removing existing group memberships.
🔹 4. Verify Group Membership
grep security /etc/group
✅ Expected Output Example:
security:x:1003:analyst,auditor
If both usernames appear, the configuration is correct.
🔹 5. Lock the auditor Account (Disable Access)
sudo usermod -L auditor
✅ Purpose:
Temporarily disables login access.
Used when an account is compromised, inactive, or under review.
🔹 6. Unlock the Account Later (Re-enable Access)
sudo usermod -U auditor
✅ Purpose:
Restores login access once the issue is resolved.
🔹 7. Final Confirmation Message
echo "Security team setup and account control completed successfully 🛡️"
✅ Output:
Security team setup and account control completed successfully 🛡️
