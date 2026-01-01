# Day 04 – File Editing (Cloud Security Edition)

## 🌍 Real-World Scenario: Securing SSH Access

### ☁️ Situation
You are a Cloud Security trainee managing a Linux server.
To improve SSH security and reduce attack surface, you must safely inspect
and modify SSH configuration settings without risking server lockout.

This simulates **real-world server hardening** tasks performed by
Linux and Cloud Security Engineers.

---

## 🎯 Objectives
- Safely inspect critical configuration files
- Create backups before editing system files
- Edit SSH configuration using secure practices
- Validate configuration changes before applying
- Understand how file editing impacts server security

---

## 🧩 Step-by-Step Simulation

### 🔹 Step 1: Create a Backup of SSH Configuration
```bash
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup
sudo cp /etc/ssh/sshd_config.backup /etc/ssh/sshd_config
Step 2: Open SSH Config Safely (Read-Only)
sudo less /etc/ssh/sshd_config
Observe key security-related lines:
#Port 22
#PermitRootLogin prohibit-password
#PasswordAuthentication yes
#MaxAuthTries 6
Step 3: Create a Test Copy for Safe Editing
sudo cp /etc/ssh/sshd_config /home/$USER/sshd_config_test
Step 4: Edit the Test Configuration File
sudo nano /home/$USER/sshd_config_test
Modify (uncomment if required):
Port 2222
PermitRootLogin no
PasswordAuthentication no
MaxAuthTries 3
Step 5: Save the File
Ctrl + O → Enter → Ctrl + X
Step 6: Verify Changes
sudo diff /etc/ssh/sshd_config /home/$USER/sshd_config_test
Step 7: Test Configuration Syntax Safely
sudo sshd -t -f /home/$USER/sshd_config_test
Step 8: Apply Changes (After Testing)
Ensure another terminal session is open before restarting SSH.
sudo cp /home/$USER/sshd_config_test /etc/ssh/sshd_config
sudo systemctl restart sshd
Step 9: Confirm Completion
echo "SSH configuration test completed successfully. Safe to apply changes!" > success_ssh_configuration.txt && cat success_ssh_configuration.txt
