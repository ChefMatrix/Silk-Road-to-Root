# 10.0 - OSI Layer 1: Physical Layer (Summary)

## 10.1 - Ethernet Connection Media

### ⚙️ The Physical Layer

- OSI **Layer 1** conveys the bit stream using **electrical impulses**, **light**, or **radio signals**.
- Operates at the **electrical and mechanical** level.
- Responsible for the **hardware transmission** of data: cables, interface cards, connectors.

---

### 🔌 Ethernet Media Types

Ethernet LAN connections can be carried over:

- **Coaxial cable** *(obsolete)*
- **UTP (Unshielded Twisted Pair)** *(common for desktops)*
- **Fiber optic** *(for high speed/long distance)*
- **Wireless** *(for mobile/flexible use)*

---

### 🧵 UTP (Unshielded Twisted Pair)

- Commonly used for desktop-to-switch connections.
- Connector: **RJ-45**
- Max cable length: **100 meters**

#### 📈 UTP Cable Categories

| Category | Maximum Bandwidth |
|----------|-------------------|
| Cat 5    | 100 Mbps          |
| Cat 5e   | 1 Gbps            |
| Cat 6    | 10 Gbps           |
| Cat 6a   | 10 Gbps           |
| Cat 7    | 10 Gbps           |
| Cat 8    | 40 Gbps           |

---

### 🔁 Straight-Through vs Crossover

| Cable Type       | Use Case                                 |
|------------------|-------------------------------------------|
| Straight-Through | PC/Router → Switch                        |
| Crossover        | Device ↔ Device (same type)               |

- **Auto MDI-X**: Modern switches auto-configure TX/RX, eliminating the need to worry about cable type.

---

### 💡 Fiber Optic Cables

- Used for **long-distance** or **high-bandwidth** connections.
  - E.g., inter-building, switch-to-switch

#### 🔬 Single Mode vs Multi Mode

| Fiber Type   | Description                                   |
|--------------|-----------------------------------------------|
| Single Mode  | Longer distances, higher bandwidth, more $$   |
| Multi Mode   | Shorter distances, cost-effective             |

---
