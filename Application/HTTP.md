- Properties
	- uses TCP (initiates TCP connection (creates socket) to server)
	- server accepts TCP connection, messages exchange, close connection
	- stateless $\rightarrow$ maintains no information about past client requests
	- HTTP 1.1 Properties
		- server responds in order (FCFS) to GET requests
		- small objects have to wait for transmission (HOL blocking)
		- loss recovery (retransmitting lost TCP segments) stalls object transmission
- Request message (ASCII human readable format):
	- request line
	- header lines
	- carriage return
- Response message:
	- status line
	- header line
	- data requested
	- status code:
- Non Persistent HTTP VS Persistent HTTP
	- Non Persistent
		- requires 2 RTTs per object (1 RTT for connection, 1 for sending/receiving data)
		- OS overhead for each TCP connection
		- browser keeps multiple TCP connections in parallel to fetch referenced objects 
		- Response time = 2 RTT + File transmission time (time for entire file to be delivered to client)
	- Persistent
		- server leaves connection open after 
		- all subsequent HTTP messages are sent over open connection
		- client sends requests as soon as it encounters a referenced object
- HTTP/2 to HTTP/3 (goal: decrease delay in multiple object HTTP requests)
- HTTP/2 Properties
	- recovery from packet loss still stalls all object transmissions
	- no security over vanilla TCP connection
	- objects are divided into frames, then **interleave** frame transmission
	- combats Head of Line blocking (where a request at the front of queue blocks other requests from being processed)
	- transmission order of requested objects based on client specific object priority 
	- push unrequested objects to client
- HTTP/3 
	- adds security, per object error and congestion control (more pipelining) over UDP



### Protocol Comparison

| Feature | **HTTP/1.1** | **HTTP/2** | **HTTP/3** |
|--------|--------------|------------|------------|
| **Introduced** | 1999 | 2015 | 2022 |
| **Transport** | TCP | TCP | **QUIC over UDP** |
| **Connection Setup** | Multi-RTT | Multi-RTT with ALPN | **0-RTT (faster)** |
| **Multiplexing** | ❌ | ✅ | ✅ |
| **Header Compression** | ❌ | ✅ (HPACK) | ✅ (QPACK) |
| **Server Push** | ❌ | ✅ | ✅ |
| **Encryption** | Optional | TLS 1.2+ | **TLS 1.3 (mandatory)** |
| **Head-of-Line Blocking** | Severe | Reduced | **Eliminated** |
| **Connection Migration** | ❌ | ❌ | ✅ (via QUIC) |
### Security
- **HTTP/1**: Optional encryption (can use plain HTTP).
- **HTTP/2**: Requires TLS but allows older versions.
- **HTTP/3**: **Requires TLS 1.3**, with stronger security guarantees built into QUIC.


####  HTTP/1.1
- **Strengths**: Simplicity, wide compatibility, persistent connections.
- **Weaknesses**:
  - No multiplexing → blocking delays.
  - Inefficient headers.
  - High latency on secure connections.
####  HTTP/2
- **Strengths**:
  - Multiplexed streams (parallel requests).
  - Header compression (HPACK).
  - Server push and prioritization.
- **Challenges**:
  - More complex.
  - Still suffers TCP-level head-of-line blocking.
  - Requires HTTPS and ALPN for best use.

#### HTTP/3
- **Strengths**:
  - Built on **QUIC**, reducing latency and improving congestion handling.
  - Eliminates TCP head-of-line blocking.
  - Fast connection setup (0-RTT).
  - Connection migration for mobile.
- **Challenges**:
  - New, not universally supported yet.
  - More complex (UDP-based + QUIC).
  - Some middleboxes and firewalls may block or throttle UDP.

#### Usecases

| Use Case | HTTP/1 | HTTP/2 | HTTP/3 |
|----------|--------|--------|--------|
| Legacy Systems | ✅ | ⚠️ | ❌ |
| Static Sites | ✅ | ✅ | ✅ |
| High-traffic APIs | ⚠️ | ✅ | ✅ |
| Mobile/Realtime Apps | ⚠️ | ✅ | **✅✅** |
| Video Streaming | ⚠️ | ✅ | **✅** |
| CDNs & Edge Delivery | ⚠️ | ✅ | ✅ (growing support) |


#### Conditional GET requests
- goal: don't send object if cache has up-to-date cached version
- cache: specify date of cached copy in HTTP request
- server: response contains no object if cached copy is up-to-date