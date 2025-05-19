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

## Q6.

## Q7.
ISPs often assign dynamic IPs

## Q8.

## Q10.
In order to ensure reliability (without in-order guarantee), we must ensure each packet send is received exactly once without caring about the order in which they are received.

To do this, the receiver must acknowledge each packet.
- A simple approach to this would be assigning a unique identifier to each packet and requiring the receiver to acknowledge the identifier of each packet received
- We could use a sliding window for this to prevent needing to record the identifiers of *all* packets simultaneously




