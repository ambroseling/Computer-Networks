 Causes of congestion
-  configuration: input output link capacity R, 2 flows
- Scenario 1) Host A, Host B, 1 router, infinite buffers
	- 
- Scenario 2) Host A, Host B, 1 router, finite buffers, 
	-  packets can be lost due to full buffers, sender knows when packet has been dropped
	- sender's packets can timeout prematurely and can send 2 copies
	- **cost of congestion**: 
		- more work for the given receiver throughput
		- unneeded retransmissions: link carries multiple copies of a packet
- Scenario 3) 4 senders, multi hop paths, timeout / retransmit
	- as $\lambda_i$ and $\lambda_{in}'$ increases


AIMD (Additive Increase Multiplicative Decrease)
- **additive increase:** increasing sending rate by 1 maximum segment size every RTT until loss detected
- **multiplicative decrease:**  cut sending rate in half at each loss event

