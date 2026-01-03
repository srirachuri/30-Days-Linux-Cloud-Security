# 🌍 Real-World Scenario (Cloud Security Edition)
## Secure Access to a Production Server (SSH Key-Based Authentication)

---

## 📌 Situation
A **Cloud / Security Engineer**.

Your team states:
> “We’ve launched a Linux server.  
> Password logins are NOT allowed.  
> Only SSH key-based access is permitted.”

This is **standard security policy** in:
- AWS
- Azure
- GCP
- All production Linux servers

---

## 🔐 What Problem This Solves

### ❌ Password-based logins
- Can be brute-forced
- Can be leaked
- Often reused across systems

### ✅ SSH key-based access
- Cannot be guessed
- Uses cryptography
- Uniquely identifies the user

👉 **Security + Accountability**

---

## 🎯 Objective
- Generate SSH keys
- Configure passwordless login
- Disable password authentication completely
- Verify secure access

This is mandatory in:
- SOC environments
- Production servers
- Compliance audits (ISO, SOC2)

---

## 🧠 How This Maps to the Real World
Localhost is used **only for practice**.  
The same steps apply to **AWS EC2, Azure VMs, and GCP Compute**.

---

## 🧩 Step-by-Step Implementation

---

### 🔹 Step 1: Connect to the Server (Practice on Localhost)
```bash
ssh localhost
Cloud example:
ssh username@server_ip
📌 Meaning:
“I am securely connecting to a remote Linux server.”
🔹 Step 2: Generate SSH Keys (Your Digital Identity)
ssh-keygen
Press Enter for all prompts.
This creates:
🔐 Private key → ~/.ssh/id_rsa (never share)
🔓 Public key → ~/.ssh/id_rsa.pub (safe to share)
Verify:
ls ~/.ssh
🔹 Step 3: Grant Access Using Public Key
Practice (localhost):
ssh-copy-id localhost
What this does:
Copies your public key
Adds it to:
~/.ssh/authorized_keys
📌 Cloud equivalent:
AWS automatically places your public key into authorized_keys
Meaning:
“This user is officially allowed to access this server.”
🔹 Step 4: Verify Passwordless Login
ssh localhost
✅ Expected:
No password prompt
Authentication succeeds using cryptographic proof
This is mandatory for production servers.
🔥 Step 5: Disable Password Authentication (CRITICAL)
🔹 Open SSH configuration
sudo nano /etc/ssh/sshd_config
🔹 Update / confirm these settings
PasswordAuthentication no
PubkeyAuthentication yes
If PasswordAuthentication yes exists → change it to no.
🔹 Save and exit
CTRL + O → Enter
CTRL + X
🔹 Restart SSH service
sudo systemctl restart ssh
🔹 Step 6: Verify Server Security
Check SSH service:
sudo systemctl status ssh
Test login again:
ssh localhost
Final Success Proof
echo "Completed SSH access configured and verified successfully" > success_ssh.txt
cat success_ssh.txt
