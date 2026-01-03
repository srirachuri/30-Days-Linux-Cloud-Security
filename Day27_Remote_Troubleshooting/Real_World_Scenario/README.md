# 🌍 Real-World Scenario (Cloud Security / Linux)
## Production Server Access Issue via SSH

---

## 📞 Situation (What You’re Told)
> “Users can’t access the application.  
> The server is online, but the app isn’t responding.  
> Please log in and fix it ASAP.”

You are the **Junior Cloud / Linux / Security Engineer on duty**.

This is a **very real production incident** in AWS, Azure, and GCP.

---

## 🎯 Your Mission
You must:
- SSH into the remote server
- Check logs to identify errors
- Diagnose a service failure
- Fix a permission issue
- Restore the service safely
- Verify application recovery

---

##  STEP 1 — Connect to the Server (SSH)
```bash
ssh ec2-user@<server-ip>
Training simulation:
ssh localhost
 SSH fails → server unreachable
 SSH works → proceed with troubleshooting
STEP 2 — Check Logs (Find the Clue)
System logs
sudo journalctl -xe
Application / system logs
sudo tail -f /var/log/syslog
🔍 Observation:
permission denied: /var/log/app/app.log
service failed to start
 Suspected root cause:
Incorrect permissions on application log files causing service failure.
 STEP 3 — Create a Fake Application Script (Simulation)
Create application directory:
sudo mkdir /opt/myapp
sudo nano /opt/myapp/app.sh
Inside nano:
#!/bin/bash
while true
do
  echo "$(date) - My App is running" >> /var/log/app/app.log
  sleep 5
done
Save and exit:
Ctrl + O → Enter
Ctrl + X
Make executable:
sudo chmod +x /opt/myapp/app.sh
 STEP 4 — Prepare Log Directory (Important)
sudo mkdir -p /var/log/app
sudo touch /var/log/app/app.log
sudo chmod 644 /var/log/app/app.log
 Prevents permission denied crashes.
STEP 5 — Create a systemd Service File
sudo nano /etc/systemd/system/app.service
inside nano
[Unit]
Description=My Custom App Service
After=network.target

[Service]
ExecStart=/opt/myapp/app.sh
Restart=always
User=root

[Install]
WantedBy=multi-user.target
Save and exit.
 STEP 6 — Reload systemd (CRITICAL)
sudo systemctl daemon-reload
 Tells Linux that a new service exists.
 STEP 7 — Start the Application Service
sudo systemctl start app.service
sudo systemctl status app.service
Expected:
Active: active (running)
 Service created successfully.
 STEP 8 — Verify Application Logs
tail -f /var/log/app/app.log
Expected output:
Tue Dec 26 16:25:01 IST - My App is running
Press Ctrl + C to exit.
 STEP 9 — Simulate the Real Failure (Permission Issue)
Break permissions:
sudo chmod 000 /var/log/app/app.log
Test:
cat /var/log/app/app.log
 Output:
Permission denied
This simulates the real production issue.
 STEP 10 — Restart Service (Fails Again)
sudo systemctl restart app.service
sudo systemctl status app.service
 Result:
Active: failed (permission denied)
 STEP 11 — Investigate Permissions
ls -l /var/log/app/app.log
Example:
---------- 1 root root app.log
 App cannot write logs → service crashes.
 STEP 12 — Fix Permissions (Real Fix)
sudo chmod 644 /var/log/app/app.log
sudo chown root:root /var/log/app/app.log
(Optional advanced fix if app runs as another user):
sudo chown appuser:appuser /var/log/app/app.log
 STEP 13 — Restart Service After Fix
sudo systemctl restart app.service
sudo systemctl status app.service
 Result:
Active: active (running)
 Service restored.
 STEP 14 — Final Verification
curl localhost
