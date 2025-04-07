#### CIDR Basics
- CIDR replaces class-based addressing with a more flexible method.
- CIDR notation: Uses an IP address followed by a subnet mask (e.g., `192.168.1.0/24`).
- Allows variable-length subnet masks (VLSM), improving IP allocation efficiency.
- use hierarchical addressing, so you advertise just a less specific address 
![[Screenshot 2025-03-25 at 12.03.38 PM.png]]
#### New Address Allocation Policy
- Instead of assigning large Class A or B addresses, **multiple Class C addresses** are grouped.
- Example:
  - If a company needs **1000 IP addresses**, it can be assigned **four Class C blocks**.
### Supernetting
- Groups **contiguous** Class C addresses into a single block using a **variable-length mask**.
- Example:
  - `214.158.16.0/20` covers **16 Class C blocks**.
  - Another example:
	  - I have 4 class C networks
		- 192.168.0.0/24  
		- 192.168.1.0/24  
		- 192.168.2.0/24  
		- 192.168.3.0/24  
	- Each has a **subnet mask of 255.255.255.0 (/24)**, meaning 256 IP addresses per subnet. Now, instead of routing these four networks separately, you can **combine them into one supernet:
	- We can use supernet: 192.168.0.0/22
		- **Subnet mask**: 255.255.252.0
		- **CIDR**: /22
		- **Covers addresses from**:  
	    `192.168.0.0` to `192.168.3.255`
	- This one supernet route now represents **all four original subnets**.
#### CIDR Reduces Routing Table Size
- Pre-CIDR: **16 contiguous Class C blocks required 16 entries** in a routing table.
- Post-CIDR: **Only 1 entry** is needed for the entire range.
#### **CIDR Basics**
- **CIDR replaces class-based addressing** with a more flexible method.
- **CIDR notation**: Uses an IP address followed by a subnet mask (e.g., `192.168.1.0/24`).
- **Allows variable-length subnet masks (VLSM)**, improving IP allocation efficiency.
- use hierarchical addressing, so you advertise just a less specific address 
- it should reflect the **physical topology** of the network
- network topology follows continental / national boundaries (dictates how IP address are assigned)
![[Screenshot 2025-03-25 at 12.03.38 PM.png]]
#### New Address Allocation Policy
- Instead of assigning large Class A or B addresses, **multiple Class C addresses** are grouped.
- Example:
  - If a company needs **1000 IP addresses**, it can be assigned **four Class C blocks**.
### Supernetting
- Groups **contiguous** Class C addresses into a single block using a **variable-length mask**.
- Example:
  - `214.158.16.0/20` covers **16 Class C blocks**.
#### CIDR Reduces Routing Table Size
- Pre-CIDR: **16 contiguous Class C blocks required 16 entries** in a routing table.
- Post-CIDR: **Only 1 entry** is needed for the entire range.
#### CIDR Routing
- Routes are determined based on the **IP prefix** instead of the class.
- Routing table entries use **<IP address, network mask>**.
- Example:  
  - `192.32.136.0/21` represents a **range of addresses**.
- Routes are determined based on the **IP prefix** instead of the class.
- Routing table entries use **<IP address, network mask>**.
- Example:  
  - `192.32.136.0/21` represents a **range of addresses**.