
# Message Integrity
- Verify that a message was not tampered with

Two approaches:
- **Message Authentication Code (MAC)**
- **Digital Signatures**

## Cryptographic Hashing

A *cryptographic* hash function differs from a *plain old* hash function due to the properties:
- Collision resistance
	- Hard to find $H(m) = H(m')$
- One-way:
	- Given $H(m)$, hard to find $m$

Example functions include 
- SHA-2
- SHA-3
- bcrypt
- argon2


## Message Authentication Code (MAC)
Used to verify integrity
Requires a shared secret key (symmetric cryptography)

A MAC function:
- Generates a tag $t$ given a message and a secret key
	- $t = mac(m, K_s)$
- Is typically a cryptographic hash function that takes as input *the secret key* and *the message* concatenated somehow

### MAC Message Exchange Protocol
Alice ad Bob have a shared secret key $K_s$ and want to verify the integrity of the messages they exchange:
1. Alice generates a message $m$ she wants to share
2. Alice generates a tag $t=mac(m, K_s)$
3. Alice send $m$ and $t$ to Bob
4. Bob calculates $t' = mac(m, K_s)$
5. Bob verifies $t'=t$. If the tags match, $m$ has not been tampered with.

An adversary *cannot* forge the tag of a message without knowledge of the key

>[!note]
>The message is sent in plaintext, and does not ensure confidentiality


## Digital Signatures

**Asymmetric Cryptography:**
- A private signing key
- A public verification key

Signature algorithm
- Produce a signature for a message using the signing key
- $s = sign(m, K_{sign})$

Verification algorithm
- Verify a signature given the *verification key*, the signature and the original message
- $verify(m, s, K_{ver})$

Provide integrity and non-repudiation (signer cannot deny signing the document)
If Bob signed a message and verification is successful:
- The message must have been signed using Bob's private signing key
- Only Bob has acces

>[!example] Digital Signature Protocol
>If Bob wants to verify a message was sent by Alice and that it wasn't tampered with. Bob has access to Alice's public verification key
>1. Alice generates a signature for message $m,s=sign(m, K^A_{sign})$
>2. Alice send $m$ and $s$ to Bob
>3. Bob accepts the message only if $\text{verify}(m, s, K^A_{ver})$ succeeds

For large messages:
- Generate the hash digest of the message
- Sign and verify the *hash* instead of just the message

# Authenticated Encryption
Provides confidentiality and integrity of messages

**Approach**: encrypt then MAC

>[!Example] Encrypt then MAC Protocol
>1. Alice generates $c = \text{encrypt}(m, K^{enc}_{secret})$
>2. Alice generates a tag for $c$, $t = \text{mac}(c, K^{mac}_{secret})$
>3. Alice send $c$ and $t$ to Bob
>4. Bob generates the tag for $c$, $t' = \text{mac}(c, K^{mac}_{secret})$
>5. If $t = t'$ then $m = \text{decrypt}(c, K^{dec}_{secret})$

Encrypt then MAC is a symmetric cryptosystem, it relies on shared keys being securely exchanged
- Shared secret key
- Shared MAC key


How can the recipient of the keys (when the initial exchange is performed) be sure they have the correct public key?

## Certificates
Digital certificates securely associate identities with cryptographic public keys

A digital certificate is a signature binding together:
- Identity of principal
- Public key of that principal

Given a certificate *issuer* with a key pair ($K^{issuer}_{public}, K^{issuer}_{private}$), a principal's identity (Bob), and their public key:
- $\text{binding} = (Bob, K^{Bob}_{public})$
- $\text{signature} = \text{sign}(\text{binding}, K^{issuer}_{private})$

We now have a certificate:
- $\text{certificate}(Bob, issuer) = (\text{binding}, \text{signature})$
The Issuer is certifying that $K^{Bob}_{public}$ belongs to Bob


>[!Example] Certificate Protocol
>1. Bob creates a message $m$
>2. Bob signs the message $s_m = sign(m, K^{Bob}_{private})$
>3. Bob send $m, s, \text{certificate}(Bob, issuer)$ to Alice
>4. Alice verifies the certificate by:
>	a. Verifying the certificate's signature: $verify(binding, signature, K^{issuer}_{public})$
>	b. Verifying that the identity in *binding* corresponds to Bob's identity
>5. If verification is successful, Alice retrieves $K^{Bob}_{public}$ from certificate
>6. Accept if $\text{verify}(m, s_m, K^{Bob}_{public})$ succeeds

**Issue**:
- We need to verify the integrity of $K^{issuer}_{public}$

### Certificate Authorities

Certificate authorities are entities that are explicitly trusted

Sign certificates for others

Their public keys are contained in *root certificates* that are self-signed

