# Day 12: Sudoers & Privilege Delegation 👑

## 🎯 Goal
Learn how to grant administrative privileges to specific users safely using the `sudo` command and `/etc/sudoers` file.

## 🧩 Commands Learned
| Command | Purpose | Example |
| :--- | :--- | :--- |
| `visudo` | Edit Sudo Config | `sudo visudo` |
| `su` | Switch User | `su - user` |
| `sudo -l` | List Privileges | `sudo -l` |

## 🛠️ Practice Session
I practiced adding a user to the `sudo` group and verifying their ability to run root commands.

## 🏆 Mini Project 12: Restricted Sudo Access
**Scenario:** Granting a junior developer permission to restart a web server *without* giving them full root access.

**Steps Taken:**
1. Created user `junior_dev`.
2. Edited sudoers using `visudo`.
3. Added rule: `junior_dev ALL=(ALL) /bin/systemctl restart apache2`.
4. Verified that `junior_dev` could restart the service but not read `/etc/shadow`.

---
