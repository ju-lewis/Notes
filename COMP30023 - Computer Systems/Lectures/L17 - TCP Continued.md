
# Three-way Handshake
1. SYN packet (with sequence number = $x$)
2. SYN packet (with acknowledgement flag = $x+1$ and seq number) *aka* SYN-ACK
3. ACK packet 
At the end of the handshake, host 1 and host 2 have agreed on respective sequence numbers

SYN refers to synchronisation


## TCP Synchronisation Recap
- SYN bit is used to establish a connection
	- Connection request has SYN=1 ACK=0
	- Reply has SYN=1 ACK=1
- Sequence number - first byte this segment's payload
	- Offset by a random number - initial value is arbitrary
	- Offset will be reflected in both Sequence and Acknowledgement numbers
- Acknowledgement number - *next* byte sender expects to receive
	- Bytes received without gaps
	- A missing segment will stop this incrementing
		- Even if later segments have been received


# TCP Closing
The FIN flag is used to signify a request to close a connection
Each FIN is *directional*
- Once acknowledged, no new data can be *sent* from the sender to the receiver
- Data can continue to flow in the other direction
Typically requires 4 segments to close, 1 FIN and 1 ACK for each direction

The RST flag is used to signify a "hard" close of a connection
- Basically states the sender is closing the connection and will not listen for any further messages
- Sent in reply to a packet sent to a 5-tuple with no open connection

# TCP Sliding Window
Sliding window provides:
- Flow control (not sending too much data to the receiver)
- Reliable delivery
- In-order delivery

Sliding window is controlled by receiver
Determines the amount of data the receiver is able to accept
- Sender and receiver maintain buffers to send and receive data

When the window is 0 the sender should not send any data
- Can send URGENT data
- Can send ACK packets, with 0 bytes of data
- Can send "zero window probe": 0 byte segment that causes the receiver to re-announce the next expected byte and window size (window probe) this is designed to prevent deadlock
Senders may delay sending data, i.e. may wait for the whole window to be empty instead of 'topping it up'

**Multiple Windows**:
- Send window
	- What data the sender is able to send - unacknowledged segments and unsent data that will fit into the receive window
- Receive window
	- Amount of data the receiver is willing to receive (window size in ACK)
- Other windows
	- For congestion control

>[!Note]
>The sender must maintain the invariant:
>LastByteSent - LastByteAcked $\leq$ ReceiveWindowAdvertised


**SYN Flooding**
- Popular DOS attack in the 90s
- Because each SYN request generates an arbitrary random initial sequence number, memory was reserved to record each SYN request number
	- So a bunch of half-initialised TCP sockets are generated and reserve memory
- The solution was SYN cookies
	- Rather than storing sequence number, it is derived from connection information and a timer
	- Hashed

