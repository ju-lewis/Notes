
# The Internet

There are no direct physical connections between most pairs of nodes
- We need to tell data where to go
- We need to specify the actual physical signals to be send
- We need to share physical links between pairs
- We need a modular way to handle these tasks separately

## Protocol Stacks

Protocols contain *fields* or *named headers* that carry data

**Fields**:
- We know what they mean based on where in the message they are
**Named headers**:
- We know what they mean based on their label/name

*Payloads* are the main content of the message
- Carried transparently

>[!Example] Postage Example
>
>Examples of protocol stacks for delivering an invitation message.
>
>Invitation -> Memo -> Post
>Invitation -> Letter -> Post
>Invitation -> Letter -> Email


# Network Models
- *Model* the network as a stack of layers
- Each layer offers services to layers above it.
- Inter-layer exchanges are conducted according to a protocol

## Services to Protocols Relationship
A service is a set of primitives that a layer provides to a layer above it
- Interface between layers


Protocols are the rules which govern the format and meaning of packets that are exchanged by peers within a layer
- Packets send between peer entities


## Connection-Oriented and Connectionless Protocols
Connection Oriented: (e.g. TCP, MPLS)
- Connect, use, disconnect
- Negotiation inherent in connection setup
- Similar to telephone service

Connectionless (e.g. UDP, HTTP)
- Each message is self-contained
- Similar to text message

The choice of service type affects the reliability, quality, and cost of the service itself


## TCP/IP vs. OSI
The TCP/IP model reflects what happens on the internet

The OSI model helps reflect the though process that should be followed when designing a network or diagnosing a fault

View the OSI model as idealised, but with a degree of flexibility


# OSI Model

## Physical Layer
The physical layer is the only layer that actually does communication (e.g. signals over wire, RF communication, etc.)

All higher layers communicate with their peer by sending the signals down the layers and through the physical links


We'll focus on *application*, *transport*, and *network* layers.

**Point-to-point, end-to-end**


# TCP/IP Model

Transmission Control Protocol/Internet Protocol

![[protocol-stack-comparison.png]]


# Using Protocols

Each layer encapsulates the content from the layer above

>[!Example] Postage Example
>- An invitation gets written on a letter (adds headers like date/recipient name)
>- Letter gets placed in an envelope (transport layer)
>- Envelope is loaded into a truck (Network layer)
>- Delivery system transports it to a destination (Physical + data link)


We'll be looking at:
**Application Layer Protocols**
- HTTP, FTP, SMTP, DNS
**Transport Layer Protocols**
- TCP, UDP
**Network Layer**
- IP


## IP: The "narrow waist"

Some people say the internet protocols are like an hourglass
- Many application protocols
- One network protocol (IP)
- Many link layer protocols

"IP over everything, and everything over IP"



# Network Architecture

The narrow waist is part of the "architecture" of the network
- Design decisions that go beyond individual layers
- Hard to change - good to get them right from the start
- But trying too hard leads to stagnation, like OSI suffered



