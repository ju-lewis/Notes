
We've already established that the sliding window provides flow control.

# Sliding Window - Reliable Delivery

The acknowledgement number sent by the receiver expresses what byte it is expecting to receive next.
- If a packet arrives out of order, we can tentatively store it (provided it's in the sliding window), but won't acknowledge it until the actual next expected packet arrives

## Original Flow + Loss Control
Existed on single point-to-point links for a long time
- TCP originally used the experience from the link layer
- Caused a bad design

### Go-Back-N
- When a packet is lost, go back to where it was transmitted and retransmitted from that point onwarsd

### Selective Repeat
- Only retransmit the lost packet
- Packets arrive out-of-order. Receiver must store out-of-order packets to send them in-order to the application
- Much more complex, only helps if loss is common


>[!Note] Congestion Collapse
>In the late 80s the internet had a "congestion collapse"
>- Router buffers were overflowing, causing high loss
>- Senders were using *go-back-N*, so every packet loss caused N more packets to enter the system
>  
>  **Solution**: Packet conservation principle
>- Only retransmit when a packet is no longer in flight

Fast retransmit waits for 3 duplicate acknowledgements to consider a packet lost

>[!Warning] Fast Retransmit Deadlock
>If several packets arrive out of order, and the window fills up, when the final (out of order) packet arrives a cumulative acknowledgement is sent for the entire window, but now the window size is $0$ (since it has been fully used)
>
>This requires waiting for the application to read the data to empty the window

When a sender gets a window of size 0, it starts a *persist timer*
- Periodically transmit **ZeroWindowProbe** segments


# Sliding Window - Congestion Control
When networks are overloaded, we get congestion
- Potentially effects all layers

Lower layers attempt to reduce congestion, but in reality TCP affects congestion most significantly
- TCP offers methods to reduce data rate and hence congestion


Original TCP (before Jacobson)
- Initially, the receiver chooses a window based on its buffer size
- If the sender is constrained to this size, then congestion problems will not occur due to buffer overflow
- May still occur due to congestion within the network

## Congestion Control Window
Jacobson introduced CWND, the congestion window
Additional window that is dynamically adjusted based on network performance to aid efficient transfer
- Maintained by the send, unlike the sliding window that is controlled by the receiver
- Only used at the sender
- No changes to packet formats to send an additional field

### Incremental Congestion Control
- At first CWND <- maximum segment size
- For each segment acknowledged
	- CWND += maximum segment size
	- Sender transmits 2 more segments
- Each full window of acknowledgement *doubles* the congestion window, which grows until:
	- A timeout
	- It reaches a threshold, SSthresh

Eventually too many segments would be placed onto the network causing congestion and timeouts


- When a segment is lost, SSthresh is halved, and slow start begins again
	- This was optimised to only half the window instead of setting it to 0
- Once the SSthresh is reached, the growth is slowed to linear

The initial implementation of the incremental algorithm was *BSD Tahoe*, followed by optimisation in *BSD Reno*


# Protocol Design Exercise
**Remote Procedure Calls**
- Allow calling procedures on a remote server as if they are local to the client
- Hides the networking aspects from the programmer

To hide the networking, the client and server must be bound to respective stubs


>[!Example]
>Design a protocol to support one single function that:
>- Takes one 64-bit integer as an argument
>- Returns one 64-bit integer as the value
>  
>  **Features**:
>- Connectionless for simplicity
>- We just need to transmit the number and an identifier
>- Maybe also a checksum for validity


