# 📘 Section 7: IP Addressing and Classes (Summary)

## 7.1 Class A IP Addresses

### 🧮 Subnet Size
The larger the host portion of a network, the more hosts can be assigned.
- `/8` provides **24 bits** for hosts → ~16.7 million addresses.
- `/24` provides only **8 bits** → 256 addresses (254 usable).

---

### 🌐 Original Internet Addressing Design
The global coordination of IPv4 addressing is performed by **IANA** (Internet Assigned Number Authority).

Originally:
- Companies applied for a block of IP addresses based on need.
- E.g., a company needing 600 hosts would request an appropriately sized block.
- IPv4 was designed assuming **every internet-connected device** would have a **public IP**.

🧠 *Due to poor foresight into internet growth, IPv4 ran out of address space.*

---

### 🅰️ Class A
- Designed for very large networks.
- High-order (first) bit is always `0`.
- **Default subnet mask:** `/8`
- **Range:** `1.0.0.0` to `126.0.0.0`
- **Networks:** 126
- **Hosts per network:** 16,777,214

#### 🔒 Reserved Class A Addresses
- `0.0.0.0/8` → "This network"
- `127.0.0.0/8` → Loopback / localhost (testing)

This wastes over **33 million** addresses.

---

### 🧩 Subnetting in Class A
Organizations would not use all hosts in one giant network.
Instead, they would subnet:

Example:
- Given: `15.0.0.0/8`
- Allocate:
  - `15.0.1.0/24` → Sales (NY)
  - `15.0.2.0/24` → Accounting
  - `15.0.9.0/24` → Sales (Boston)

---

## 7.2 Class B & Class C IP Addresses

### 🅱️ Class B
- Intended for medium to large organizations.
- High-order bits: `10`
- **Default subnet mask:** `/16`
- **Range:** `128.0.0.0` to `191.255.0.0`
- **Networks:** 16,384
- **Hosts per network:** 65,534

Subnetting is common here too.

---

### 🅲 Class C
- Intended for small networks.
- High-order bits: `110`
- **Default subnet mask:** `/24`
- **Range:** `192.0.0.0` to `223.255.255.0`
- **Networks:** 2,097,152
- **Hosts per network:** 254

May be used as-is or further subnetted.

---

### 🔐 Private IP Addresses
Non-routable IP ranges reserved for internal use:

| Class | Private Range                   |
|-------|----------------------------------|
| A     | `10.0.0.0` to `10.255.255.255`   |
| B     | `172.16.0.0` to `172.31.255.255` |
| C     | `192.168.0.0` to `192.168.255.255` |

---

## 7.3 Class D & E IP Addresses

### 🅳 Class D (Multicast)
- High-order bits: `1110`
- **Range:** `224.0.0.0` to `239.255.255.255`
- **No subnet mask**
- Used for sending one packet to multiple interested hosts.
  - E.g. `239.0.0.1` sends to all subscribed multicast receivers.

---

### 🅴 Class E (Experimental)
- High-order bits: `1111`
- **Range:** `240.0.0.0` to `255.255.255.255`
- Not used for general assignment
- **255.255.255.255** is the broadcast address.

---

## 📌 Section Summary

| Class | First Octet     | Slash | Subnet Mask     |
|-------|------------------|-------|------------------|
| A     | 1 – 126          | /8    | 255.0.0.0        |
| B     | 128 – 191        | /16   | 255.255.0.0      |
| C     | 192 – 223        | /24   | 255.255.255.0    |
| D     | 224 – 239        | —     | —                |
| E     | 240 – 255        | —     | —                |
