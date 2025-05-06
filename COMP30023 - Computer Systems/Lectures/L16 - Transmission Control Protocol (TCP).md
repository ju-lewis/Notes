

The network layer gets packets end-to-end, but:
- Packets may be lost
- Packets may arrive out of order
- Packets may be duplicated
- Packets may arrive faster than we can process them
- Packets don't say which application they are for
- Packets may be corrupted

The transport layer provides a "cleaner", more "friendly" set of services

# TCP Overview
TCP lets applications transmit and receive a stream of bytes, without worrying about:
- Segmenting into IP datagrams (*stream oriented*)
- Bytes being dropped or duplicated (*reliable*)
- Bytes arriving out of order (*in order*)

TCP transport entity manages TCP streams and interfaces to the IP layer
- TCP entity accepts user data streams, segments them, and sends each piece as a separate IP datagram

Recipient TCP entities reconstruct the original byte streams from the encapsulation


## TCP Service Primitives

| Primitive  | Packet Sent    | Meaning                                |
| ---------- | -------------- | -------------------------------------- |
| Listen     | (none)         | Block until something tries to connect |
| Connect    | CONNECTION REQ |                                        |
| Send       |                |                                        |
| Receive    |                |                                        |
| Disconnect |                |                                        |

## TCP - Service Model

>[!Example]
>Four 512-byte segments sent as separate IP datagrams
>The 2048 bytes of data (may be) delivered to the application as a single TCP packet

The sender and receiver both create sockets
- A kernel data structure named by the 5-tuple of: IP address and port number of local and remote host, and the protocol
- For the TCP service to be activated, connections must be explicitly established between a socket at a sending host (src-host, src-port) and a socket at a receiving host (dest-host, dest-port)


### Features of TCP connections
- Full duplex - data in both directions simultaneously
		- (As opposed to simplex)
- End-to-end - exact pairs of senders and receivers
	- (Opposed to point-to-point)
- Byte streams, not message streams
	- Application layer message boundaries are not preserved
	- Can't tell where one `write()` ends and the next starts
- Buffer capable
	-


Data is exchanged between TCP entities in segments
- Each has a 20-60 byte header, plus *zero or more* data bytes

TCP entities decide how large segments should be, given two constraints:
- IP payload < 65,515 bytes
- Maximum Transfer Unit (MTU) - generally 1500 bytes

Sliding window protocol
- Initial use: reliable data delivery without overloading the receiver
- Now also tied closely with congestion control
- *Info in next lecture*

### TCP Header
- Source port
- Destination port
- Sequence number
- Acknowledgement number
- TCP header length
- TCP flags
- Window size
- Checksum
- Urgent pointer
- Options (0 or more 32-bit words)
- Data (optional)

The header uses 32-bit words to increase processing efficiency (this was particularly important when 32-bit machines were standard)


### TCP - Important Header Fields

Source port - Sending port
Destination port - Receiving port
Sequence number - if `SYN` = 1, initial sequence number; if `SYN` = 0; is accumulated sequence number of the first data byte of this segment
Acknowledgement number - if `ACK` = 1
