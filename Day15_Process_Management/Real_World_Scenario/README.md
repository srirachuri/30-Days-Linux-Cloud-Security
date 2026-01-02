# 🚨 REAL-WORLD SCENARIO (Cloud Security Incident)
## Detect & Stop a Suspicious High-CPU Process on a Cloud Server

---

## 📌 Situation
A **Cloud Security Engineer** monitoring an **Ubuntu server on AWS**.

Users report:
> “The server is very slow. Pages are loading slowly. CPU usage is at 100%.”

This is a **very common real-world cloud incident**.

Your responsibilities:
- Investigate system health
- Identify suspicious processes
- Safely terminate malicious activity
- Collect evidence
- Verify server recovery

This workflow reflects **daily tasks of cloud security and SOC teams**.

---

## 🎯 Objectives
✔ Detect abnormal CPU usage  
✔ Identify the malicious process  
✔ Safely kill the process  
✔ Collect forensic evidence  
✔ Check logs for intrusion signs  
✔ Restore server health  

---

## 🧩 Incident Response – Step by Step

---

### 🔹 STEP 1: Check System Health (Live Monitoring)
```bash
top
Observe:
CPU usage
Load average
Top CPU-consuming process
Example:
%CPU   COMMAND
98.7   crypto_miner.sh
 Red Flags
CPU near 100%
Suspicious script name
Unexpected workload
Exit top:
q
🔹 STEP 2: List Processes by CPU Usage
ps aux --sort=-%cpu | head
Why this works
ps aux → list all processes
--sort=-%cpu → highest CPU first
head → show only top 10
Example Output
ubuntu   2334  98.7  12.0  /tmp/crypto_miner.sh
Suspicious Indicators
Extremely high CPU
Running from /tmp
Malicious-looking filename
🔹 STEP 3: Inspect the Process in Detail
ps -fp 2334
Command Breakdown
ps → process status
-f → full detailed format
-p 2334 → inspect only PID 2334
This shows:
User who started it
Parent process
Start time
Full command path
Inspect the file:
ls -l /tmp/crypto_miner.sh
cat /tmp/crypto_miner.sh
If it contains unknown commands, URLs, or mining logic → confirmed malicious.
🔹 STEP 4: Kill the Malicious Process
Try a graceful stop first:
kill 2334
If it persists, force kill:
kill -9 2334
Confirm removal:
ps aux | grep crypto
🔹 STEP 5: Check Logs for Evidence
sudo journalctl -xe
sudo tail -n 50 /var/log/auth.log
Why logs matter
Failed login attempts
Unknown users
Suspicious IP addresses
Service failures
tail -n 50 = show most recent 50 entries, which is where attacks appear first.
🔹 STEP 6: Search for Other Mining Processes
ps aux | grep -E "miner|crypto|xmrig"
Explanation
-E → extended regex
Searches multiple miner names at once
 xmrig
A well-known crypto-mining malware
If found → server compromise confirmed
🔹 STEP 7: Capture Evidence (Forensics)
Security teams never clean before collecting evidence.
ps aux > /tmp/evidence_process.txt
sudo journalctl -xe > /tmp/evidence_logs.txt
sudo cp /tmp/crypto_miner.sh /tmp/evidence_miner_script.txt
🔹 STEP 8: Remove the Malicious File
sudo rm -f /tmp/crypto_miner.sh
🔹 STEP 9: Check Who Created the File
ls -l /tmp/crypto_miner.sh
STEP 10: Verify Server Health After Fix
top
