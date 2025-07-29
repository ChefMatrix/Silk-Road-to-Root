---
ID: RECON003  
Date: 30/07/2025 
Tags: #nmap #recon #stealth #timing #tcp  
Category: Recon Tools  
---

# REC003 – Nmap Timing & Stealth Scan Options

## 🧠 What I Learned

Nmap isn’t just about scanning — it’s about **how you scan**. By adjusting **timing** and **stealth flags**, you can:
- Evade firewalls or intrusion detection systems (IDS)
- Speed up or slow down scans depending on your engagement
- Avoid detection during red team or CTF ops

---

## 🎛️ Nmap Timing Templates

```bash
nmap -T0 target.com  
nmap -T4 target.com  
nmap -T5 target.com
```
**Timing Values:**
- `T0` = Paranoid (very slow, good for stealth)  
- `T1` = Sneaky  
- `T3` = Normal  
- `T4` = Aggressive (default for local scans)  
- `T5` = Insane (use cautiously — can cause detection)
  
---

## 🕵️‍♂️ Stealth Scanning Techniques

```bASH
nmap -sS target.com  
nmap -sN target.com  
nmap -sF target.com  
nmap -sX target.com
```
**Scan Types:**
- `-sS` = SYN scan (default, semi-stealthy)  
- `-sN` = NULL scan (no TCP flags)  
- `-sF` = FIN scan (sends only FIN flag)  
- `-sX` = Xmas scan (sets FIN, URG, and PUSH flags)

These scans can bypass poorly configured firewalls or logging tools.

---

## 🔐 When to Use Stealth Scans

- Red Team: To avoid alerting SOC or IPS  
- Internal Pentests: Test segmentation between VLANs  
- CTF/HTB: When full-connect scans are blocked or slow

---

## 🛡️ Defender Tip

To catch stealth scans, use:
- IDS/IPS tools like **Snort** or **Suricata**
- Behavior-based detection: watch for half-open or malformed TCP packets
- Nmap detection signatures in Wazuh or ELK stack

---

## 🔗 Resources

- [Nmap Book – Timing and Performance](https://nmap.org/book/performance.html)  
- [HackTricks – Nmap](https://book.hacktricks.xyz/network-services-pentesting/nmap)  
- [Linux Man Page – Nmap](https://man7.org/linux/man-pages/man1/nmap.1.html)

---
