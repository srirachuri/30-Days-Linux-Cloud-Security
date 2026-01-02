# 🌍 REAL-WORLD CLOUD SCENARIO
## 🚨 “Website Not Opening” – DNS & Network Investigation

---

## 📌 Situation
A client reports:
> “Our website is not loading for users.”

A **on-call** as a **Cloud / Security Engineer**.
Your responsibility is to determine whether the issue is caused by:
- DNS resolution
- Network routing
- Exposed or blocked web ports

This is a **very common real-world incident** in AWS, Azure, and GCP.

---

## 🎯 Objective
- Verify DNS resolution
- Inspect DNS record types
- Check network path reachability
- Verify web ports exposure
- Document findings clearly for escalation or audit

---

## 🔎 Incident Troubleshooting Flow (Production-Style)

---

### 1️⃣ Is DNS Resolving?
```bash
dig website.com
Check Specific DNS Record Types
dig google.com A  +short > dns_a.txt
dig google.com MX +short > dns_mx.txt
dig google.com NS +short > dns_ns.txt
A record → maps domain to IP address
MX record → mail routing
NS record → authoritative name servers
Saving output provides evidence for incident reports.
2️⃣ Is the Network Path Reachable?
traceroute website.com
3️⃣ Are Web Ports Open?
nmap website.com
What you are checking
Port 80 → HTTP
Port 443 → HTTPS
4️⃣ Incident Note 
echo "DNS resolved, network path reachable, web ports open — issue not network-related" > incident_day23.txt
cat incident_day23.txt
