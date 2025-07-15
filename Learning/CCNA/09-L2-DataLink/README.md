# 9.0 - OSI Layer 2: Data-Link Layer (Summary)

## 9.1 Local Area Network Layer 2 - Ethernet

### 📦 Layer 2 - The Data Link Layer

- Frames are encoded and decoded into bits at this layer.
- Provides **error detection and correction** for the Physical Layer.
- **Ethernet** is the dominant Layer 2 protocol used on LANs.

---

### 🧱 Ethernet Frame Structure

| Field              | Description                            | Size                     |
|--------------------|----------------------------------------|--------------------------|
| Preamble           | Synchronization                        | 8 Bytes                  |
| Destination Address| Receiver MAC Address                   | 6 Bytes                  |
| Source Address     | Sender MAC Address                     | 6 Bytes                  |
| Length/Ethertype   | Type of payload or length              | 2 Bytes                  |
| Data               | Actual payload                         | 46–1500 Bytes (Variable) |
| FCS                | Frame Check Sequence (error detection) | 4 Bytes                  |

---

### 🔍 Media Access Control (MAC) Address

- Ethernet uses a **48-bit hexadecimal MAC address**.
- MAC = **OUI (24 bits)** + **Vendor Assigned (24 bits)**.

#### 📌 OUI – Organizationally Unique Identifier
- Assigned by **IEEE**.
- Identifies the **manufacturer** of the network interface.

#### 🧬 Vendor Assigned Portion
- Assigned by manufacturer.
- Ensures each MAC is **globally unique**.

**Example:**
```
00:50:56:C0:00:08
```

- `00:50:56` → VMware (OUI)
- `C0:00:08` → Unique NIC value

---
