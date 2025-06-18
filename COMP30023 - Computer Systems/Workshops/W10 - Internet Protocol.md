# Tutorial Questions

## Q1.
Yes, virtual-circuit networks need to be able to route arbitrary packets, as they must have some protocol for establishing the connections to other routers


## Q2. 
When a new connection is created, The network must first establish a connection route from the source to the destination


## Q3. 
Routers typically have multiple IP addresses, since addresses are bound to *interfaces* not *devices*.

## Q4.
The time-to-live field prevents packets from routing indefinitely in the case of a protocol malfunction or unexpected error

## Q5. 
This technique could be used for malicious purposes, like DDOSing - as it obfuscates the actual origin of the attack. This could adversely affect the actual IP address owner as they'd receive all of the response packets.

## Q6.
**6a.**
The version number (6 in the case of IPv6)

**6b.**
The flow label

**6c.**
If the `uint32_t` were not present, the result would be assumed to be a `uint8_t` (as that's the element type for the array). This would cause the bitshifts to effectively clear the variable instead of extracting the correct 20 bit value.
## Q7.
Your phone changes IP address when you move around as it's connecting to different subnets through the nearest cell tower. IP address changing also occurs on a home computer when your network has been allocated a dynamic (rather than static) IP address from your ISP.

## Q8.

## Q9.
You first need to consider the OSI (or TCP/IP) layer it's to operate in, then you can determine requirements such as reliability, simplicity, speed, etc.
- The solutions to all of these requirements are dependent on the layer of operation for the protocol.

## Q10.
In order to ensure reliability (without in-order guarantee), we must ensure each packet send is received exactly once without caring about the order in which they are received.

To do this, the receiver must acknowledge each packet.
- A simple approach to this would be assigning a unique identifier to each packet and requiring the receiver to acknowledge the identifier of each packet received
- We could use a sliding window for this to prevent needing to record the identifiers of *all* packets simultaneously




