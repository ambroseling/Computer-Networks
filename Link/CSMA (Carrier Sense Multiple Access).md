- idea is to listen before transmit
- If channel sensed idle: 
	- transmit entire frame
- If channel sensed busy: 
	- **1 persistent:**  keep sensing till channel becomes idle, then transmit
	- **p-persistent:**  wait **until** channel becomes idle, then transmit with probability $p$ and wait a time-slot with probability $(1-p)$
	- **non persistent:** relinquish the channel, wait a random time and sense the channel again
#### Collisions:
- can still occur with carrier sensing
-  collision: entire packet transmission time wasted
### CSMA / CD
- collisions detected within short time
- colliding transmissions **aborted**, reducing channel wastage, reduces the amount of time wasted  in collisions
- collision detection:
	- wired LANs: measure signal strengths, compare transmitted, received signals
	- wireless LANs: received signal strength overwhelmed by local transmission length (CANNOT USE CSMA CD)
#### Algorithm Overview
- NIC receives datagram from the network layer, creates frame
- NIC senses channel:
	- if idle: start frame transmission
	- if busy: wait until channel idle, then transmit
- NIC transmits entire frame without collision, NIC is done with frame
- if NIC detects another transmission while sending: abort, send jam signal
- after aborting, NIC enters binary exponential backoff
	- after $m$th collision, NIC chooses K at random from ${0,1,2,\cdots,2^m}$

#### CSMA / CD Efficiency
- $T_{prop} =$ maximum prop delay between 2 nodes in LAN (within the LAN)
- $t_{trans} =$ time to transmit maximum size frame
- $\text{efficiency} = \frac{1}{1 + 5 \frac{t_{prop}}{t_{trans}}}$ 
- bit better than ALOHA

