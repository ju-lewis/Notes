
# Lecture Summary
- Transport layer overview
- Services provided
- Simple example: UDP


# Transport Layer

>[!Info] Role
>Provide services needed by applications, using services available by the network layer

Services provide a "logical" communication channel between processes running on different hosts
- *Connection oriented*:
	- Connection establishment, data transfer, connection release
	- Like a phone call
- *Connectionless*
	- Like a text message


**Application Needs**:
- Data from one application is not mixed with that for another
- Data doesn't arrive faster than we can handle
- Data is a stream of bytes
- Data arrives reliably (or we know when a packet has been lost)

**Network Provides**:
- Get packets from host to host
	- Most of the time
	- Sometimes multiple copies

## Transport Layer Services

**Terminology**:
- Segments - sent at the transport layer
- Packets - sent at the internet/network layer
- Frames - sent at the link/data link layer


An *unreliable* connectionless server
- Provides *multiplexing* between different processes

A *reliable* connection oriented service
- Provides a notional "perfect" connection between two nodes
- Hides acknowledgements, congestion control, lost packets
- The service is provided to the higher layers

## Transport Layer Encapsulation
- Abstract representation of messages sent to and from transport entities
- Encapsulation of *segments* in *packets* in *frames*

### Multiplexing / Demultiplexing
Shortened to MUXING and DEMUXING
- Multiplexing - combining multiple distinct streams into a single shared stream
- Demultiplexing - splitting distinct streams out from a single shared stream

#### Multiplexing: Transport Layer Addressing
- Specification of the remote process to "connect to" is required at both the application and transport layers
- Addressing in the transport layer is typically done using *port numbers*
- Full address is a 5-tuple
	- TCP listen sockets and most UDP sockets only have a 3-tuple


#### Port Allocations
- Port numbers can range from 0-65535 (16 bits)
- Allocated by Internet Assigned Numbers Authority (IANA)
- Ports are classified into 3 segments:
	- Well-known
		- 0-1023
	- Registered ports
		- 1024-49151
	- Dynamic ports
		- 49152-65535

## UDP Protocol

The user datagram protocol (UDP) allows for applications to transmit datagrams over IP without a connection
- Transmitting data in segments consisting of a header followed by the payload

UDP headers contain source and destination ports
- UDP socket is really a 3-tuple, but each *network packet* has a 5-tuple (for identifying the remote machine)

The payload is handed to the process which is attached to the specified port at the destination
- Using BIND primitive or similar

### Conversations over UDP
Each message is carried independently

First message to a well-known port, from a dynamic port
Server replies from a well known-port to same dynamic port
Client replies using same ports
- Server can guess it is part of the same conversation, but the payload must say where within the conversation it is


**Summary**
- Simple and efficient
- Suitable for some client-server settings
- UDP is connectionless
	- Each message is carried independently
- Also suitable for real-time services



