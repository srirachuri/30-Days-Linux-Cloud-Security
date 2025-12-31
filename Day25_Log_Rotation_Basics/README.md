# 📅 Day 25 — Log Rotation Basics (Linux)

## 📌 Project Overview
This project focuses on **log rotation**, a critical Linux mechanism that prevents disks from filling up due to continuously growing log files.

In real servers and cloud environments, improper log rotation can lead to:
- Disk full errors
- Service crashes
- Missed security logs
- Failed updates and deployments

Linux uses **logrotate** to automatically manage logs safely and efficiently.

---

## 🎯 Learning Objectives
By the end of Day 25, I am able to:
- Understand why log rotation is essential
- Explain how Linux manages logs automatically
- Read and interpret `logrotate` configuration files
- Audit security-critical log rotation rules
- Safely test log rotation using dry-run mode
- Explain log rotation clearly in interviews

---

## 🧠 What is Log Rotation?
Logs grow continuously due to:
- Login attempts
- `sudo` usage
- Errors and warnings
- Application activity

If logs are never controlled:
❌ Disk fills up  
❌ Server becomes unstable  
❌ Services crash  

**Log rotation means:**
- Old logs are renamed
- Older logs are compressed
- Very old logs are deleted
- A new empty log file is created automatically

---

## 🔧 Tool Used — `logrotate`
Linux uses **logrotate** to manage logs automatically using configuration files.

---
