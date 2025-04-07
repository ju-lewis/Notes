

# TLB Discussion

After a context switch occurs:
- The TLB contains mappings that are only valid for the currently running process
	- The same virtual page maps to different physical frames for different processes
- On approach is to flash the TLB on a context switch
- The newly running process will encounter many TLB misses while the TLB is re-populated with valid entries


# Secure Communication

Secure communication has the following properties:
- Confidentiality
	- Only the sender and intended receiver should be able to understand the contents of the communication
- Integrity
	- Be able to detect if the content of the communication has been tampered with
- Authentication
	- Establish identities of one or both of the endpoints to confirm that they are who they claim to be


## Cryptographic Principles
- Encryption
- Cryptographic hashing
- Message authentication codes
- Digital signatures

Modern cryptography is based on mathematics
- Problems that are considered to be computationally hard

Cryptography is not always absolute - there is no perfect security
- Always *technically* susceptible to brute force attack
- The challenge is making the brute force attack take so long as to be infeasible to perform



## Encryption

Used to provide *confidentiality*

Take a message, called the plaintext, and encrypt it into a ciphertext in such a way that only authorised parties know how to decrypt it back to plaintext.

Two functions
- $c = \text{encrypt}(m, K_e)$
- $m = \text{decrypt}(c, K_d)$

Kerchoffs' Principle:
- Secrecy should depend only on the decryption key remaining secret
- Secrecy should not depend upon the algorithm remaining secret.


### Symmetric Encryption
- Both keys are the same
- Key must remain secret
### Asymmetric Encryption
- Uses *two* different keys
- A public key to encrypt and a private key to decrypt

>[!example] Symmetric Encryption Protocol Example Description
>Alice wants to send a message to Bob.
>1. Alice and Bob securely exchange $K_s$
>2. Alice computes ciphertext $c$ by running $\text{encrypt}(m, K_s)$
>3. Alice sends $c$ to Bob
>4. Bob recovers $m$ by computing $\text{decrypt}(c, K_s)$


## Advanced Encryption Standard - AES

AES is a block cipher
- Breaks data into fixed-sized blocks and encrypts/decrypts each block

AES, and block ciphers in general, have different modes of operation
- The mode of operation determines how each bock is treated/linked
- Examples of modes of operation include:
	- ECB - Electronic Codebook
	- CBC - Cipher Block Chaining


### ECB - Electronic Codebook

Each block is encrypted and decrypted independently using $K_s$
- *Deterministic Encryption*

This approach is *not secure*!
- It leaks patterns in the plaintext


### CBC - Cipher Block Chaining

Based on probabilistic encryption
- The use of randomness during encryption so that encrypting the same plaintext results in different ciphertexts

When using CBC,  we cannot conclude that because two ciphertexts are different that the plaintexts are different

Randomness is introduced through an Initialization Vector (IV)
- Must be random and not reused
- Does not need to be secret


**Encryption**:
- First block: XOR plaintext and IV, encrypt, get ciphertext
- Other blocks: XOR previous ciphertext with plaintext, encrypt, get ciphertext

Must be done sequentially
- Encrypting block $n$ requires encrypting block $n-1$ first

**Decryption**:
- First block: decrypt ciphertext and XOR with IV, get plaintext
- Other blocks: decrypt ciphertext and XOR with previous ciphertext, get plaintext

Can be done in parallel
- No need to decrypt block $n-1$ before descrypting block $n$

>[!note]
>If a ciphertext block is lost/corrupted, it only impacts itself and the block immediately after

## Asymmetric Encryption

Also known as public key encryption
Every principal (i.e. Alice, Bob) has a pair of keys: a public and private

Example algorithms:
- RSA, ElGamal

>[!example] Protocol
>For Alice to send a message to Bob:
>1. Bob generates a key pair
>2. Bob shares his public key
>3. Alice encrypts the message $m$ using the public key
>4. Alice send $c$ to Bob
>5. Bob recovers $m$ by computing $\text{decrypt}(c, K^B_{private})$

There is no need to securely exchange any keys
Provides confidentiality provided:
- Private key is kept secret
- The public key used is Bob's correct public key

*Very computationally expensive!*

## Hybrid Encryption

We can combine these approaches by using asymmetric key encryption to share the symmetric key.
- We get the speed of symmetric key encryption with the security guarantees of asymmetric encryption

>[!example] Protocol
>Alice and Bob want to exchange messages using symmetric key encryption
>
>1. Alice generates a key pair
>2. Alice posts her public key online
>3. Bob obtains Alice's public key
>4. Bob generates a secret key $K_{secret}$
>5. Bob computes the ciphertext of the secret key (using Alice's public key)
>6. Bob shares the ciphertext with Alice
>7. Alice decrypts the ciphertext using her private key
>8. Alice and Bob can now use symmetric key encryption



