---
ID: NET004
Date: 08/07/2025
Tags: #arp #spoofing #mitm #networking
Category: Networking
---

# NET004 – ARP Spoofing

## 🧠 What I Learned

**ARP spoofing** (a.k.a. ARP poisoning) is a **Man-in-the-Middle (MITM)** attack where an attacker sends falsified ARP (Address Resolution Protocol) messages on a local network.

The goal is to **associate the attacker's MAC address** with the IP address of another device (e.g., the default gateway), allowing them to intercept, modify, or block traffic.

---

## 🔧 How ARP Works

- Devices on LAN use ARP to map IP addresses to MAC addresses.
- When a device wants to talk to another, it broadcasts:
  
  `Who has 192.168.1.1? Tell 192.168.1.50`
 
- The legitimate device replies:

  `192.168.1.1 is at AA:BB:CC:DD:EE:FF`

---

## 💀 ARP Spoofing in Action

Attacker injects forged ARP replies like:

`192.168.1.1 is at 11:22:33:44:55:66 ← (attacker's MAC)`

Now the victim sends traffic to the attacker, thinking they’re talking to the gateway.

---

## 🛡️ Mitigation

- Use **static ARP entries** where possible (on critical systems)
- Use **switch port security** (e.g., Cisco sticky MAC)
- Use **packet inspection tools** like Suricata or Zeek
- Implement **Dynamic ARP Inspection (DAI)** if supported by network hardware

---

## 🔗 Resources

- [Bettercap ARP Spoofing Guide](https://www.bettercap.org/)
- [ARP Poisoning – HackTricks](https://book.hacktricks.xyz/network-services-pentesting/arp-poisoning)
- [Wireshark Filtering ARP](https://wiki.wireshark.org/ARP)

---

## ✅ Key Takeaway

> ARP spoofing is simple, powerful, and often overlooked. It’s one of the easiest ways to MITM LAN traffic — if your network isn’t hardened, **you’re exposed.**
