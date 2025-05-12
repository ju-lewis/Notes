
# Tutorial Questions

## Q1. 
**1a** No, you can't have multiple TCP connections described by the same 5-tuple
**1b** Yes, as they would have different 5-tuples

## Q2.
Two ports are needed in all cases for a TCP connection (it is a bidirectional protocol)

## Q3.
```c
/* 3a. */
int get_syn_flag(uint8_t *buf) {
	
	// The SYN flag is located in the 13th byte at the 2nd rightmost bit
	return buf[13] & (1 << 1);
}

/* 3b. */
uint8_t *get_first_data_byte(uint8_t *buf) {
	
	// Get the header length (shift to lower 4 bits)
	// NOTE: Remember header_len is in 32 bit words
	uint8_t header_len = buf[12] >> 4;
	
	return buf + (header_len * 4);
}
```


## Q4. 
**4a.** TCP is stream oriented, there is no concept of separate transmissions and this must be handled in the application layer. As a result, the lack of delimiter in this protocol could have resulted in command misinterpreting.

**4b.** Yes, there are multiple ways this protocol could be misinterpreted

## Q5.
A port is part of the identifier for a socket. A socket is a kernel level data structure for representing a connection endpoint.

## Q6.
If the SYN+ACK packet is lost, the machine that sent the original SYN packet will retransmit the SYN packet until it receives back the correct SYN+ACK packet.

## Q7.
**7a.** TCP provides reliable data transfer (using sliding window), but not UDP
**7b.** This is not provided by any transport layer protocols
**7c.** Yes this is provided by TCP, not UDP
**7d.** This cannot be provided by the transport layer
**7e.** UDP preserves these boundaries, but not TCP
**7f.** TCP guarantees this with the sliding window

## Q8.
Reliable delivery without an in-order guarantee 

## Q9.
First, the three-way TCP handshake needs to be performed (3 packets)
Then, the data can be transmitted across 2 segments exactly, however each transmitted packet needs to be acknowledged (SYN, then ACK)
Finally, the connection must be closed with FIN, FIN+ACK, ACK

So overall there are 10 packets sent

## Q10.
