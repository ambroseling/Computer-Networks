#### Network IP Addresses: Allocation & Hierarchical Addressing
- **IP Address Allocation**: 
  - A network gets its subnet from its Internet Service Provider (ISP).
  - Example: An ISP with a block `200.23.16.0/20` allocates smaller subnet blocks (`/23`) to different organizations.
- **Understanding IP Address Allocation by ISPs** (EXPLANATION)
	- 1. ISP's Address Block
		- The ISP (Internet Service Provider) is allocated a block of IP addresses from a larger authority (like ICANN or a Regional Internet Registry).
		- In this example, the ISP is given:
		  - **Binary representation**: `11001000 00010111 00010000 00000000`
		  - **CIDR notation**: `200.23.16.0/20`
		- CIDR Notation (`/20`)
		- The **`/20`** means that the first 20 bits are fixed as the **network prefix**.
		- The remaining **12 bits (32 - 20 = 12)** are available for subnetting or host allocation.
	- 2. Subnet Allocation**
		The ISP takes the **200.23.16.0/20** block and divides it into **smaller subnets**.
		- The ISP creates **8 subnets**, each having a **/23 prefix**.
		- **Why `/23`?**
		  - The original `/20` block has **12 bits** available for allocation.
		  - If we divide it into **8 subnets**, we use **3 more bits**, making it `/23` (20 + 3 = 23).
		  - Each `/23` subnet contains **512 IP addresses** (since `2^(32-23) = 512`).
	- 3. Subnet Distribution to Organizations
		- The ISP assigns each **/23 subnet** to different organizations.

| Organization | Binary Representation | Assigned CIDR Block |
|-------------|-----------------------|---------------------|
| Organization 0 | `11001000 00010111 00010000 00000000` | `200.23.16.0/23` |
| Organization 1 | `11001000 00010111 00010010 00000000` | `200.23.18.0/23` |
| Organization 2 | `11001000 00010111 00010100 00000000` | `200.23.20.0/23` |
| ... | ... | ... |
| Organization 7 | `11001000 00010111 00011110 00000000` | `200.23.30.0/23` |
	   **Why is This Approach Useful?**
	5. *Efficient Address Management**  
	   - By using CIDR (`Classless Inter-Domain Routing`), ISPs can allocate **only the required number of IP addresses** to organizations, preventing waste.
	2. **Hierarchical Routing & Aggregation**  
	   - Instead of advertising **8 separate subnets**, the ISP can advertise just **one aggregate route (`200.23.16.0/20`)**.
	   - This reduces **routing table size** and makes Internet routing **more efficient**.

Hierarchical Addressing & Route Aggregation:
	  - Enables efficient advertisement of routing information.
	  - Reduces the size of forwarding tables.
	  - Example: Instead of advertising multiple specific routes, a single aggregated route (e.g., `200.23.16.0/20`) is advertised.
	  
#### CIDR (Classless Inter-Domain Routing) Aggregation:
  - Helps consolidate multiple address ranges into a single prefix.
	  - Example:
	    - Given: `128.100.212.0/24, 128.100.213.0/24, 128.100.214.0/24, 128.100.215.0/24`
	    - Aggregated as: `128.100.212.0/22
- Understanding how CIDR works (EXPLANATION)
	### **CIDR Aggregation (Classless Inter-Domain Routing Aggregation)**
	1.  Why is CIDR Aggregation Needed?
		- In traditional classful addressing, networks were assigned fixed-size blocks (Class A, B, C), leading to **waste of IP addresses**.
		- CIDR allows **flexible allocation** by assigning IP addresses based on need.
		- Without aggregation, routers would have to store **many individual routes**, increasing memory usage and processing time.
	 2. How CIDR Aggregation Works
		- Multiple contiguous IP subnets are combined into a **single larger prefix**.
		- Instead of advertising multiple specific routes, routers advertise a **single aggregated route**.
	 3. Example: Aggregating Four /24 Blocks
	Imagine we have four consecutive subnets:
	
	```
	128.100.212.0/24
	128.100.213.0/24
	128.100.214.0/24
	128.100.215.0/24
	```
	- Each `/24` subnet contains **256 IP addresses**.
	- The first **22 bits** of all these addresses are the same.
	- We **aggregate them into a single** `/22` subnet:
	  ```
	  128.100.212.0/22
	  ```
	- This reduces four separate route entries into **one**.

- Example of CIDR Aggregation in an ISP
	- An ISP owns the address block **200.23.16.0/20** and assigns **8 smaller /23 subnets** to different organizations:
	- Org 0: 200.23.16.0/23
	- Org 1: 200.23.18.0/23
	- Org 2: 200.23.20.0/23
	- ... ...
	- Org 7: 200.23.30.0/23
	1. instead of **8 separate advertisements**, the ISP advertises just:
	```
	200.23.16.0/20
	```
	- This tells other networks:  *"Send all traffic for 200.23.16.0 - 200.23.31.255 to us!"
	- How to Find an Aggregated CIDR Block**
		To aggregate multiple subnets:
		1. **Convert IPs to binary** and find the **longest common prefix**.
		2. Count how many bits remain fixed → This becomes the **new prefix length**.
		3. Write the new aggregated block in **CIDR notation**.
		Example:  192.168.4.0/24  , 192.168.5.0/24  , 192.168.6.0/24  , 192.168.7.0/24  
		Aggregated as: `192.168.4.0/22`
	
		
#### Network Address Translation (NAT)
- **Motivation for NAT**:
  - Helps conserve IPv4 addresses by allowing multiple devices to share a single public IP.
  - Protects internal devices from direct exposure to the public Internet.
  - Allows network changes (e.g., switching ISPs) without reconfiguring internal IP addresses.
  - you have 1 IP address for all devices in your local network
  - you can change addresses of the devices inside the local network without notifying the outside world
- **Types of NAT**:
  1. **Static NAT**:
     - One-to-one mapping between a private IP and a public IP.
     - Example: `192.168.0.2 → 215.234.17.17`
  2. **Dynamic NAT**:
     - Maps private IPs to a pool of public IPs dynamically.
  3. **Overloading (PAT - Port Address Translation)**:
     - Multiple internal addresses share a single public IP by assigning different port numbers.
     - Example: `192.168.0.2:4554 → 56.113.21.44:5001`
     - each computer on the private network is translated to the same IP address but with a different port number assignment

Implementation of NAT
- outgoing datagram: (source IP, port #) -> (NAT IP, new port #)
- remember: (source IP, port #) -> (NAT IP, new port #)
- incoming datagram: (source IP, port #) <- (NAT IP, new port #)
- **NAT Table**:
  - Maintains mappings of internal (private) to external (public) addresses and ports.
  - Example entry:  
    ```
    (192.168.1.1, 5001) <--> (213.31.218.101, 5001)
    ```
#### NAT Traversal Issues & Solutions
- **Problem**:
  - Devices behind NAT cannot be directly addressed from the public Internet.
- **Solutions**:
  1. **Port Forwarding**: Manually configure NAT to forward traffic on a specific port to an internal device.
  2. **UPnP (Universal Plug and Play) IGD (Internet Gateway Device) Protocol**:
     - Allows internal devices to dynamically request public IP mappings.
  3. **STUN, TURN, and ICE**:
     - Protocols used in real-time communication (e.g., VoIP, WebRTC) to traverse NAT.

#### Key Takeaways
- **Hierarchical addressing & route aggregation** optimize routing by reducing routing table size.
- **CIDR** enables efficient allocation and aggregation of IP addresses.
- **NAT** helps with IPv4 address conservation but introduces complexities in direct connectivity.
- **NAT traversal techniques** are essential for applications requiring peer-to-peer communication.

