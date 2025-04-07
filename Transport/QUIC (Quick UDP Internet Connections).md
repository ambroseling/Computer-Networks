- built on top of UDP
- increase performance of HTTP
#### Key features / properties:
- error and congestion control
- connection establishment: 
	- TCP + TLS : 2 serial handshakes
	- QUIC: reliability congestion control, authentication, crypto state, 1 handshake
- they are multiplexed, multiple application level streams **multiplexed** over single QUIC connection