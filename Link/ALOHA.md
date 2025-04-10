#### Slotted ALOHA
- Pros:
	- single active node can continuously transmit at full rate of channel 
	- highly decentralized: only slots in nodes need to be in sync
-  Cons:
	- collisions, wasting slots
	- idle slots
	- nodes may be able to detect collision in less than time to transmit packet
	- clock synchronization
- Efficiency: long run fraction of successful slots
- Binomial Distribution
	- $p(X=k) = {N \choose k} p^k (1-p)^{N-k}$
	- $p(idle) = p(X=0) = (1-p)^N$
	- $p(success) = p(X=1) = N p (1-p)^{N-1}$
	- $p(collision) = p(X \ge 2) = 1 - (1-p)^N - Np(1-p)^{N-1}$
	- $p(\text{success in given node in a slot}) = P_s = p(1-p)^{N-1}$
	- $\text{average time for succesful transmission} = \frac{1}{P_s}$
- Max efficiency: $\frac{1}{e}  = 0.37$


#### Unslotted / Pure ALOHA
- simpler, no synchronization
- when frame first arrives, transmits immediately
- collision probability increases $\rightarrow$ frame sent at $t_0$ collides with other frames sent in $[t_0-1.t_0+1]$
- Max efficiency: $\frac{1}{2e} = 0.18$


