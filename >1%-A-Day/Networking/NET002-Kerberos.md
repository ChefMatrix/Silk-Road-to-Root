---
ID: NET002
Date: 01/07/2025
Tags: #Kerberos #Networking
Category: Networking
---
# NET002 – Kerberos
## 📘 Overview  
Kerberos is a **network authentication protocol** designed to provide **strong authentication for client/server applications** using **secret-key cryptography**.  
It was developed by MIT and is widely used in enterprise environments (especially Windows Active Directory).

---

## 🎯 Goal  
The main goal of Kerberos is to allow entities to **prove their identity over an untrusted network** (like the internet or internal corporate LAN) without transmitting passwords in plain text.

---

## 🔐 How it works (High-Level)  
Kerberos relies on **tickets** and a **trusted third-party (KDC)** to verify identity.

🧠 Think of it like:  
> “Here’s a signed hall pass (ticket) from the office (KDC), so I don’t need to keep asking for permission every time I enter a room (service).”

---

## 🧱 Key Components  

| Component       | Description |
|----------------|-------------|
| **Client**      | The user or machine requesting access |
| **KDC (Key Distribution Center)** | Trusted authority that handles authentication |
| **AS (Authentication Server)** | Part of KDC; verifies identity and issues TGT |
| **TGS (Ticket Granting Server)** | Part of KDC; issues service-specific tickets |
| **TGT (Ticket Granting Ticket)** | Used by client to request access to services |
| **Service Server** | The resource/server the client wants to access |

---

## 🔁 Authentication Flow  

1. **Client → AS**  
   Sends username → gets back encrypted TGT (Ticket Granting Ticket) if password is correct.

2. **Client decrypts TGT** using password-derived key  
   Stores this TGT (valid for a limited time).

3. **Client → TGS**  
   Uses TGT to request a Service Ticket for a specific resource (e.g., a file share).

4. **TGS → Client**  
   Sends encrypted Service Ticket.

5. **Client → Service Server**  
   Presents Service Ticket. If valid, access is granted.

---

## 💡 Why is this secure?

- Passwords are **never sent in plaintext**.
- Tickets are **time-limited**.
- Mitigates **replay attacks** using timestamps and session keys.
- KDC is a **trusted central authority**, making it scalable and secure in domains.

---

## ⚠️ Weaknesses / Attacks  

| Attack Name              | Description |
|--------------------------|-------------|
| **Pass-the-Ticket (PtT)** | Reuses valid Kerberos tickets |
| **Kerberoasting**        | Extracts service account tickets to crack offline |
| **AS-REP Roasting**      | Requests encrypted data for users not requiring pre-auth |

---

## 🧠 Notes for Blue & Red Teams  

- **Red Team:**  
  - Kerberoasting = dump TGS tickets and crack service account passwords.  
  - AS-REP Roasting = look for accounts with `Do not require Kerberos preauthentication`.

- **Blue Team:**  
  - Monitor for abnormal ticket requests, especially TGS requests with high frequency.  
  - Use strong passwords for service accounts (mitigates Kerberoasting).  
  - Limit lifetime of tickets, and enable AES encryption.

---

## 🧪 Lab Practice Ideas  

- Set up a Windows AD Lab and try:
  - Requesting a TGT with `kinit`
  - Dumping TGS tickets with `Rubeus`
  - Cracking TGS with `hashcat`

---

### References:
- https://www.fortinet.com/resources/cyberglossary/kerberos-authentication
- https://www.hackthebox.com/blog/what-is-kerberos-authentication
