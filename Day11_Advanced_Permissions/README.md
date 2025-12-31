# Day 11: Advanced Permissions (Sticky Bit & Umask) 🛡️

## 🎯 Goal
Understand special permissions like **Sticky Bit** (for shared folders) and **Umask** (default file permissions).

## 🧩 Commands Learned
| Command | Purpose | Example |
| :--- | :--- | :--- |
| `chmod +t` | Set Sticky Bit | `chmod +t /shared` |
| `umask` | Check Default Perms | `umask` |
| `umask 022` | Set Default Perms | `umask 002` |
| `ls -ld` | View Dir Perms | `ls -ld /tmp` |

## 🛠️ Practice Session
I explored how the `/tmp` directory uses the **Sticky Bit** to allow everyone to write files but prevents users from deleting others' files.

## 🏆 Mini Project 11: The Shared Team Folder
**Scenario:** Creating a collaboration folder where team members can add files, but cannot delete each other's work.

**Steps Taken:**
1. Created directory `team_share`.
2. Assigned group ownership to `devops`.
3. Applied the **Sticky Bit**: `chmod +t team_share`.
4. Verified that User A could not delete User B's file.
---
