#### Address Resolution Protocol (ARP)
- ARP table: 
	- each IP node (host, router) on LAN has an ARP table
	- IP / MAC address mappings for some LAN nodes
	- TTL (Time To Live): time after which address mapping will be forgotten
- Steps:
	- initially) table is empty
	- 1) destination MAC address = FF-FF...
	- 2) broadcast ARP query, all nodes on LAN receive ARP query
	- 3) B replies to A with ARP response, giving its MAC address
	- 4) A receives B's reply and adds B's MAC address into its local ARP table


#### ARP Protocol Format
- ![[Screenshot 2025-04-10 at 11.35.36 AM.png]]
- note: very similar to IP protocol format

