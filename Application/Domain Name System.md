- We create a mapping btw IP addresses and names
- We don't do centralized DNS to avoid single point of failure, high traffic volume, high maintenance, does not scale
- Steps
	- 1) client queries a root server for com DNS server
	- 2) client queries com DNS server for amazon.com DNS server
	- 3) client queries amazon.com DNS server to get IP address for wwww.amazon.com
- RootName servers: local DNS contacts this if they cant resolve name
- Top level domain servers: for com,org,net (top level domains)
- Authoritative DNS servers: organization's DNS server, provide hostname to IP mappings, maintained by organization
- Local name server: each ISP has one, when host makes DNS query, query sent to local DNS server
- Name resolution methods:

| Iterated Query                               | Recursive Query                              |
| -------------------------------------------- | -------------------------------------------- |
| ![[Screenshot 2025-02-26 at 1.51.37 PM.png]] | ![[Screenshot 2025-02-26 at 1.52.05 PM.png]] |

- DNS Caching
	- once server learns mapping it caches mapping
	- cache entries timeout after some time
	- TLD servers typically cached in local name servers
- DNS records
	- RR (resource records) format (name, value, type, ttl)
	- Type=A: `name` is hostname, `value` is IP address
	- Type=CNAME: `name` is alias name for some `real` name
	- Type=NS: `name` is domain, `value` is hostname of authoritative name server
	- Type=MX: `value` is name of mail-server associated with name
	- records are inserted by a DNS registrar
- DNS protocol
	- query and reply messages, both with same message format
- DNS uses UDP 
	- no need handshake, reduces latency, queries are usually small, dont need much of the retransmission mechanisms of TCP