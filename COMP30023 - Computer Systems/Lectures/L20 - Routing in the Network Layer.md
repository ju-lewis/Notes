
# Packet Forwarding
- Each router has a forwarding (or routing) table
- This maps destination addresses to outgoing interfaces


## Routing
How do these forwarding tables get created?

The routing algorithm decides which output line an incoming packet should be transmitted on
- Combination of:
	- An algo local to each router
	- A protocol to gather the network information needed by the algorithm


### Routing Algorithm
The algorithm should be:
- Correct
- Simple
- Robust
- Stable
- Fair
- Efficient
- Flexible

What do we want to optimise?
- Mean packet delay?
- Max network throughput?

Simplest approach:
- Minimise the number of hops a packet has to make
	- Tends to improve both
	- Hopefully reduces distance travelled
		- Crossing the Pacific is one IP hop
- Actual algorithm gives cost to each link

#### Non-Adaptive (Static)
- Does not adapt to topology
- Calculated offline and uploaded to router at boot
- Does not respond to failure

#### Adaptive
- Dynamic routing, adapts to changes in topology and traffic
- Optimise some property: distance, hops, transit time, etc.
- Dynamically collects information from other routers

#### Flooding
- Send packet to all neighbours who don't have it yet
- Guarantees shortest distance and minimal delay
- Useful benchmark in terms of speed
- Extremely robust (will always find a path)
- Extremely inefficient
- Have to have a way of discarding packets (TTL)

### Optimality Principle (Bellman 1957)
If router $J$ is on the optimal path from router $I$ to $K$, then the optimal path from $J$ to $K$ also falls along the same route.

#### Sink Tree
The optimality principle means that a set of optimal routes from all source form a tree rooted at the destination

We compute this by considering the network as a labelled graph
- We then apply a shortest path algorithm like Dijkstra's algorithm

## Link State Routing
LS is a "distributed" algorithm that replace Distance Vector Routing (which converged slowly)
Variants of Link State Routing used today

Simple 5 step process at each router:
1. Discover its neighbours and learn their network neighbours
2. Set the distance or cost metric to each of its neighbours
3. Construct a packet containing all it has just learned
4. Send the packet to, and receive packets from, all other routers
5. Compute the shortest path to every other router

To discover neighbours, a router on boot sends out a HELLO packet on each interface
- Other router must reply with its unique ID

Cost can be set automatically or manually
- Common technique is 1/bandwidth

### Packet Structure
A link state packet consists of ID, sequence number, age, and a list of their respective costs
- Flooding is used to send packets to all other routers
- Acknowledgements are required to guarantee every other router receives the packet
- To avoid waste, a router discards a link state packet if its sequence number is not larger than a previous one




