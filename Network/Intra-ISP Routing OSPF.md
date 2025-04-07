#### Autonomous Systems and OSPF
- AS = a group of networks and routers controller by a single administrative authority
- Stub AS:
	- it has only 1 connection to another AS
- Multi-homed AS:
	- can have more than 1 connection to other AS, should not route traffic of the autonomous systems they are connected
- Transient AS:
	- it is connected to more than 1 AS and allows traffic to pass through
	
- Intra AS
	- routing within same AS, all routers in AS must run same intra-domain protocol, routers in different AS can run different intra domain routing protocols
	- gateway router: at edge of its own AS, has link to router in other AS'es
- Inter AS
	- routing among AS, gateways perform inter and intra domain routing

#### Open Shortest Path First Routing
- open: publicly available
- classic link state:
	- uses IP directly
	- each router floods OSPF link state advertisements to all routers in AS
	- multiple link cost metrics possible
	- each router has the full topology, uses Dijkstra's algorithm to compute forwarding table
- advance features
	- security: all OSPF messages are authenticated
	- multiple paths allowed
	- hierarchical OSPF in large domains
	- scalable by breaking a large network into areas
	- OSPF allows virtual networks that abstract the details of physical connections
	- OSPF allows routers to exchange routing information learned from other sites
- Hierarchical OSPF
	- 2 level hierarchy: local area and the backbone (boundary routers form eh backbone, connecting to other ASs)
	- link state advertisements flooded only in area, or backbone
	- each node has detailed area topology; only knows direction to reach other destinations
- Types of Links
	- point to point link: 2 routers 
	- transient link: multiple routers connected on the same network
	- stub link: a sole router supports a single network
	- virtual link: established when the link btw 2 routers is broken, the administrator creates virtual link btw them
- Message Format:
	- uses 24 octet common headers
	- source router IP address $\rightarrow$ address of router sending message


#### OSPF Messages
- Hello Message
	- generated periodically and sent to all neighbour nodes
	- if hello message is not received within interval, link is broken
	![[Screenshot 2025-04-07 at 2.15.15 AM.png]]
- Link State Advertisements
	- router link (Type 1): a true router uses this LSA to announce cost of all links in an area
	- network link (Type 2): designated router distributes this LSA in an area
	- summary link to network (Type 3): 
	- summary link to AS border router 
	- external link (Type 5)
	![[Screenshot 2025-04-07 at 2.11.05 AM.png]]

| Link State Advertisements                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |                                              |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------- |
| 1. **Internal Routers**  <br>   - Send **Type 1 (Router LSAs)**  <br>   - Describe their own links (interfaces), states, and costs within an area.<br>2. **Designated Routers (DRs)** on multi-access networks (e.g., Ethernet)  <br>   - Send **Type 2 (Network LSAs)**  <br>   - Represent the multi-access network and list all routers connected to it.<br>3. **Area Border Routers (ABRs)**  <br>   - Send:<br>     - **Type 1 (Router LSAs)** within their area<br>     - **Type 3 (Summary LSAs)** to advertise routes from one area to another<br>     - **Type 4 LSAs** to describe ASBRs to other areas<br>4. **Autonomous System Boundary Routers (ASBRs)**  <br>   - Send:<br>     - **Type 5 (External LSAs)** — to advertise external (non-OSPF) routes like BGP, static routes, etc.<br>5. **Backbone Routers** (part of Area 0)  <br>   - Behave like internal routers within the backbone — sending Type 1, and possibly Type 3 or 5, depending on their role. | ![[Screenshot 2025-04-07 at 1.45.41 AM.png]] |
