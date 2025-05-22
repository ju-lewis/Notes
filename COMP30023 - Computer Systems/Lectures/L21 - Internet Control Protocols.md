
>[!Info] Note
>Protocols don't really form a single stack
>- BGP (network layers) uses TCP (transport layer) for updates
>
>A better model is to think of different "planes" of protocols
>- Data plane
>- Control plane
>- Management plane

## ICMP - Internet Control Message Protocol
**Message Types**
- Destination unreachable
- Time exceeded
- Parameter problem
- Source quench
- Redirect
- Echo and echo reply
- Timestamp request/reply
- Router advertisement/solicitation

ICMP is used by `ping` and `traceroute`

`traceroute` exploits the time exceeded message
- Traceroute sends out packets to the same destination, each with an incremented TTL
- Counters will hit zero at successive routers, causing the router to return a *Time Exceeded* message, revealing the IP address of the router
- Sender can use this information to determine path and timings of the route a packet will take

## DHCP - Dynamic Host Configuration Protocol

The internet layer requires each host/interface to have a unique IP address
- This needs to be configured for each host and network
DHCP automatically handles IP allocation
Security concerns - connecting any device will issue an IP address

### Protocol Behaviour:
- Network has a DHCP server for issuing IP addresses
- Host sends out a DHCP discover packet
	- Routers can be configured to relay these to a remote DHCP server
- DHCP server receives the request and responds with an OFFER packet containing an IP address
- IP addresses are typically leased
	- Leases can be renewed before the lease expires
- Used to set a number of parameters
	- Default gateway
	- DNS servers address
	- Time servers

## MAC - Media Access Control) Address
The DHCP server uses information from the link layer to identify devices before IP assignment

Addressing used at the Host-to-network/data link layer

## ARP - Address Resolution Protocol
ARP is the link between the internet layer and the underlying network layer
- It translates an IP address into a MAC address
Broadcasts an ethernet (or wifi) packet asking who owns the target IP address
- Arrives at every host on the network, the owner will respond with its MAC address
- This protocol is run a lot, even to find out how to communicate with the nearest router

**Properties**
- Simple
- Not efficient
- Security nightmare
	- No authentication
	- Caching of responses, even when no directly requested
	- ARP spoofing is the basis of most man-in-the-middle-attacks
	- Provides a way of intercepting TCP

# Route Aggregation
Routing only requires network prefixes until the target network is reached
- These prefixes can overlap, *exceptions* are defined by the more specific subnet mask


