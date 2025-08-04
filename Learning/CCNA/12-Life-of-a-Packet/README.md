
# 12.0 – The Life of a Packet (summary)

## 12.1 – 🌐 DNS: The Domain Name System

- DNS resolves **FQDNs (Fully Qualified Domain Names)** like `www.google.com` into IP addresses.
- Enterprises typically use an **internal DNS server** to resolve internal hostnames.
  - If a query can't be resolved internally, it's forwarded to a public DNS server.
- DNS uses:
  - **UDP/53** primarily
  - **TCP/53** as a fallback when necessary

---

## 12.2 – 🔧 Configuring DNS on Cisco Routers

### Client-side configuration:
```cisco
ip domain-lookup
ip name-server 172.23.4.1
ip domain-name flashboxa.lab
ip domain-list flaskboxb.lab
```
### Enable DNS service on router and set static mappings:
```cisco
ip dns server
ip host LinuxA 172.23.4.2
```
### Example – Router 3 as DNS Server:
```csico
conf t
ip domain-lookup
ip name-server 10.10.20.1
ip domain-name testbox.lab
ip dns server

ip host R1 10.10.10.1
ip host R2 10.10.10.2
ip host R3 10.10.20.1

ip host R1.testbox.lab 10.10.10.1
ip host R2.testbox.lab 10.10.10.2
ip host R3.testbox.lab 10.10.20.1
```
### Example – Router 1 as DNS Client:
```cisco
conf t
ip domain-lookup
ip name-server 10.10.20.1
ip domain-list testbox.lab
```

---

## 12.3 – 🔁 ARP: Address Resolution Protocol
### IP-to-MAC Mapping
If Host A knows the IP but not the MAC of Host B → it uses ARP to resolve it.

### ARP Request:
```
"Who has 172.23.4.2? Tell 172.23.4.1"
Src MAC: 1111.2222.3333
Dst MAC: FFFF.FFFF.FFFF
```
### ARP Reply:
```
"Here I am."
Src MAC: 2222.3333.4444
Dst MAC: 1111.2222.3333
```
### ARP Cache Commands
#### Windows:
```bash
arp -a                            # View
netsh interface ip delete arpcache # Clear
```

#### Linux:
```bash
arp -n
ip -s -s neigh flush all
```

---

## 🌍 12.4 – ARP for Routed Traffic

When traffic is destined to another **subnet**, it is sent to the **default gateway**, not directly to the destination.

### 🧾 Example

| Host         | IP            | MAC             | Default Gateway   |
|--------------|---------------|------------------|--------------------|
| Sender       | 172.23.4.1    | 1111.2222.3333   | 172.23.4.254       |
| Router (SW1) | 172.23.4.254  | 4444.5555.6666   | -                  |
| Receiver     | 192.168.10.1  | 2222.3333.4444   | 192.168.10.254     |

### 🔁 Flow Summary

1. **Host** sends ARP request for the **default gateway’s MAC**
2. **Router** replies → Host sends IP packet to the **Router**
3. **Router** forwards the packet based on its **routing table**
4. If next-hop MAC is **unknown**, router sends ARP request to resolve it and **completes the delivery**

---

## 📦 12.5 – Full Life of a Packet

### 🎯 Objective  
**Host A** wants to access `www.testbox.com`.

### 🧾 Device Overview

| Device        | IP             | MAC             |
|---------------|----------------|------------------|
| Host A        | 10.10.10.10    | 1111.2222.3333   |
| DNS Server    | 10.10.100.10   | 3333.4444.5555   |
| Web Server    | 10.10.12.10    | 2222.3333.4444   |
| Routers/Switches | _See full sequence_ | _Multiple_ |

---

### 🧭 Step-by-Step Summary

1. **DNS Lookup Begins**  
   Host A initiates DNS query for `www.testbox.com`  
   → Detects destination is outside local subnet → uses **default gateway**

2. **ARP for Default Gateway**  
   Broadcast ARP request → Router replies with its MAC  
   → Host A updates ARP cache → Sends DNS query

3. **Router Forwards to DNS**  
   Router checks routing table  
   → Sends ARP request to resolve DNS server’s MAC  
   → Forwards DNS packet

4. **DNS Response Returned**  
   DNS replies with IP for `www.testbox.com` → `10.10.12.10`  
   → Packet flows back to Host A

5. **HTTP Request Initiated**  
   Host A sends HTTP GET request to `10.10.12.10`  
   → Router determines route via Router B → performs ARP for next hop

6. **ARP Chain & Forwarding**  
   Routers resolve MACs hop-by-hop  
   → Packet reaches the **Web Server**

7. **Web Server Responds**  
   Web server uses cached MAC of gateway  
   → Sends HTTP response to Host A

8. **Host A Receives Web Page**  
   Host receives TCP response  
   → Web page content rendered by browser

---

## 🧠 Key Concepts Reinforced

- **DNS** – FQDN → IP via **UDP/53**
- **ARP** – Resolves IP → MAC for local delivery
- **Routing** – Default gateway MAC resolution is key
- **Router Logic** – Uses both **ARP** and **routing tables**
- **Efficiency** – After ARP and MAC tables are populated → traffic is unicast and fast

---
