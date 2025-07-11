---
ID: LIX001
Date: 11/07/2025
Tags: #linux #permissions #privilegeescalation
Category: Linux
---

# LIX001 – File Permissions in Linux

## 🧠 What I Learned

Linux uses a permission system to control **who can read, write, or execute files**. These permissions are crucial for maintaining security and controlling access to sensitive information or system-level files.

Permissions are represented using either **symbolic notation** (e.g., `-rw-r--r--`) or **octal notation** (e.g., `644`).

---

## 🔐 Breakdown of Permissions

Each file has:
- **Owner**
- **Group**
- **Others**

And three permissions:
- `r` – read
- `w` – write
- `x` – execute

Example:  
```bash
-rwxr-xr-- 1 root root 1337 Jun 30 01:00 example.sh
