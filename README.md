# Security
 - [1. Encryption](#encryption)
    - [1.1 Symmetric Encryption](#symmetric-encryption)
    - [1.2 Asymmetric Encryption](#asymmetric-encryption)
    
 - [2. Hash](#hash)

- [3. OpenSSL](#openssl)

## Encryption

### Symmetric Encryption
### Asymmetric Encryption

## Hash

## OpenSSL

### Definition 
SSL  (Secure Sockets Layer)
- Is an encryption-based protocol
- Ensure confidentiality,,Authentication and Integrity 
- the predecessor of modern TLS(Transport Layer Security) encryption in use today

=> A website that implements SSL / TLS has an “HTTPS” in its URL instead of an “HTTP”.

OpenSSL is a software library for applications that secure communications over computer networks against eavesdropping or need to identify the party at the other end.
It contains an open-source implementation of the SSL and TLS protocols. The core library, written in C programming language, implements basic cryptographic functions and provides various utility functions.

### More about openSSL

OpenSSL supports a number of different cryptographic algorithms:
Supported Ciphers
AES, Blowfish, Camella, Cacha20, Poly1305, SEED, CAST-128, DES, IDEA, RC2, RC4, RC5, Triple DES, GOST 28147–89, SM4
Cryptographic hash functions
MD5, MD4, MD2, SHA-1, SHA-2, SHA-3, RIPEMD-160, MDC-2, GOST R 34.11–94,BLAKE2, Whirlpool, SM3
Public-key cryptography
RSA, DSA, Diffie-Hellman key exchange, Elliptic curve, X25519, Ed25519, Ed448, GOST R 34.10–2001, SM2
Certificates
X.509V3 ( encoding/decoding ASN1 and PEM )

### CMD 


encrypt the "file" with "aes-128-cbc" algorithm and put the result in "h1"
```
openssl enc -aes-128-cbc -in file -out h1

// Apply the algoritm 2 times
openssl enc -aes-128-cbc -iter 2 -in file -out h1
```
