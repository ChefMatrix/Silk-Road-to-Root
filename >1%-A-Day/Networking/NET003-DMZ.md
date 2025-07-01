---
ID: NET003
Date: 02/07/2025
Category: Networking
---

# DMZ (Demilitarized Zone) 🌐🧱  
> Public-facing buffer zone between untrusted and internal networks

---

## 📘 Overview  
A **DMZ (Demilitarized Zone)** is a network segment that acts as a **buffer zone** between an untrusted network (e.g., the internet) and an internal, trusted network (e.g., company LAN).

It’s used to host **public-facing services** such as:
- Web servers
- Mail servers
- DNS servers
- Reverse proxies
- VPN concentrators

---

## 🧠 Analogy  
> Think of the DMZ as a reception area in a secure building — visitors are allowed here, but not beyond without checks.

---

## 🧱 Basic Architecture  

```plaintext
[Internet]
     |
[Firewall 1]
     |
   [DMZ]
     |
[Firewall 2]
     |
[Internal LAN]
```

- Firewall 1 (External Firewall): Controls access from the internet to the DMZ
- Firewall 2 (Internal Firewall): Controls access from the DMZ to the internal network
- Servers in the DMZ should never initiate connections to internal hosts unless explicitly required

## 🎯 Why Use a DMZ?

| Benefit                | Explanation |
|------------------------|-------------|
| **Improved Security**  | Isolates public services from internal systems |
| **Risk Containment**   | Breach of a DMZ host doesn’t expose entire LAN |
| **Controlled Access**  | Tight control on what enters and exits each network zone |

---

## 🧪 Real-World Services in DMZ  

| Service        | Why It Goes in DMZ |
|----------------|--------------------|
| **Web Server** | Needs internet access for HTTP(S) |
| **Mail Server**| Receives emails from outside |
| **DNS Server** | Resolves public domain names |
| **VPN Gateway**| Users connect from internet to internal LAN |
| **Jump Box / Bastion Host** | Secure gateway to access internal systems remotely |

---

## 🔥 Red Team POV (Offensive)  

- **Target of Recon & Exploits**  
  These services are **exposed to the internet**, making them juicy attack surfaces.

- **Pivoting Point**  
  If compromised, attackers may attempt to **pivot** into the internal LAN.

- **Look for Misconfigurations**  
  Improperly secured SSH, RDP, or exposed admin panels are common weaknesses.

---

## 🛡️ Blue Team POV (Defensive)  

- **Harden All DMZ Hosts**  
  Minimize running services and patch aggressively.

- **Log & Monitor**  
  Set up **IDS/IPS and centralized logging** for all DMZ traffic.

- **Segment Properly**  
  Use **strict firewall rules** between DMZ, internet, and internal LAN.

- **Apply Principle of Least Privilege**  
  Services should only access what they need — nothing more.

---

## ⚠️ Common Mistakes  

| Mistake                            | Risk |
|------------------------------------|------|
| DMZ host has open access to LAN    | Enables lateral movement post-compromise |
| Internal DNS used in DMZ           | Leaks internal names & zones |
| Services share auth with internal  | Credential compromise extends to LAN |
| No monitoring/logging              | Blind to attacks and breaches |

---

## 🧪 Lab Simulation Ideas  

- Simulate a DMZ in a **home lab** using:
  - **pfSense or OPNsense** as your firewall
  - Place **Apache/NGINX** on a separate subnet labeled as "DMZ"
  - Configure firewall rules:
    - Allow internet → DMZ (HTTP/S)
    - Allow LAN → DMZ (admin access)
    - Deny DMZ → LAN by default

---

## 📌 Summary  

A **DMZ** is a critical part of secure network architecture.  
> It isolates externally accessible systems while protecting internal assets.

You should always assume that **DMZ services are under constant threat**, and design them with **isolation, logging, and minimal trust**.

---

## References  

- [Cisco: Demilitarized Zone (DMZ) Design Guide](https://www.cisco.com/c/en/us/support/docs/security-vpn/ipsec-negotiation-ike-protocols/70963-dmz.html)  
- [OWASP: Network Segmentation](https://owasp.org/www-community/controls/Network_Segmentation)  
- [Red Hat: What is a DMZ?](https://www.redhat.com/en/topics/security/what-is-a-dmz)  
- [NIST SP 800-41 Rev.1 - Guidelines on Firewalls and Firewall Policy](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-41r1.pdf)  

---
