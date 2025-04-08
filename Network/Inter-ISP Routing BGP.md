Border Gateway Protocol 
- is a path vector protocol, advertises paths
- allows subnets. to advertise its existence and the destinations it can reach to rest of internet
- enables routing between Autonomous Systems
- it provides a means for Autonomous Systems to :
	- **eBGP**: 
		- obtain subnet reachability information from neighbouring Autonomous Systems
		- exchanges routing information between different Autonomous Systems, find best route for data travel
	- **iBGP**: 
		- propagate reachability information to all AS-internal routers
		- used by routers within the same Autonomous System
- BGP basics:
	- 2 BGP routers exchange messages over semi-permanent TCP connection
	- advertising paths to different network prefixes

#### eBGP, iBGP
![[Screenshot 2025-04-07 at 11.12.26 AM.png]]

#### BGP advertisements
- it advertises route in the form of **prefix** and **attributes**


#### BGP messages
- 