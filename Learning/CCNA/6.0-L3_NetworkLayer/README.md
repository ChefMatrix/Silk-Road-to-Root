# 📡 Section 6 – The Network Layer (Summary)

## 6.1 The IP Header

The network layer is responsible for routing packets to their destinations and for enforcing Quality of Service (QoS). The best-known Layer 3 protocol is **IP (Internet Protocol)**—specifically **IPv4**, which is the focus of this section.

IP is a **connectionless** protocol, meaning it does **not perform acknowledgements** (ACKs) at Layer 3.

Other common Layer 3 protocols include:
- **ICMP** (Internet Control Message Protocol)
- **IPSec** (Internet Protocol Security)

### 🔢 IP Addressing

IP addressing is a **logical addressing** scheme implemented at Layer 3. Network designers use IP addressing to break the network into smaller **subnets**, which:
- Improve network **performance**
- Enhance **security**
- Make **troubleshooting** easier

Unlike Layer 2's flat MAC addressing, Layer 3 introduces logical separation between networks.

### 🧬 IP Header Structure (IPv4)

The IP header is composed of several 32-bit fields:

1. **Version (4-bit)** – IP version (usually 4)
2. **Header Length (4-bit)** – Length of the IP header
3. **Total Length (16-bit)** – Total size of the packet in bytes
4. **Identification (16-bit)** – Used for uniquely identifying fragments of an original IP datagram
5. **Flags (3-bit)** – Used for fragmentation control
6. **Fragment Offset (13-bit)** – Position of this fragment in the original datagram
7. **Time to Live (8-bit)** – Limits the lifetime of the packet
8. **Protocol (8-bit)** – Indicates the Layer 4 protocol (e.g., TCP = 6, UDP = 17)
9. **Header Checksum (16-bit)** – Error checking for the header
10. **Source IP (32-bit)**
11. **Destination IP (32-bit)**
12. **Options + Padding (optional)**
13. **Data (variable length)**

---

## 6.2 Unicast, Broadcast, and Multicast Traffic

There are three core IP traffic types:

| Type      | Description                             |
|-----------|-----------------------------------------|
| Unicast   | Sent to **one specific** destination    |
| Broadcast | Sent to **all hosts** in a subnet       |
| Multicast | Sent to **interested hosts** only       |

### 🧭 Unicast

- Host A sends traffic **only** to Host D.
- Hosts B and C **ignore** the packet.

### 📢 Broadcast

- Sent to **every host** in the local subnet.
- Routers **block** broadcast traffic by default.

### 📡 Multicast

- Sent to a specific group of interested hosts.
- Only **one copy** is transmitted to the switch, which then **delivers it efficiently** to subscribers.

---

## 6.3 Converting from Decimal to Binary

Humans use **decimal** (base-10). Computers use **binary** (base-2).

### 🧠 Binary Refresher

Each binary place value doubles:

| Bit | Value |
|-----|-------|
| 1st | 1     |
| 2nd | 2     |
| 3rd | 4     |
| 4th | 8     |
| 5th | 16    |
| 6th | 32    |
| 7th | 64    |
| 8th | 128   |

Example:  
`236 = 128 + 64 + 32 + 8 + 4 → 11101100`

---

## 6.4 IPv4 Addresses

IPv4 addresses are **32-bit** numbers written in **dotted decimal** format.

Example:  
`192.168.1.1`  
Each octet = 8 bits → 4 × 8 = 32 bits

### 👨‍💻 How to Check Your IP

- Windows: `ipconfig`
- Linux/macOS: `ifconfig`

### 🧭 Static vs Dynamic

- **Static**: Set manually (used for printers, routers, etc.)
- **Dynamic**: Assigned via **DHCP** (used for desktops, laptops, etc.)

---

## 6.5 Calculating IPv4 Addresses in Binary

Each octet ranges from 0 to 255.

Example: `192.168.10.15`

| Octet | Binary         |
|-------|----------------|
| 192   | `11000000`     |
| 168   | `10101000`     |
| 10    | `00001010`     |
| 15    | `00001111`     |

Binary representation:
11000000.10101000.00001010.00001111

---

## 6.6 The Subnet Mask

A **subnet mask** allows a host to determine whether another device is on the same or a different subnet.

Example:

| Address Type | IP Address       | Binary Representation         |
|--------------|------------------|-------------------------------|
| IP           | 192.168.10.15    | `11000000.10101000.00001010.00001111` |
| Subnet Mask  | 255.255.255.0    | `11111111.11111111.11111111.00000000` |

### 📍 Network vs Host

- Network: `192.168.10`
- Host: `15`

### 🛑 Reserved Addresses

- **Network address**: All host bits = `0` → `192.168.10.0`
- **Broadcast address**: All host bits = `1` → `192.168.10.255`

Valid range for hosts:  
`192.168.10.1` → `192.168.10.254`

---

## 6.7 Slash Notation

Instead of dotted decimal, subnet masks can be written in **slash notation** (CIDR).

| Notation | Binary (1’s)             | Dotted Decimal   |
|----------|--------------------------|------------------|
| /8       | `11111111.00000000...`   | 255.0.0.0        |
| /16      | `11111111.11111111...`   | 255.255.0.0      |
| /24      | `11111111.11111111.11111111.00000000` | 255.255.255.0 |

Example:  
`10.10.10.15/8` = Subnet mask of `255.0.0.0`

---

> 🧠 **Note:** Two hosts with the same IP address will cause a conflict on the network. Each host must have a **unique** IP address within its subnet.

---
