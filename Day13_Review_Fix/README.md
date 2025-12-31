# Day 13: Permissions Troubleshooting 🔧

## 🎯 Goal
Review Days 8-12 (Users, Groups, Permissions) and solve a broken permissions scenario.

## 🛠️ Challenge Scenario
**Task:** Fix a "Permission Denied" error on a critical application script.

**Steps Taken:**
1. Identified a script `deploy.sh` that failed to run.
2. Checked permissions using `ls -l` (Found: `-rw-r--r--`).
3. Fixed execution rights: `chmod +x deploy.sh`.
4. Fixed ownership: `chown appuser:appgroup deploy.sh`.
5. Verified the script ran successfully.

---
