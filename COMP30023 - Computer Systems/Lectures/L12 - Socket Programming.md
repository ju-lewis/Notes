
# Using Sockets

The "address" of a socket is the 5-tuple:
- Protocol
	- Transport layer protocol
- local-IP
- local-port number
- remote-IP
- remote-port number

## Berkeley Sockets
Socket interface
- All major OSes copy Berkeley UNIX
- Portability

In UNIX, everything is like a file
- All input is like reading a file
- All output is like writing a file
- file is "addressed" by and integer file descriptor

Our distinction between servers and clients is simply:
- Clients initiate a connection
- Servers accept a connection

### Socket Primitives

- SOCKET - creates a new communication endpoint
- BIND - Associates a local address with a socket
- LISTEN - Announce willingness to accept a connection
- ACCEPT - Accept a connection from a remote machine
- CONNECT - Initiate a connection with a remote machine
- SEND - Send data over the socket
- RECEIVE - Read data over the socket
- CLOSE - Close the socket


### Servers
Servers have two (or more) sockets
- Listening socket (half socket)
	- Identified by: (protocol, local IP address, local port)
- Connection socket(s)
	- Identified by full 5-tuple (protocol, local addr, local port, remote addr, remote port)


Remote machines, when they `connect()` to the server send a request that is received and queued by the listening socket

When the server `accept()`s a connection a full 5-tuple socket is established relating the local and remote machine



### Blocking and Non-Blocking Reads
Over a network data arrives in stages
- Always check how much data was read

If the socket is *blocking*, it waits there until there is *some* data
- May return less than what was sent with a `write()` call

If it's *non-blocking*, it just reads data that has arrived
- May return 0 bytes even if not at the end of the connection

# Transport Layer Security / SSL

Sockets carry plain text
TLS (formerly SSL) encrypts data
Extra "handshake" at the beginning to verify and set up crypto
TLS sits on top of TCP, but then 'looks like' TCP after the handshake has been performed.


TLS can be used for:
- Setting up encryption
- Verifying identities


