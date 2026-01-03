# 🌍 REAL-WORLD CLOUD SCENARIO
## 🚨 “Suspicious Login Alert” – Authentication Incident Investigation

---

## 📌 Situation (Very Real)
Security monitoring raises an alert:

> “Multiple failed login attempts detected on server.
> **on-call** as a **Cloud Security Engineer**.
> Responsibility is to **verify the alert using logs**, determine if the
attack succeeded, and document the findings.

This is a **daily task for SOC, Cloud Security, and DevSecOps teams**.

---

## 🎯 Objective
- Confirm whether the alert is real or false
- Identify failed and successful login attempts
- Detect any privilege escalation
- Check SSH service health
- Monitor logs in real time
- Document findings for audits and escalation

---

## 🔎 Incident Response Flow (Production-Style)

---

### 1️⃣ Confirm Suspicious Activity (Failed Logins)
```bash
sudo grep -i "failed password" /var/log/auth.log
Interpretation
 No output → false alarm
 Output found → suspicious login attempts detected
 Failed logins often indicate:
Brute-force attacks
Credential stuffing
Bot activity
2️⃣ Check for Successful Logins
sudo grep -i "accepted password" /var/log/auth.log
3️⃣ Check for Privilege Escalation
sudo grep -i "sudo" /var/log/auth.log
4️⃣ Inspect SSH Service Health
sudo journalctl -u ssh
5️⃣ Monitor Logs Live (Active Incident)
sudo journalctl -f
6️⃣ Write an Incident Note (Professional Habit)
echo "Incident checked: Authentication logs reviewed, no unauthorized root access detected" > incident_summary_day24.txt
cat incident_summary_day24.txt
