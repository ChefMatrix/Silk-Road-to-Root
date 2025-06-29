# 📘 Section 3 – OSI & TCP/IP Models (Summary)

This section documents key concepts from Section 3 of the CCNA course, focusing on the OSI and TCP/IP models, their roles in communication, and the responsibilities of each layer. The intention is to gain a clear and foundational understanding of how data moves through a network — from application to transmission and back.

---

## 🔹 OSI Reference Model Overview

The OSI (Open Systems Interconnection) model is a conceptual framework used to describe how data is transmitted across a network. It is divided into seven layers, each with specific responsibilities during data encapsulation and decapsulation.

### ▶ Data Flow: PC-A to PC-B (Layer 7 → Layer 1)

When a user on PC-A sends an email to PC-B:

1. **Application (L7)** – Creates user data such as sender, recipient, and content
2. **Presentation (L6)** – Formats and encrypts data
3. **Session (L5)** – Establishes and maintains session context
4. **Transport (L4)** – Adds TCP/UDP header with source/destination ports
5. **Network (L3)** – Adds IP addressing; routers operate here
6. **Data Link (L2)** – Adds MAC addressing; switches operate here
7. **Physical (L1)** – Converts data to bits for transmission over the medium

### ◀ Data Flow: PC-B to PC-A (Layer 1 → Layer 7)

On receiving the data:

1. **Physical (L1)** – Receives the bitstream
2. **Data Link (L2)** – Verifies MAC address before passing up
3. **Network (L3)** – Verifies IP address
4. **Transport (L4)** – Identifies service via port number
5. **Session–Application (L5–L7)** – Decapsulates and passes data to application

### ✅ Benefits of the OSI Model

- Allows specialization — network engineers typically focus on Layers 1–4, while developers often work with Layers 5–7
- Helps in isolating and troubleshooting networking issues efficiently

### 🧠 OSI Layer Mnemonic

> **Please Do Not Throw Sausage Pizza Away**

| Layer | Name          |
|-------|---------------|
| 7     | Application   |
| 6     | Presentation  |
| 5     | Session       |
| 4     | Transport     |
| 3     | Network       |
| 2     | Data Link     |
| 1     | Physical      |

---

## 🔹 TCP/IP Suite

The TCP/IP model was developed by ARPA in the 1960s and remains the foundation of modern networking. It contains fewer layers and serves a practical implementation purpose.

| TCP/IP Layer | Corresponds to OSI Layers | Description |
|--------------|----------------------------|-------------|
| Application  | Layers 5–7                 | Handles user data, encoding, and session control |
| Transport    | Layer 4                    | Manages end-to-end communication (TCP/UDP) |
| Internet     | Layer 3                    | Responsible for logical addressing and path selection |
| Link         | Layers 1–2                 | Handles hardware, MAC addressing, and transmission medium |

While the TCP/IP model is used in real-world systems, the OSI model is often referenced for teaching and troubleshooting.

---

## 🔹 Communication Terminology (Encapsulation Terms)

| Layer Group          | Data Unit Name |
|----------------------|----------------|
| Application → App    | **Data**       |
| Transport → Transport| **Segment**    |
| Internet → Internet  | **Packet**     |
| Link → Physical       | **Frame**      |

---

## 🔹 Upper OSI Layers (L5–L7)

These layers are more relevant for software/application-level developers, but still essential to understand from a networking perspective.

### Application Layer (L7)
- Interfaces directly with user applications
- Manages session setup and partner availability
- Ensures reliable access to network services

### Presentation Layer (L6)
- Handles data translation, compression, and encryption
- Ensures cross-platform readability (e.g., encoding schemes)

### Session Layer (L5)
- Manages session establishment, maintenance, and termination
- Tracks multiple simultaneous sessions (e.g., on a web server)

---

## 🔹 Lower OSI Layers (L1–L4)

These layers are critical for network engineers and are discussed in more depth in later sections.

### Transport Layer (L4)
- Splits data into segments and adds source/destination ports
- Supports TCP or UDP communication models
- Enables error checking and reassembly of data

### Network Layer (L3)
- Adds IP headers and logical addressing
- Determines routing paths across different networks
- Routers operate at this layer

### Data Link Layer (L2)
- Adds MAC addressing for frame delivery on local networks
- Switches operate at this layer
- Responsible for error detection at the data frame level

### Physical Layer (L1)
- Handles transmission of raw bits over physical medium
- Includes cables, connectors, voltage levels, and bit rates

---

This summary provides a foundational understanding of how the OSI and TCP/IP models structure and handle data during transmission. The next sections of the course will dive deeper into each lower-layer function and their real-world applications.
