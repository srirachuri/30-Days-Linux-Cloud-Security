# 🌍 Real-World Scenario (Cloud Security Edition)
## Secure Shared Folder on a Cloud Server

---

## 🔐 Situation
You are a **Cloud Security Trainee** managing a Linux server where three users
collaborate on logs and reports:

- analyst  
- auditor  
- developer  

They all must work inside **one shared folder**, but with strict security rules:

❌ Users must NOT delete each other’s files  
✔️ All users can create new files  
✔️ The administrator controls the folder  

This mirrors how real systems protect:
- `/tmp`
- `/var/tmp`
- `/srv/shared`

---

## 🎯 Objective
Create a shared folder `team_logs` such that:

- Everyone in the team can write files
- Users cannot delete files created by others
- File ownership remains with the creator
- Admin retains full control

This requires:
- `chmod`
- `chgrp`
- **Sticky Bit (`+t`)**

---

## 🧩 Step-by-Step Implementation

### 🔹 Step 1: Create a Group for the Team
```bash
sudo groupadd teamsec
Step 2: Add Users to the Group
sudo usermod -aG teamsec analyst
sudo usermod -aG teamsec auditor
sudo usermod -aG teamsec developer
Verify:
grep teamsec /etc/group
Step 3: Create the Shared Folder
sudo mkdir -p /srv/team_logs
📌 Why /srv?
Used for service and shared application data on real servers
Common paths:
/srv/projects
/srv/reports
/srv/shared
-p ensures parent directories are created if they do not exist.
🔹 Step 4: Change Group Ownership
sudo chgrp teamsec /srv/team_logs
Now the folder belongs to the security team.
🔹 Step 5: Grant Write Access to the Group
sudo chmod 770 /srv/team_logs
Meaning:
Owner → rwx
Group → rwx
Others → ---
🔹 Step 6: Enable the Sticky Bit (MOST IMPORTANT)
sudo chmod +t /srv/team_logs
🔐 Sticky Bit = Anti-Delete Protection
Verify:
ls -ld /srv/team_logs
Expected:
drwxrwxrwt 2 root teamsec ...
The final t confirms the sticky bit is enabled.
Test the Setup
Login as analyst:
su - analyst
touch /srv/team_logs/a_file.txt
exit
Login as auditor:
su - auditor
rm /srv/team_logs/a_file.txt
exit
Expected Output:
rm: cannot remove 'a_file.txt': Operation not permitted
Sticky bit protection is working correctly.
Final Confirmation
echo "Day 11 Cloud Security Scenario Completed Successfully! 🛡️" > success_scenario_day11.txt
cat success_scenario_day11.txt
