#### Key features / properties
- global: all routers have complete topology and link cost info
- centralized:  network topology is known to all nodes, link costs know to all nodes (using link state broadcast)
- iterative: after k iterations, we know k least cost paths to k destinations
#### Algorithm overview:

![[Screenshot 2025-03-26 at 10.16.03 AM.png]]
- graph G = (N,E)
- N set of routers, E set of links
- each router must broadcast its link state information to other n routers
- O(n) link crossings to disseminate a broadcast message from one source
- each router's message crosses O(n) links, overall O(n^2)
- you use link state if you use the entire topology and link costs of the network

#### Example:
![[Screenshot 2025-04-06 at 7.28.51 PM.png]]![[Screenshot 2025-04-06 at 7.29.27 PM.png]]


#### On Failure Event
- router sets link distance to infinity & floods the network with an update packet
- all routers immediately update their link database & recalculate their shortest paths
- fast recovery