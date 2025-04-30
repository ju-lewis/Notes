

# HTTP Overview
Defines resources by URLs
- Uniform resource locator
- Can be absolute, or relative

- Client initiates a TCP connection to server (port 80)
- Server accepts TCP connection from client
- HTTP messages (application-layer protocol messages) exchanged between client and server
- TCP connection closed


HTTP 1.0 - single use connection
HTTP 1.1 - persistent connections, additional headers

## Persistent vs. Non-persistent

**Non-persistent**
- Requires 2 round-trips for requesting any data
- Significant OS overhead from creating sockets
- Can parallelise downloads

**Persistent**
- Can immediately request objects when enough of the HTML has loaded
	- Don't have to wait for full message to complete


With HTTP 1.1 we can *pipeline* requests (i.e. send multiple without receiving a response)
- This is the fastest method
- Limited by the standard


## Key Step Summary
1. Browser determines URL
2. DNS resolution
3. Initiate TCP connection
4. Send HTTP request for the page
5. Server sends the page as HTTP response
6. Browser fetches other URLs as needed, possibly opening more TCP
7. Browser displays the page
8. The TCP connections are released


## Request Methods
- GET  - safe, idempotent, cacheable
- HEAD - ^, ^, ^
- POST - unsafe, not idempotent, uncacheable
- PUT
- DELETE
- CONNECT
- OPTIONS
- TRACE
- PATCH

## HTTP Response Codes
- 1xx - Information
- 2xx - Success
- 3xx - Rediction
- 4xx - Client error
- 5xx - Server error

## HTTP Headers
- Date (request and response) Date and time the message was sent
- Host


## HTTPS - HTTP over TLS
Hardly a separate protocol - mostly just ordinary HTTP over a different service
Everything is encrypted! (including URLS)


# HTTP/2
Compatible at a high level with HTTP 1.1
Aim: decrease latency
- Compress HTTP headers
- Server push
	- if i've just sent HTML containing an \<img\>  tag, I'll start sending the image before you ask for it
- Multiplexing requests over a TCP connection
	- One image doesn't have to wait until the previous is loaded

# HTTP/3
Aim: decrease latency
- Runs over QUIC not TCP: more parallelism, esp. with packet loss
Application layer protocol basically unchanged from HTTP/2
Supported by about 34% of websites, increasing at 1% per year.
