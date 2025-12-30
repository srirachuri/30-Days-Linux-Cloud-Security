# Day 04 – File Editing (nano & vim)

## 🎯 Goal
Learn how to open, edit, save, and exit files using Linux text editors.

---

## 🛠 Commands Practiced

- `nano filename` → Beginner-friendly text editor
- `vim filename` → Powerful editor used by system administrators
- `cat filename` → Verify file content after editing

---

## 🧠 Editing Basics

| Editor | Edit Mode | Save | Exit |
|------|----------|------|------|
| nano | Just type | Ctrl + O | Ctrl + X |
| vim  | Press `i` | :w | :q |
| vim (save & exit) | `i` → edit | :wq | Enter |
| vim (force exit) | — | — | :q! |

---

## 🧪 Step-by-Step Practice

### 1️⃣ Create workspace
```bash
mkdir day4_editing
cd day4_editing
nano notes.txt
This is my first nano edit.
Learning Linux Day 4.
cat notes.txt
vim notes2.txt
cat notes2.txt
nano notes.txt
Editing this file again!
mkdir project4
cd project4
nano summary.txt
vim commands.txt
ls
echo "I completed Linux Day 4" > success_day4.txt && cat success_day4.txt
