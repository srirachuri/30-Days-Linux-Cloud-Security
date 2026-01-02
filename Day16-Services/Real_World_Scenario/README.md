# 🌍 Real-World Cloud Scenario
## Website Down – Nginx Service Investigation

---

## 📌 Situation
A production **website is down**, and **Nginx is suspected**.

### What is Nginx?
- Nginx is a **web server**
- It **serves website content** to users
- Think of it as:
  - 🚪 Door (entry point)
  - 🛡️ Security guard (controls access)
  - 🧑‍💼 Receptionist (routes requests)

If Nginx is down → the website is unreachable.

This is a **common real-world incident** in **AWS, Azure, and GCP**.

---

## 🎯 Objective
- Check whether the Nginx service is running
- Restart or reload it safely
- Ensure it starts automatically on reboot
- Inspect logs for errors
- Follow cloud security best practices

---

## 🧩 Incident Handling – Step by Step

---

### 🔹 Step 1: Check Nginx Service Status
```bash
sudo systemctl status nginx
🔹 Step 2: Restart the Service
sudo systemctl restart nginx
Used when the service is unresponsive or crashed.
🔹 Step 3: Reload If Restart Fails
sudo systemctl reload nginx
💡 Reload:
Re-reads configuration
Does NOT fully stop the service
Safer in production when possible
🔹 Step 4: Enable Auto-Start on Boot
sudo systemctl enable nginx
✅ Ensures Nginx starts automatically after:
Server reboot
Power failure
Cloud maintenance
🔹 Step 5: Check Logs for Errors
sudo journalctl -u nginx -xe
🔍 Option Breakdown
-u nginx → logs only for the nginx service
-x → adds helpful explanations
-e → jumps to the latest logs
 This is mandatory before restarting blindly.
Step 6: Success Confirmation
echo "Completed – Website is down, nginx suspected successfully!" > success_suspected.txt
cat success_suspected.txt
