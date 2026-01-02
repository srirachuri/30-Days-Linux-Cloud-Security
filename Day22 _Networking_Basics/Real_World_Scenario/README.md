# 🌍 REAL-WORLD CLOUD SCENARIO
## 🚨 “Website Not Loading” – On-Call Incident Troubleshooting

---

## 📌 Situation
A user reports:
> “The website is not opening.”

You are **on-call** as a **Cloud / Security Engineer** and must quickly
determine whether the issue is related to:
- Network connectivity
- Internet access
- Firewall rules
- Web service ports

This is a **very common real-world incident** in AWS, Azure, and GCP.

---

## 🎯 Objective
- Verify server network health
- Confirm outbound internet access
- Check whether web ports are listening
- Identify firewall-related issues
- Document findings clearly

---

## 🔎 Incident Troubleshooting Flow (Production-Style)

---

### 1️⃣ Is the Server Online?
```bash
ping -c 3 google.com
Can the Server Reach Websites?
curl -I https://google.com
Enable Firewall (UFW)
sudo ufw enable
Check firewall status:
sudo ufw status
3️⃣ Is the Web Port Listening?
ss -tuln | grep -E '80|443'
Command Explanation
ss → socket statistics
-tuln → show TCP/UDP listening ports
grep -E → extended regex
'80|443' → match HTTP (80) OR HTTPS (443)
Interpretation
 No output → Web server not running or not listening
 Output present → Web ports are open
4️⃣ Is the Firewall Blocking Traffic?
sudo ufw status
Disable Firewall (Testing Only)
sudo ufw disable
Incident Note 
echo "Checked network, ports, firewall — no network issue found" > incident_day22.txt
cat incident_day22.txt
