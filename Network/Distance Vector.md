Distance vector:
- Idea: you don't know the shortest paths, node $i$ only has local information from neighbours

#### Algorithm Overview
- distance vector algorithm
	- use bellman ford: $D_x(y) = min_v\{ {c_{x,v}+D_v(y)}\}$
		- min taken over all neighbours v of x
		- $D_x(y)$ : v's estimated least cost path to y
		- $c_{x,v}$: direct cost of link from x to v
	- Idea:
		- each node sends its own distance vector estimate to neighbours
		- when x receives new DV estimate from any neighbour, it updates its own DV using bellman ford equation $\rightarrow$ $D_x(y) = min_v\{c_{x,v} + D_v(y)\}$
		- actual cost converges to the actual cost d_x(y)
		- On each node: 
			- 1) wait for change in local link cost or msg from neighbour
			- 2) recompute DV estimates using DV received from neighbour
			- 3) if DV to any destination has changed, notify neighbours
	![[Screenshot 2025-03-26 at 10.42.14 AM.png]]
	
	- iterative asynchronous: each local iteration caused by local link cost change, DV update message from neighbour
	- distributed, self stopping: each node notifies neighbours only when its DV changes
	- Iterative example:
		- ![[Screenshot 2025-03-26 at 11.25.49 AM.png]]
		- Steps:
			- 1) Node 3 and 5 update their distances first cuz its immediate neighbours with destination
			- 2) next up we update Node 1 with distance 3 coming from 3, Node 2 with distance 6 coming from 5, Node 4 with distance 3 coming from 3
			- 3) Node 2 realizes that it can reach destination with shorter cost through 4, with cost 4, so it chooses that path, nothing else gets updated

	- Procedure:
		- add link cost  (A to B, A to C, A to D) to each cost vector
		- take argmin of each column to find the cost vector for node A

#### Example:
![[Screenshot 2025-04-06 at 11.11.11 PM.png]]
- **Iteration 1**: 
	- C no longer has a direct path to F, it looks at its neighbours A and B, A and B stiil think they can reach F through C, C thinks it can reach F via A, so its updated to 1 + A's cost to F
- **Iteration 2**:
	- A hears from C about its new cost of 3, A updates its route to F via B with cost 3
	- B also does the same, it chooses A as next hop to F w/ cost 3
- **Iteration 3**:
	- in the previous iteration, C believes it could reach F via A with cost 3, now C hears from A that A's cost to F is now 3
	- C updates its cost to 3 + 1 = 4 via A
- **Iteration 4**: 
	- A hears from B and C (that cost is 4, link cost is 1), but A can directly get to F with cost of 5, so it directly chooses that path
	- B hears form A (cost of 4), adds link cost of 1, same for C
- **Iteration 5, 6, 7** onwards, the link costs do not change


#### Poisoned Reverse Algorithm
- if a neighbour is selected as the next node to destination, to that neighbour, report infinite distance to the destination

- ![[Screenshot 2025-04-07 at 12.02.07 AM.png]]![[Screenshot 2025-04-07 at 12.04.24 AM.png]]