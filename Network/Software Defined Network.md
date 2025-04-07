**Generalized Forwarding and SDN**
- Traditional networks rely on **destination-based forwarding** (forwarding decisions depend on destination IP address).
- **Generalized Forwarding** in SDN enables:
  - Matching on **multiple header fields** (not just destination IP).
  - Actions like **drop, copy, modify, log, forward**.

Flow:
- flow: defined by header field values (in link, network, transport layer fields)
- generalized forwarding: simple packet-handling rules


**Flow Tables in SDN**
- Routers and switches store a **flow table** that maps packet **header fields to actions**.
- Each flow table entry consists of:
  - **Match Fields** (e.g., source IP, destination IP, MAC address, TCP/UDP port).
  - **Actions** (e.g., forward to a specific port, drop, modify, send to controller).
  - **Priority:** disambiguate overlapping patterns
  - **Counters** (track packet and byte statistics).
#### OpenFlow Protocol
- OpenFlow is a protocol that allows centralized control over packet forwarding decisions.
- OpenFlow Flow Table Entries
	Each entry consists of:
	- **Matching Fields** (e.g., source/destination IP, MAC addresses, transport-layer ports).
	- **Actions**:
	  1. **Forward to port(s)**.
	  2. **Drop the packet**.
	  3. **Modify packet header fields**.
	  4. **Encapsulate & forward to SDN controller**.
	- **Counters** track the number of packets/bytes processed.
- Examples of OpenFlow Applications
	1. **IP-based Forwarding**
	   - Forward all packets **destined for IP 51.6.0.8** to **port 6**.
	2. **Firewall Rule**
	   - Block all traffic to **TCP port 22 (SSH)**.
	   - Block all traffic from **host 128.119.1.1**.
	1. Layer 2 Forwarding
	   - Frames destined for **MAC 22:A7:23:11:E1:02** should be forwarded to **port 3**.
SDN & Network Programmability
	- 
### **Match-Action Abstraction**
OpenFlow generalizes packet processing across different network devices:
- **Routers**: Match on longest **destination IP prefix**, then action: forward.
- **Switches**: Match on **destination MAC address**, then action: forward.
- **Firewalls**: Match on **IP addresses & ports**, then action: allow or deny.
- **NAT Devices**: Match on **IP & port**, then action: rewrite them.
**Network-Wide Orchestration**
With OpenFlow, centralized SDN controllers can create complex **network-wide behaviors**:
- **Example**: Ensure all packets from hosts **h5 & h6** are sent to **h3 or h4 via switch s1**.

### **Summary: Benefits of SDN**
- Decouples **control plane** from **data plane**.
- Enables **programmable networks**.
- Supports **custom traffic management policies**.
- Leads to the development of new networking languages like **P4**.
