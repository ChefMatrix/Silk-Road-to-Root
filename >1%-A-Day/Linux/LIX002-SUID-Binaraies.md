---
ID: LIX002  
Date: 28/07/2025  
Tags: #linux #suid #privesc #filepermissions  
Category: Linux  
---

# LIX002 – SUID Binaries in Linux

## 🧠 What I Learned

**SUID (Set User ID)** is a special permission in Linux that allows a file to run **with the privileges of its owner**, not the user who executes it.

When a binary with the SUID bit set is owned by `root`, it will run as `root` — even if a regular user launches it.

This is extremely powerful — and dangerous if misconfigured.

---

## 🔍 How to Identify SUID Binaries

To find SUID binaries on a system:
```bash
find / -perm -4000 -type f 2>/dev/null
```
You’ll often see:

- /usr/bin/passwd  
- /bin/su  
- /usr/bin/sudo  

These are expected. But custom or uncommon binaries here could be a **privilege escalation vector**.

---

## 💣 Misuse Example

Let’s say you find this:

```bash
-rwsr-xr-x 1 root root 13432 Jun 2 10:33 /usr/local/bin/customscript
```
If this script runs something you can control (e.g., environment variables, `$PATH`, or an unescaped system call), you might gain root access.

```c
// Compile this as root-owned SUID
int main() {
  setuid(0);
  system("/bin/bash");
  return 0;
}
```
Running this binary as a regular user will drop you into a **root shell**.

---

## 🛡️ Mitigations

- Avoid SUID binaries unless absolutely necessary  
- Use `sudo` with fine-grained control instead  
- Regularly audit with:

```bash
find / -perm -4000 -type f
```
- Remove SUID from unknown or unused binaries:

```bash
chmod -s /path/to/binary
```
---

## 🔗 Resources

- [GTFOBins – SUID Exploits](https://gtfobins.github.io/)  
- [HackTricks – Linux SUID](https://book.hacktricks.xyz/linux-unix/privilege-escalation/sudo-and-suid)  
- [Linux chmod man page](https://man7.org/linux/man-pages/man1/chmod.1.html)  

---
