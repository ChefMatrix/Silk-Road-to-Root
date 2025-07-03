# 📘 Section 5 – Layer 4, Transport Layer (Summary)

---

## 🎯 Overview: Transport Layer Responsibilities

The **Transport Layer** (Layer 4 of the OSI model) is responsible for the **transparent transfer of data** between hosts. Its main duties include:

- **End-to-end error recovery**
- **Flow control**
- **Session multiplexing**
- **Reliable communication**

---

## 🔄 Flow Control

Flow control is the process of **adjusting the flow of data from the sender** to ensure the receiving host can process it.

> 📌 Example: If a sender transmits more data than the receiver can handle, the receiver can notify the sender to slow down.

---

## 🧵 Session Multiplexing

**Session multiplexing** allows a host to support **multiple sessions simultaneously** and manage separate traffic streams over a single link.

> ✅ The transport layer uses **port numbers** to distinguish between different sessions.

### 📦 Example:
- Sender 1 sends:
  - SMTP traffic (Port 25) to Receiver 1
  - HTTP (Port 80) and SMTP (Port 25) to Receiver 2
- The transport layer tracks these sessions using:
  - **Destination Port**
  - **Source Port**

When Receiver 1 responds:
- It **swaps the source and destination ports** to complete the communication.
  - Example:
    - Outbound: `SRC:1500` → `DST:80`
    - Inbound: `SRC:80` → `DST:1500`

---

## 🛠 TCP (Transmission Control Protocol)

TCP is a **connection-oriented**, **reliable** protocol.

### ✅ Key Features:
- Requires a **handshake** before data transmission
- **Segments** data and ensures it’s received in **order**
- Guarantees **delivery** using acknowledgements (ACKs)
- Supports **flow control** and **error recovery**

### 🤝 TCP Three-Way Handshake:
1. `SYN` (Client → Server)
2. `SYN-ACK` (Server → Client)
3. `ACK` (Client → Server)

### 🧱 TCP Header:
Carries additional information such as:
- Sequence numbers
- Acknowledgement numbers
- Window size
- Control flags

---

## 🚀 UDP (User Datagram Protocol)

UDP is a **connectionless**, **unreliable** protocol designed for **low-latency** communication.

### ❌ No Guarantees:
- No handshaking
- No sequencing
- No acknowledgements
- No flow control

If reliability is needed, it must be **handled by upper layers** of the stack.

### 🔹 UDP Header:
- Lightweight and simpler than TCP
- Contains only basic information

---

## ⚖️ TCP vs UDP

| Feature               | TCP                              | UDP                            |
|-----------------------|----------------------------------|--------------------------------|
| Connection Type       | Connection-Oriented              | Connectionless                 |
| Reliability           | Reliable (ACKs, sequencing)      | Unreliable                     |
| Flow Control          | Yes                              | No                             |
| Overhead              | Higher (more headers, processing)| Low                            |
| Use Case              | Apps needing accuracy            | Real-time apps needing speed   |

---

## 🎯 Protocol Examples

| Protocol | Transport Layer | Port | Description            |
|----------|------------------|------|------------------------|
| FTP      | TCP              | 21   | File Transfer Protocol |
| SSH      | TCP              | 22   | Secure Shell           |
| Telnet   | TCP              | 23   | Remote Login           |
| HTTP     | TCP              | 80   | Web Traffic (Unsecure) |
| HTTPS    | TCP              | 443  | Web Traffic (Secure)   |
| TFTP     | UDP              | 69   | Trivial File Transfer  |
| SNMP     | UDP              | 161  | Network Monitoring     |
| DNS      | TCP/UDP          | 53   | Domain Name Resolution |

> 📝 **Note:** DNS uses both TCP and UDP. Typically, DNS uses UDP for queries and TCP for zone transfers or responses over 512 bytes.

---
