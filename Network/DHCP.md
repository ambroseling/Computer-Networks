#### Why DHCP?
- **IP addresses can be assigned dynamically** instead of being manually configured.
- Supports **mobile users**, **address reuse**, and **automatic configuration**.
### DHCP Process (Four Steps)
1. **DHCP Discover** – Client broadcasts a request for an IP address.
2. **DHCP Offer** – Server responds with an available IP address.
3. **DHCP Request** – Client requests to use the offered IP.
4. **DHCP Acknowledge (ACK)** – Server confirms and assigns the IP.

### Key Features of DHCP
- **Supports address leasing** – Clients get an IP **only while connected**.
- **Can assign more than just an IP address**:
  - First-hop router’s IP address.
  - DNS server’s IP address.
  - Network mask.
### DHCP in a Network
- Typically, a **DHCP server is co-located with a router**.
- In **VLANs**, each VLAN has its own **DHCP server**.
#### Broadcasting in DHCP
- The DHCP server **broadcasts** the assigned IP to ensure all devices receive it.
- This is important when **multiple DHCP servers** are available.

#### DHCP in Practice
- **A laptop connecting to a network**:
  - Sends a **DHCP request**.
  - The **router running DHCP** assigns an IP.
  - The client receives:
    - **IP address**
    - **First-hop router address**
    - **DNS server address**
- **Encapsulation of DHCP messages**:
  - Sent in **UDP** (port 67, 68).
  - Encapsulated in **IP and Ethernet**.
###  Key Takeaways
- **CIDR solved IP address exhaustion** by allowing flexible subnetting.
- **CIDR reduced routing table size** significantly.
- **DHCP enables automatic IP address assignment**, reducing manual configuration.
- **DHCP provides more than just IP addresses**, helping with network configuration.

