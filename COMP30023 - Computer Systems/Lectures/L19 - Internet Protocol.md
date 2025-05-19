

# Network Layer
- Most network layer code runs on routers
- Protocol data units called *packets*
- What types of services does the network layer provide?
	- Connectionless
		- Packet switching
		- Minimum required service (send packet)
		- Called *datagram network*
	- Connection-oriented
		- (Virtual) Circuit Switching
			- Asynchronous Transfer Mode - ATM
			- MultiProtocol Label Switching - MPLS

## Store-and-Forward Packet Switching
The internet is a packet switched network

Host H1 wants to send a packet to H2
1. Transmits to the nearest router (A)
2. The packet is buffered while it is arriving (and checksum is verified)
3. If valid, the packet is *stored* until the outgoing interface is free
4. The router *forwards* the packet onto the next router in the path
5. Repeat 2-4


## Packet Forwarding 

### Connectionless (Datagram Networks)
Routers store forwarding tables (routing tables)
- Simple router inputs/outputs

**Pros**
- Routers do not hold state
- Very robust (in case of link failure)
**Cons**
- Slow
### Connection-oriented (Virtual Circuit Networks)

Small virtual circuits are established between routers
- Defined by persistent connections
	- Initial connection requires universal source and destination address, but once a path through the network has been established, the network only needs to track small VC numbers
- Identifiable by virtual circuit (VC) numbers

Each entry in the forwarding tables store:
- "In": Port?, input VC number
- "Out": Port, output VC number

VC number is *local* to a router
- That means we can use *much* smaller numbers to identify hops

**Pros**
- Fast
- Easy congestion control
**Cons**
- Routers store a significant amount of state

## Internet Protocol

**Design Principles**:
- Releasing something that works OK is better than never releasing a perfect standard
- Occam's Razor
- Be strict when sending and tolerant when receiving
- Make clear choices
- Avoid static options and parameters
- Think about scalability
	- This is mainly a modern principle

Responsible for moving the packets through the various networks from source to destination host
- Multiple paths through the networks

### IP Version 4 Protocol

Fields:
- Version
- IHL - header length
- Differentiated service - QoS service class
- ECN - explicit congestion notification
- Total length - Including payload, max 65,535
- Identification - used in the handling of fragmentation
- TTL - countdown of hops, at zero packet is discarded
- Protocol - Transport layer service
- Source and destination
- Options


#### Addresses
- 32-bit number
- Expressed in decimal notation, each byte is shown as a decimal, separated by a period
- IP addresses are given to *interfaces* not hosts. I.e. a host with multiple network cards will have multiple IP addresses
- Supply of IPv4 has basically been exhausted

**Types:**
- Unicast
	- One destination
- Broadcast
	- Send to everyone
- Multicast
	- Send to a particular set of nodes
	- Used for streaming video of live events

### Network and Host Addresses
Hierarchical - encodes the network and host number
- Network in top bits
- Host in bottom bits

Assigned to networks in blocks, the network part will be the same for all hosts on that network
- A network corresponds to a contiguous block of IP address space, called a prefix
- Prefixes are written as the lowest IP address followed by a slash and the size of the network portion (e.g. 192.0.2.0/24)
- An interface must "know" the size of its network part

the network size can also be written as a subnet mask, a binary mask of 1's
- In the case of /24: the subnet mask is 255.255.255.0


### IPv6 Header
- Version: 6
- Differentiated services: 6 bits for service class, 2 bits for congestion control
- Flow label: Pseudo-virtual circuit identifier
- Payload length: Bytes after the *40 byte* header
- Next header: Used to specify additional headers or Protocol (TCP/UDP)
- Hop Limit: Same as TTL
- Source and Destination: 16 byte IPv6 addresses
