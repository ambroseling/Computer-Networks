IPv6: Motivation and Features
**Why IPv6?**
- **IPv4 address exhaustion**: The 32-bit IPv4 address space has been completely allocated.
- **Performance improvements**:
  - IPv6 uses a **40-byte fixed-length header** for faster processing and forwarding.
  - Provides **flow-based network-layer treatment**.
**IPv6 Datagram Format**
IPv6 introduces a **128-bit addressing scheme**, significantly increasing the available IP addresses.

Key **differences from IPv4**:
- **No checksum**: This speeds up router processing.
- **No fragmentation/reassembly**: Handled at the transport layer instead.
- **No options in the header**: Options exist as separate headers to maintain a fixed 40-byte header size.

**IPv6 Address Space Comparison**
- Earth's crust volume = **51.1 x 10²⁷ cubic inches**.
- If each cubic inch contains **10,000 grains of sand**, then IPv6 provides **666 billion IP addresses per grain of sand**.

Transition from IPv4 to IPv6
A major challenge is that **not all routers can be upgraded at once**. There is no "flag day" where the world switches to IPv6 overnight. Instead, we use **dual-stack networks** and **tunneling**.

**Tunneling**
IPv6 datagrams are encapsulated **inside IPv4 packets** to be transmitted across IPv4 routers. 
- **Tunneling is widely used** in networks such as **4G/5G**.
- Example:
  - An **IPv6 packet is sent** from an IPv6 router.
  - It is **encapsulated in an IPv4 packet** while traversing an IPv4 network.
  - The **IPv6 packet is extracted** at the destination router.\
 
**IPv6 Adoption Trends**
- **Google:** ~40% of clients access services via IPv6.
- **NIST:** 1/3 of US government domains are IPv6-capable.
- **Slow adoption**: Despite 25+ years of development, IPv6 adoption is still not universal.

