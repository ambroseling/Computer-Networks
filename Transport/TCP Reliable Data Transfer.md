- Reliable data transfer
	- error detection: find that an error has happened in the received data (checksum or cyclic redundancy check)
	- error correction: process of correcting the error (retransmission)
	- we use **sequence number** to distinguish btw packets, field in the header of a TCP segment
	- how to set timeout? timeout > RTT
	- automatic repeat request
		- how we do handshaking:
			- checksum to detect errors
			- ACKs: receiver explicitly tells sender packet is OK 
			- NACKs: receiver tells sender packet has ERRORS
				- if no NAKs, we send ACK for last packet received OK
				- receiver must include sequence number of packet being ACKed

| NACKs                                        | Timeout                                      |
| -------------------------------------------- | -------------------------------------------- |
| ![[Screenshot 2025-02-27 at 8.37.49 PM.png]] | ![[Screenshot 2025-02-27 at 8.38.32 PM.png]] |

- Types of reliable data transfer
	- Stop and Wait (SW)
		- only sends next packet after you received ACK, if you dont receive ACK you wait till timeout and send again
		- time: $\frac{L}{R} + RTT$
		- utilization (fraction of time sender is actually sending): $\frac{\frac{L}{R}}{L/R + RTT}$ 
		- SW has very low utilization
	- Go back N (GBN)
		- a pipelining protocol: send multiple to be ACKed packets
		- $U_{GBN} = \frac{N \times L/R}{RTT + \frac{L}{R}}$
		- can send up to N unACKed packets
		- keep a window of up to N consecutive unACKed packets
		- retransmit all N packets if the first one is lost 
		- only send ACK for **correctly received packets so far**, with highest in order seq #
		- if you get an out of order packet, juts re-ACK packet with higesht in order seq #
		- $N \le 2^m -1$
			- $N$ is window size
			- $m$ is number of bits in sequence number
		- GBN is not efficient on long haul transmission links with high bandwidth![[Screenshot 2025-02-28 at 2.25.37 AM.png]]
	- Selective repeat (Automatic Repeat Request)
		- **sender:** allows up to N unACKed packets in pipeline, maintains timer for ecah unACKed packet, if timer expires retransmit only the unACKed packet
		- **receiver**: individually acknowledges all correctly received packets, buffer packets for in order delivery to upper layer
		- ![[Screenshot 2025-02-28 at 2.25.13 AM.png]]
