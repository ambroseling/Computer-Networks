#### Key features / properties
- **reliable transport** btw sending and receiving process
- **flow control:** sender won't overwhelm receiver
- **congestion control:** throttle sender when network overloaded
- does not provide timing and minimum throughput guarantee 
- **connection oriented**: setup required btw client and serve
- uses a **single** retransmission timer
- retransmissions triggered by:
	- timeout events (if the ACK gets lost, wait for timeout)
	- premature timeout (timeout too early, before ACK was received)
	- duplicate ACKs

#### TCP Segment Structure
![[Screenshot 2025-04-06 at 2.37.47 PM.png]]

#### Sequence numbers:
- a number representing the first byte in the segment's data
#### Acknowledgements:
- sequence number of next byte expected from other side
- cumulative ACKs
#### Sender:
- event: data received from application
- event: timeout
- event: ACK received
#### Initializing (3 way handshake):
- 1) choose init sequence num X, client send TCP SYN msg (SYN bit)
- 2) choose init sequence num Y, server send TCP SYNACK msg (SYN bit)
- 3) client receive SYNACK indicates server is live, send ACK for SYNACK, this segment may contain client to server data (ACK flag set)
#### Closing connection:
- 1) client sends packet with FIN bit set after `clientSocket.close()`
- 2) server sends ACK back, client waits for server to close
- 3) server sends packet FINBit set, server can no longer send data
-  Karn's Algorithm
	- **rule 1:**  if a packet is transmitted, do not use its ACK for the update of the timeout
	- **rule 2:** when a timeout happens, we double the timeout value
		- new_timeout = 2 x old_timeout
- Segment Structure:
	- source port # + dest port #
	- sequence number
	- ack number
	- length of TCP header + flow control: # of bytes receiver willing to accept
- $TimeoutInterval = EstimatedRTT + 4*DevRTT$
- $DevRTT = (1 - \beta) * DevRTT + \beta*|SampleRTT-EstimatedRTT|$
- $EstimatedRTT(new) =(1 -  \alpha) * EstimatedRTT(old) + (\alpha)* SampleRTT$

