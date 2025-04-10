#### Packet Routing to Another Subnet
- assumptions
	- A knows B's IP address
	- A knows IP address of first hop router, R
	- A knows R's MAC address
- steps:
	- 1) A creates IP datagram with IP source, destination B
	- 2) A creates link layer frame containing A-to-B IP datagram
	- 3) frame received at R, datagram removed, passed up to IP
	- 4) R determines outgoing interface, passes datagram with IP source A, destination B to link layer
	- 5) creates link layer frame containing A to B IP datagram, frame destination address: B's MAC address
	- 6) transmits link layer frame



