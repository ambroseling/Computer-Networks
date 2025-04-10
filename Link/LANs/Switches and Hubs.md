### Hubs (Repeater)
- a **physical** layer device
- active central element in a star topology
- simple repeated in ethernet LANs
- performs signal regeneration
- all traffic appears in both LANs
### Switches (Bridge)
- a **link** layer device
- performs MAC address filtering
- local traffic stays in own LAN
- key features:
	- store and forward ethernet frames
	- examine incoming frame's MAC address, selectively forward frame to one-or-more outgoing links when frame is to be forwarded on segment, uses CSMA / CD to access segments
	- it is transparent, hosts are unaware of presence of switches
	- plug and play, self learning, switches do not need to be configured, learns which hosts can be reached through interfaces

#### Switch Frame Filtering / Forwarding Algorithm Overview
- Steps:
	- 1) frame received at switch
	- 2) record incoming link, MAC address of sending host
	- 3) index switch table using MAC destination address
	- 4) if entry found for destination
		- if destination on segment from which frame arrived 
			-  drop frame
		- else:
			- forward frame on interface indicated by entry
		else:
		- flood


#### Comparison 

![[Screenshot 2025-04-10 at 11.49.56 AM.png]]


#### Switches VS Routers

| Feature                       | Routers                                                                 | Switches                                                                 |
|------------------------------|-------------------------------------------------------------------------|--------------------------------------------------------------------------|
| Functionality                | Network-layer devices (examine network-layer headers)                   | Link-layer devices (examine link-layer headers)                          |
| Operation Mode               | Store-and-forward                                                       | Store-and-forward                                                        |
| Forwarding Table             | Compute tables using routing algorithms, IP addresses                  | Learn forwarding table using flooding, learning, MAC addresses           |
- Note: we do not replace routers with switches because we always need to broadcast and flood which is a waste of resources