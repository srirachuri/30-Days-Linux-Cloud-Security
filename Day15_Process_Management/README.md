#### 📝 Day 15: Process Management
**File Path:** `Day-15-Process-Management/README.md`

```markdown
# Day 15: Linux Processes ⚙️

## 🎯 Goal
Understand how to view, monitor, and kill system processes.

### 🧩 Commands Learned
| Command | Purpose | Example |
| :--- | :--- | :--- |
| `ps aux` | List Processes | `ps aux \| grep python` |
| `top` / `htop` | Real-time Monitor | `htop` |
| `kill` | Stop Process (PID) | `kill 1234` |
| `killall` | Stop Process (Name)| `killall firefox` |
| `bg` / `fg` | Background/Foreground | `Ctrl+Z` then `bg` |

## 🛠️ Practice Session
I started a long-running process (`sleep 1000`), sent it to the background using `&`, and then killed it using its PID.


## 🏆 Mini Project 15: The "Unresponsive App" Simulation
**Scenario:** Finding a resource-heavy process and terminating it safely.

**Steps Taken:**
1. Simulated a high-load process.
2. Used `top` to identify the Process ID (PID).
3. Used `kill -9 <PID>` to force stop the process.
4. Verified system resources returned to normal.

---
