# 11.0 – Cisco Device Functions (Summary)

---

## 11.1 – Switches vs Hubs

Both **hubs** and **switches** allow Ethernet-connected end-hosts (PCs, printers, servers) to communicate in a LAN.

Switches can scale networks by **cascading multiple switches** together. E.g., connect a 48-port switch to another to extend host capacity.

---

### 🔌 Hubs

- Operate at **Layer 1 (Physical Layer)**
- Function in **half-duplex**: send OR receive at a time
- All devices share **one collision domain**
- Use **CSMA/CD** (Carrier-Sense Multiple Access with Collision Detection)
- **Broadcasts** all traffic to all ports → poor efficiency & security

---

### 📶 Switches

- Operate at **Layer 2 (Data Link Layer)** (and partially L1)
- Support **full duplex**: send AND receive simultaneously
- Each port is a **dedicated collision domain**
- Uses **MAC Address Table** to intelligently forward frames
- Floods only unknown or broadcast frames (e.g. ARP)
- More efficient and secure than hubs

#### 🧠 Learning MAC Addresses:

1. Learns source MAC on each frame and maps it to the port
2. If destination MAC is known → forwards frame to that port
3. If destination MAC is unknown → floods frame to all ports (except source)

---

### 🧪 Example: Switch Operation

#### MAC Table Before

| Port | MAC Address |
|------|-------------|
| 1    | 1.1.1.1     |

If PC1 sends to unknown MAC (e.g., 2.2.2.2):
- Frame floods to all except Port 1
- PC2 replies → switch learns 2.2.2.2 is on Port 2

#### MAC Table After

| Port | MAC Address |
|------|-------------|
| 1    | 1.1.1.1     |
| 2    | 2.2.2.2     |

Now traffic between PC1 ↔ PC2 is directly switched.

---

### 🧪 Multi-Switch Example

**Setup:**

- PC1 → Switch 1 Port 1  
- PC2 → Switch 1 Port 2  
- Switch 1 → Switch 2 Port 24  
- PC3 → Switch 2 Port 1  
- PC4 → Switch 2 Port 2  

1. PC1 sends frame to unknown MAC 2.2.2.2  
2. Switch 1 floods → Switch 2 floods  
3. PC2 replies → Switch 1 learns 2.2.2.2, Switch 2 learns 1.1.1.1  
4. Future traffic is directed via MAC tables only

#### Final MAC Tables

**Switch 1**

| Port | MAC Address |
|------|-------------|
| 1    | 1.1.1.1     |
| 2    | 2.2.2.2     |
| 24   | 3.3.3.3     |

**Switch 2**

| Port | MAC Address |
|------|-------------|
| 24   | 1.1.1.1     |
| 1    | 3.3.3.3     |
| 24   | 2.2.2.2     |

---

## 11.2 – Switch Operation Summary

- **Learning**: Source MAC learned and added to MAC table
- **Forwarding**: If MAC is known → forward to correct port
- **Flooding**: If unknown or broadcast → send to all ports

---

## 11.3 – Routers

- Operate at **Layer 3 (Network Layer)** and below
- Required for **inter-subnet routing**
- Know **paths to remote IP subnets**
- Do NOT forward broadcast traffic (by default)

### 🆚 Routers vs Switches

| Feature         | Switch                     | Router                            |
|-----------------|----------------------------|------------------------------------|
| Layer Awareness | L2 (some L3 in L3 switches)| L3 and below (often up to L7)     |
| Interfaces      | Ethernet                   | Ethernet, Serial, ADSL, etc.       |
| Ports           | Many                       | Fewer                             |
| Broadcast       | Forwards                   | Blocks by default                 |

---

### 🧩 Layer 3 Switches

- Switches that support **routing between subnets**
- Still primarily support **Ethernet only**
- Used in enterprise core/distribution layers

---

## 11.4 – Other Cisco Devices

### 🔐 Security

- **Cisco ASA** – Adaptive Security Appliance (Firewall)
- **Cisco SourceFire** / **FirePower** – Intrusion Prevention System (IPS)

### 📡 Wireless

- **Cisco Wireless LAN Controller**
- **Cisco Wireless Access Point**

### 🤝 Collaboration

- **Cisco Unified Communication Manager**
- **Cisco IP Phones**
- **Cisco TelePresence**
- **Cisco WebEx**

### 🏢 Data Center

- **Cisco UCS** – Unified Computing System
- **Cisco Nexus Switches**

---
