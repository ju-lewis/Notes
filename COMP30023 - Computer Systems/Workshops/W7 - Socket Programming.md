

# Tutorial Questions

## 1. Socket Syscalls
You would lose the flexibility of being able to establish full socket vs. half socket servers


## 3. Socket Syscalls Continued

**3a.** 
- Passive open -> `bind`, `listen`, `accept`
- Active connect -> `connect`

**3b.** Listen creates a queue to store all connection requests. Allocates required interface structures. Accept actually allows external connections to be made and passed on to the listening queue.

**3c.**
- Listen creates half-sockets (3-tuples) as it has no concept of the remote machine
- Accept creates full sockets (5-tuples) as it receives connections and passes them to the listening queue


## 4. 

## 6. DNS Server Dependency
Most people wouldn't be able to use any online services, as it is quite rare to be familiar with the IP addresses for websites.

## 7. Mail Servers Sharing Domain Alias
These can be distinguished by different DNS record types, MX for mail exchange, A for IP resolution.

## 8. DNS UDP vs TCP
DNS using UDP instead of TCP doesn't cause a problem, because it only uses idempotent read operations - so it doesn't matter how many read requests you send, you'll always get the same result.
- If a request times out, just send another.

## 9. DNS Cache Access
You can read the DNS cache, as frequently (or recently) queried websites will be cached.

## 10. Checking Cached Domains (non-admin)
You can check how long the domain resolution takes, as recently used domains will resolve instantly as they can be read from the cache.

## 11. `getaddrinfo` Resolution Speed
It'll execute faster because it'll likely retrieve a cached value.

## 12. DNS Socket IP
The IP addresses of root servers is hard-coded into devices.

## 14. Email Auto-response
This auto-responder system would be located in a message transfer agent, as it will always be online (whereas the user receiver agent might not be)

## 15. SMTP Improvements
We would consider a better text encoding than plain ASCII (e.g. UTF-8), also the ability to transfer binary data (e.g. images, files, videos)

We could also reduce the number of exchanges made between client and server

## 16. SMTP vs IMAP (Push vs Pull)
A push protocol means the exchange is initiated by the sender

A pull protocol means the exchange is initiated by the receiver
- The user receiver agent requests (pulls) mail from the message transfer agent mailbox





