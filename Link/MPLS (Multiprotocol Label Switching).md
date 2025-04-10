- Key features / properties
	- solve high speed IP forwarding among network of MPLS capable routers
	- no need longest prefix matching
	- fixed length label (instead of longest prefix matching)
	- faster lookup using fixed length identifier
	- borrowing ideas from Virtual Circuit (VC) approach
	- but IP datagram still keeps IP address
	- Note: we always route by label not by interface or by IP address
- MPLS routers
	- forward packets to outgoing interface based only on label value (don't look at IP address)
	- MPLS forwarding table is **distinct** from IP forwarding tables
	- is much more flexible and allows re-route flows quickly if link fails: pre-computed backup paths

| Feature                      | IP Routing                                                                 | MPLS Routing                                                                 |
|-----------------------------|-----------------------------------------------------------------------------|------------------------------------------------------------------------------|
| Routing Decision Basis      | Destination address alone                                                  | Can use source and destination address                                      |
| Flexibility                 | Less flexible, one path per destination                                    | More flexible, multiple paths to destination based on different criteria    |
| Example Behavior            | Same destination → same path                                               | Different MPLS routes to same destination based on IP source or other fields|
| General Concept             | Standard IP forwarding                                                     | Flavor of generalized forwarding (like MPLS 10 years earlier)               |
| Fast Reroute Capability     | Not inherently supported                                                   | Supports fast reroute by precomputing backup routes                         |
| Router Types                | IP routers (gray)                                                          | IP/MPLS routers (purple base)                                               |


#### MPLS Signalling
- modify OSPF link state flooding protocol to carry info used by MPLS routing
- entry MPLS router uses a reservation signalling protocol to set up MPLS forwarding at downstream routers

![[Screenshot 2025-04-10 at 6.35.28 PM.png]]