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


### CMD 

- Encrypt the "file" with "aes-128-cbc" algorithm and put the result in "file.enc"
```ubuntu
openssl enc -aes-128-cbc -in file -out file.enc

// Apply the algoritm 2 times

openssl enc -aes-128-cbc -iter 2 -in file -out file.enc
```

- Decrypt 
```
openssl ecn -d -aes-128-cbc -in file.enc -out filerestored

openssl ecn -d -aes-128-cbc  -iter 2 -in file.enc -out filerestored
```

- Generate RSA Key: 

```
openssl genrsa -out mykey 2048

```
- Generate RSA params: 

```
openssl rsa -in mykey -text -noout 
```

-noout : print the output in the terminal 

- Generate a public key from a private key 

```
openssl rsa -in mykey -pubout -out pub 
```

- Private Key Encryption :
**des** : algorithm
```
openssl rsa -in mykey -des -out mykey.enc 
```
-  Encrypt with public key 
```
openssl rsault -encrypt -pubin -inkey PUB -in file -out file.enc 
```
- Decrypt 
```
openssl rsautl -decrypt -inkey mykey.enc -in file -out rsa.enc 
```

### Signature 

- Sign with the private key 
```
openssl rsault -sign -inkey myKey.enc -in file -out fileRSA.sign 
```

- Verify signature 
```
openssl rsault -verify -pubin -inkey PUB -in fileRSA.sign
```

- Encrypt + Sign 

```
openssl dgst -sha256 -verify PUB -signature fileHashSign file 
```

### Certificate 

Digital Certificates are verifiable small data files that contain identity credentials to help websites, people, and devices represent their authentic online identity.


An SSL Certificate is a popular type of Digital Certificate that binds the ownership details of a web server to cryptographic keys. These keys are used in the SSL/TLS protocol to activate a secure session between a browser and the web server hosting the SSL Certificate.

