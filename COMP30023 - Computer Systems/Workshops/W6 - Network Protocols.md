
# Tutorial Questions
## Q1. Changing a Protocol Layer
Layer $k-1$ wouldn't be affected, as layers provide services to the layer above them only; layer $k+1$ would be affected.


## Q2. New Transport Protocol

**2a.** This impacts the application layer and transport layer
**2b.** You are assuming that the interface provided to the application layer (HTTP) remains the same (if no change is to be made to the application layer)
**2c.** You assume that the new application layer protocol is compatible with the current TCP transport layer protocol
**2d.** They can unilaterally decide to update both the transport and application layer protocols without interference


## Q3. Computing Overhead
Message length: $M$ bytes
Number of lower layers: $n$
Header length per layer: $h$

Total number of bytes sent = $M + nh$

Fraction = $\frac{nh}{M + nh}$

## Q4. Application Layer Protocols



