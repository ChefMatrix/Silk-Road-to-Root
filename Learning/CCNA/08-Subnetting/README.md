# 📘 08.0 – Subnetting & CIDR (Summary)

This note introduces subnetting and CIDR (Classless Inter-Domain Routing), explaining how IP address space is more efficiently allocated, structured, and summarized.

---

## 8.1 – CIDR (Classless Inter-Domain Routing)

### ❌ Problem with Classful Addressing
- Class A/B/C blocks were rigid:
  - Class B: 65,534 hosts
  - Class C: 254 hosts
- Companies needing ~300 hosts were forced to use an entire Class B – wasting IP space.

### ✅ CIDR Solution (Introduced in 1993)
- Removes strict class boundaries (/8, /16, /24)
- Allows flexible prefix sizes like `/20`, `/22`, etc.
- **Example**: `175.10.10.0/20` (4096 addresses)

### 🧩 Route Summarisation
- CIDR enables **prefix aggregation**.
- ISPs can advertise one block instead of hundreds of small subnets.

#### Example:
```
ISP A:

175.10.0.0/24

...

175.10.255.0/27 → summarised as 175.10.0.0/16

ISP B:

175.11.0.0/24

...

175.11.255.0/27 → summarised as 175.11.0.0/16
```


### 🔍 Benefits of Summarization
- Smaller routing tables
- Less memory and CPU usage
- Localized fault domains

---

## 8.2 – Subnetting Basics

### 🎯 Why Subnet?
- Break down large address blocks into smaller networks
- Enable separation of departments/regions
- Allow IP address reuse internally with private IPs

### 📐 Borrowing Host Bits
- Given: `200.15.10.0/24`
- Borrowing bits moves the subnet mask rightward (e.g., /25, /26)
- **More subnets, fewer hosts per subnet**

### 📊 Calculations

| Metric | Formula | Example |
|--------|---------|---------|
| Subnets | `2^borrowed` | /28 → 4 bits → 16 subnets |
| Hosts | `2^host bits - 2` | /28 → 4 bits → 14 hosts |

> Subtract 2 for network and broadcast address.

---

## 8.3 – Subnetting Class C & VLSM

### 🔹 /31 Subnetting
- Cisco supports `/31` for **point-to-point** links
- 1 usable bit → 2 IPs, both usable
- Breaks traditional rule: no network/broadcast needed

### 🔹 /30 Subnetting (Traditional)
- 2 host bits: 2 usable hosts
- Commonly used for point-to-point

### 🔹 /29 Subnetting
- 3 host bits: `2^3 - 2 = 6 hosts`
- 32 subnets

### 🔁 VLSM (Variable Length Subnet Masking)
- Allocate different subnet sizes within same address range
- e.g., /30 for routers, /24 for offices
- All modern routing protocols support this

---

## 8.4 – Practice Question

🧮 For `198.22.45.173/26`:
- Subnet Mask: `255.255.255.192`
- Network Address: `198.22.45.128`
- Broadcast: `198.22.45.191`
- Valid Hosts: `198.22.45.129 – 198.22.45.190`
- Next Subnet: `198.22.45.192`

---

## 8.5 – Subnetting Class A & B

### Example 1: Class B `135.15.0.0/16` → `/29`
- Borrowed: 13 bits → 8192 subnets
- Hosts: 4 bits → `2^4 - 2 = 14 hosts`

**Q: `135.15.10.138/29`**
- Subnet Mask: `255.255.255.248`
- Network: `135.15.10.136`
- Broadcast: `135.15.10.143`
- Valid Hosts: `135.15.10.137 – 135.15.10.142`

---

## 🔢 The Magic Number Method

### Example 2: Class A `60.0.0.0/8` → `/28`
- Subnet mask: `255.255.255.240` = /28
- Hosts per subnet: `14`
- Borrowed bits: 20 → `2^20 = 1,048,576 subnets`

**Example 2A: `60.15.10.75/28`**
- Network: `60.15.10.64`
- Broadcast: `60.15.10.79`
- Valid IPs: `60.15.10.65 – 60.15.10.78`

---

## 8.6 – Subnetting on the 3rd Octet

### Class A `60.0.0.0/8` → `/19`
- Borrowed: 11 bits → `2048 subnets`
- Hosts: 13 bits → `8190 hosts per subnet`

**Example: `60.15.10.75/19`**
- Network: `60.15.0.0`
- Broadcast: `60.15.31.255`
- Valid IPs: `60.15.0.1 – 60.15.31.254`

---

## 8.7 – Subnetting on the 4th Octet

**Given: `172.19.216.50/28` (255.255.255.240)**

- Subnets increase by 16:
  - `172.19.216.0`
  - `172.19.216.16`
  - `172.19.216.32`
  - `172.19.216.48` ← belongs here

- Network: `172.19.216.48`
- Broadcast: `172.19.216.63`
- Hosts: `172.19.216.49 – 172.19.216.62`

---

## 8.8 – Subnetting on the 3rd Octet

**Given: `172.19.216.50/23`**

- Subnets increase by 2 on the 3rd octet:
  - `172.19.216.0`
  - `172.19.218.0`

- Network: `172.19.216.0`
- Broadcast: `172.19.217.255`
- Hosts: `172.19.216.1 – 172.19.217.254`

---

## 8.9 – Private IP Addresses (RFC 1918)

| Class | Range | CIDR | Subnet Mask |
|-------|-------|------|-------------|
| A     | 10.0.0.0 – 10.255.255.255 | /8   | 255.0.0.0     |
| B     | 172.16.0.0 – 172.31.255.255 | /12 | 255.240.0.0   |
| C     | 192.168.0.0 – 192.168.255.255 | /16 | 255.255.0.0   |

- **Private IPs** are not routable on the public internet
- Used internally with **NAT (Network Address Translation)**
- Saves IPv4 address space

---

## 8.10 – NAT & IPv6

### 🌍 Why NAT Exists
- IPv4: 32-bit → 4.3 billion addresses
- IPv6: 128-bit → virtually unlimited
- IPv6 was meant to replace IPv4 but adoption is still slow
- NAT allows private IPv4 to access public internet

### 📈 Modern Practice
- Enterprises use:
  - `/24` for user subnets
  - `/30` for point-to-point links
  - `/32` for loopbacks
- VLSM optimizes usage and segmentation

---

## 🔗 Subnetting Practice
- https://subnettingpractice.com/

