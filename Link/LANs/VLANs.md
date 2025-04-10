- Problems with scaling LANs naively
	- Single broadcast domain: 
		- all broadcast traffic (ARP, DHCP, unknown MAC) must cross entire LAN
		- efficiency, security 
	- Administrative Issues
- Key features / Properties
	- a VLAN is switch(es) supporting VLAN capabilities can be configured to define multiple virtual LANs over single LAN infrastructure 
	- VLANs have the same broadcast domain (same packet is sent to all nodes on the VLAN)
	- VLANs do not share same collision domain
#### Port Based VLANs
- switch groups are grouped so that single physical switch operates as multiple virtual switches
- Ports 1- 8 are for 1 VLAN, Ports 9-15 are for another VLAN
- Key features / Properties
	- traffic isolation: define VLAN based on MAC addresses of endpoints, rather than switch port
	- dynamic membership: dynamically assign ports among VLANs
	- forwarding between VLANs (done via routing)

#### Tagged VLANs
- Trunk Port
	- a reserved port for carrying frames btw VLANs defined over multiple physical switches
	- frames forwarded within VLAN between switches
- we need VLAN ID info to distinguish which VLAN the packet is for
-  we use the **802.1q** protocol adds / removes additional header fields for frames forwarded between trunk ports
- VLAN tag is added after source MAC address in each frame (VLAN protocol ID + tag)


![[Screenshot 2025-04-10 at 5.53.08 PM.png]]



