
# DNS
- Application layer protocol
Maps variable-length domain names to fixed-length IP addresses

DNS is comprised of 4 elements:
- *Domain name space*
	- Tree-structured name space to identify resources on the internet
- *DNS database*
	- Each node/leaf in the name space tree names a set of information that is organised in a *resource record (RR)*
	- RRs are organised in a distributed database
- *Name servers*
	- Server programs that hold information about a portion of the domain name tree structure and the associated RRs
- *Resolvers*
	- Programs that extract information


## Domain Names
- Not case sensitive
- *Constituents* are separated by "."
- Can have up to 63 character per constituent
- Can have up to 255 characters per path
- After 1999 these became a subset of unicode characters (instead of just ASCII)

**Top-level domains (TLD)**
- Generic TLDs
- Country TLDs

## Resource Records
- SOA Record
	- Start of Authority (signals the start of a resource record)
- A Record
	- IPv4 address of a host
- AAAA Record
	- IPv6 address of a host
- MX Record
	- Mail exchange
	- Host that handles the mail protocol can be different to the standard address resolution host
- NS Record
	- Name of a server for this domain
- CNAME Record
	- Domain name (alias), allows you to enter slightly different names to go to the same address.

DNS record names come in two different forms:
- Absolute domain names
	- End with a "." in the record
	- E.g. `cs.vu.nl`
- Relative domain names
	- End with nothing, signals that it is relative to an absolute path
	- E.g. `www` -> `www.cs.vu.nl`

>[!Example]
> ![[resource-record-example.png]]

## Name Server Zones

**Zones:**
- DNS namespaces is divided into non-overlapping zones
	- The name servers are authoritative for that zone
- Name servers are arranged hierarchically manner extending from a set of *root servers*

**Root name servers:**
- The root servers form the authoritative cluster for enquiries
- The root servers are contacted by a local name server that cannot resolve name


### Types of Name Servers
**Top-level domain DNS servers:**
- Responsible for com, org, net, edu, etc, all top-level country domains
- Examples include: *Network Solutions* maintains servers for com; and *Educause* for edu

**Other authoritative DNS servers:**
- Organisations DNS servers, providing authoritative hostname to IP mappings for organisations
- Can be maintained by organisations or service providers

**Local DNS servers:**
- Typically each ISP has a default name server which handles DNS queries
- Returns cached value if one exists
- Otherwise, acts as a proxy, and forwards the request to the hierarchy


>[!Example] Full DNS Resolution Example
>This example assumes *nothing* is cached (i.e. we need to query for all domain constituents)
> ![[dns-resolution-example.png]]

# Email

## Email Services and Architecture
1. Sender (user agent)
2. Message transfer agents
3. Receiver (user agent)

## User Agent (Mail Programs)
**Basic Functions**:
- Compose, report, display, dispose

## SMTP - Simple Message Transfer Protocol
SMTP uses TCP to transfer email messages *from client to server*, default port 25.
- Also used for transfer between mail servers
- Typically direct transfer (sending server to receiving server)

Three phases of transfer:
1. Handshaking
2. Transfer of messages
3. Closure

Command/response interactions
- Commands in ASCII text

SMTP performs all of the *transfer* (up to the mail sever), but not the *delivery*.
- A different protocol is used to actually deliver the mail to the recipient's user agent

## POP3/IMAP
Pull protocols
Used by the final receiver to pull the emails to their device
