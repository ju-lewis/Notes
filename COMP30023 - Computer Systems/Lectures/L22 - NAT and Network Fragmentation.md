
Private addresses were created to address IPv4 scarcity problem
- Many hosts in a company only need internal access
- Private subnets are: 192.168.0.0/16, 172.16.0.0/12, 10.0.0.0/8
- Private IP addresses can be reused

# Network Address Translation
- Each customer/home is assigned one (or a small number) of public IP addresses
- Internally, hosts/interfaces are issued with private IP addresses
	- E.g. 192.168.20.1

NAT changes destination IP and port
- Port changes to prevent collisions

Source port is replaced with index of entry in NAT translation table
- One of 65,536 entries (16 bits - same as TCP port field)
- When a packet arrives from the internet at the NAT box it looks up the destination port from the TCP header
	- Retrieves original source port and source IP address, updates headers and checksums before relaying to the internal host


>[!Warning] Criticisms of NAT
> - Breaks end-to-end connectivity, an interface in the private network can only receive packets once a mapping in the NAT table has been established
> - Violets IP architectural model that states every IP indicates a unique interface
> - Layering violation by assuming nature of payload messages
> - Changes internet from connectionless to pseudo-connection-oriented
> 	- NAT maintains connection state, if it crashes all connections are lost
> - Limits number of connections

Carrier grade NAT:
- ISPs only gives customers private addresses
- Useful for huge numbers of people

NAT also helps with security, since external packets can't initiate connections
- Theoretically you can guess a translated port number

## Attempts to Improve NAT
Universal Plug and Play (UPnP)
- Helps home machines act as servers
- UPnP implements the internet gateway protocol that allows port mappings to be created in the NAT translation table to allow servers to be run on the internal network
- Bad implementations of UPnP have allowed attackers to alter translation tables from external IP addresses

