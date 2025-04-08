2 physical topologies
- **bus**: 
	- popular through mid 90s
	- all nodes in same collision domain (can collide each other)
- **switched**:
	- active link layer 2 switch in centre
	- each spoke runs a separate Ethernet protocol

#### Frame Structure
- sending interface encapsulates IP datagram in Ethernet frame ![[Screenshot 2025-04-08 at 12.24.19 AM.png]]
- **Preamble**:
	- used to synchronize receive, sender clock rates
	- 7 bytes of 10101010 followed by 1 byte of 10101011
	- Min Ethernet Frame Size = 64 bytes
	- Max Ethernet Frame Size = 1518 bytes
- **Addresses:**
	- 6 byte source, destination MAC address
	- if adapter receives frame with matching destination address, or with broadcast address, it passes data in frame to network layer protocol
	- otherwise adapter discards frame
- **Type**:
	- indicates higher layer protocol
	- mostly IP but others possible
	- used to demultiplex up at receiver
- **CRC**:
	- cyclic redundancy check at receiver
	- error detected: frame is dropped


### Ethernet Key features
- Connectionless
	- no handshaking between sending and receiving NICs
- Unreliable
	- receiving NIC doesn't send ACKs or NAKs to sending NIC
	- data in dropped frames recovered only if initial sender uses high layer reliability (e.g. TCP) otherwise dropped data lost
- MAC protocol:
	- un-slotted CSMA CD with binary backoff

#### Ethernet CSMA CD Algorithm
- NIC receives datagram from network layer, creates frame
- If NIC senses channel idle, starts frame transmission. If NIC senses channel busy, wait until channel idle, then retransmits
- If NIC transmits entire frame without detecting another transmission, NIC is done with frame 
- If NIC detects another transmission while transmitting,  aborts and sends jam signal
- After aborting, NIC enters **exponential backoff**, after mth collision, NIC chooses K at random from $\{0,1,2,\cdots,2^{m-1}\}$
- **Jam Signal**: make sure all other transmitters are aware of collision 10Mbps Ethernet
- **Bit time**: 0.1 microsecond for 10 Mbps Ethernet



