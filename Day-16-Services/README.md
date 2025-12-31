# Day 16: Managing System Services 🚦

## 🎯 Goal
Understand `systemd` and `systemctl` to start, stop, and enable services—a core skill for Cloud Engineers.

## 🧩 Commands Learned
| Command | Purpose | Example |
| :--- | :--- | :--- |
| `systemctl status` | Check Status | `systemctl status ssh` |
| `systemctl start` | Start Service | `systemctl start nginx` |
| `systemctl stop` | Stop Service | `systemctl stop nginx` |
| `systemctl enable` | Auto-start | Enable on boot |

## 🛠️ Practice Session
I practiced managing the **SSH service**:
1. Checked status: `Active (running)`.
2. Stopped the service and verified connection failure.
3. Restarted the service to restore access.

---
