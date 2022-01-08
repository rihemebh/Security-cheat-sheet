# Security
- [0. Before we start](#before-we-start)
- [1. Encryption](#encryption)
    - [1.1 Symmetric Encryption](#symmetric-encryption)
    - [1.2 Asymmetric Encryption](#asymmetric-encryption)
      - [1.2.0 Needham-Schroeder](#needham-schroeder)
      - [1.2.1 RSA](#rsa)
      - [1.2.2 Diffie Hellman (DH)](#dh)
      - [1.2.3 ELGamal](#elgamal)
    
- [2. Hash](#hash)
- [3. OpenSSL](#openssl)
## Before we start 
### Some important notions
|name|description|
|---|---|
|Identification|Who are you ?|
|Authentication|Prove it|
|Authorization|Do you have the right to do something ?|
|Audit| What did you do ?|
|FootPrint|Recognition|
|Integrity|Ensuring that information cannot be changed|
|Confidentiality|Ensuring that information can be accessed (read) only by authorized persons|

### Attacks 
|Attack|Description|Example|
|---|---|---|
|Birthday Attack|It is made against the Hash algorithms. (Belongs to a class of brute force)  <br/> All hashed messages have a fixed length (independent from the input length) and they unique for that message. this attack refers to the probability of finding two random messages m1 and m2 that has the same Hash h(m1) = h(m2) so the attacker can safely replace the message by his own one|What is the relation with the birthday: <br/> Since we have a finite number of days in one year (365) there is a big chance to have 2 persons with the same birthday in a finite number of persons.|
|Password attack|Trying to guess the password or having a databse of passwords called dictionnary|- **Brute Force** : using a random approach by trying different passwords and hoping that one work Some logic can be applied by trying passwords related to the person’s name, job title, hobbies or similar items. <br/> - **Dictionary attack**: dictionary of common passwords is used to attempt to gain access to a user’s computer and network. One approach is to copy an encrypted file that contains the passwords, apply the same encryption to a dictionary of commonly used passwords, and compare the results.|
|Man in the middle|occurs when a hacker inserts itself between the communications of a client and a server|Session hijacking <br/> <img src="https://github.com/rihemebh/Security-cheat-sheet/blob/main/mitm%201.PNG" /> <br/> <img src="https://github.com/rihemebh/Security-cheat-sheet/blob/main/mitm%202.PNG" />|
|SQL Injection|SQL commands are inserted into data-plane input (for example, instead of the login or password) in order to run predefined SQL commands|“SELECT * FROM users WHERE account = ‘’ or ‘1’ = ‘1’;”<br/> Because ‘1’ = ‘1’ always evaluates to TRUE, the database will return the data for all users instead of just a single user.|
|Cross-site scripting (XSS)|Use third-party web resources to run scripts in the victim’s web browser or scriptable application|<img src="https://github.com/rihemebh/Security-cheat-sheet/blob/main/xss.PNG"  />| 



### Frequently used CMDs
``gpg`` :  is the cmd for encryption 
- Get Hostname 
```
hostname -I
```
- Connect remotely
```
ssh <username>@<hostname>
```
- Secure copy : 
```
scp <filename> <username>@<hostname>:<path>
```

## Encryption
Encryption is used to garantee Confidentiality 

### Symmetric Encryption
Use one shared encryption key between sender and receiver 
- Encrypt the file : 
   - Binary format (default)
     ```
     gpg -c <filename>
     ```
   - ASCII format 
     ```
     gpg -c --armor(or -a) <filename>
     ```
- Get all the algos 
```
 gpg --version 
```
Examples of symmetric algorithms: <br/>
AES (Advanced Encryption Standard), DES (Data Encryption Standard), IDEA (International Data Encryption Algorithm),RC4/5/6 (Rivest Cipher 4/5/6)

- Encrypt the file and specify the algo (cipher)
```
gpg -c -a --cipher-algo <filename>
```
- Decrypt 
```
gpg -d <filename>
```

|Advantages ++ |Disadvantages -- |
|---|---|
|Fast|non secure key|
|-|Large number of keys|
|-|Without signature|

### Asymmetric Encryption
Use public keys for encryption and private keys for decryption <br/>

- Generate Keys 
```
gpg --full-generate-key
gpg --gen-key
```

- Get the Key List 
```
gpg --list -keys
```

|Advantages ++ |Disadvantages -- |
|---|---|
|Secured|Slow|
|Signature||
|Less number of keys||


#### Needham-Schroeder
Authentication Protocole 

#### RSA
NP-complete problem
#### DH
DLP : Discrete logarithm problem 

- Problem ? 

#### ELGamal
DLP : Discrete logarithm problem 


## Hash
Hash is used to garantee Integrity : We use non-bijective functions to hash the message 

Examples of Hash functions : 
- sha, sha256, md5 


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

- Digital Certificates are verifiable small data files that contain identity credentials to help websites, people, and devices represent their authentic online identity.
- Digital certificates cover three main uses: 
     - Authentication: used to validate the identity of issuers as part of an authentication process, a crucial element of computer network security.
     - Signing: sed to sign a document or a file and to guarantee its integrity
     - Encryption: Garantee the security and integrity of information exchanged between a website and a browser, by means of a cryptographic key enabling a secure session to be activated (HTTPS protocol)

- Certification Authority issues digital certificates

----------------------------------------------------------------------------

- Get the Certification of the www.google.com website: 
```
openssl s_client www.google.com:443
```

- Get the authority of a certification : 
<br/> google.cert is the file that contains google certification : output of the above cmd
```
openssl x509 -in google.cert -subject -issuer -noout
```
=> google trust

----------------------------------------------------------------------------


Goal:
- Create a certification authority called "**INSAT**"
- Create a certification for INSAT
- **GL4** will ask a certification from **INSAT** 
- **INSAT** will verify this request and generate a certificate 
- Now **INSAT** is the authority of **GL4**

----------------------------------------------------------------------------

- Create RSA keys for INSAT and put it in INSAT.key 
```
openssl genrsa -des3 -out INSAT.key 3072
```

- Create a certification for INSAT
```
openssl req -new -x509 -days 730 -key INSAT.key -out INSAT.cert
```
=> In this certificate INSAT is the subject and issuer : **Self Signed Certificate**

- Create keys for GL4
```
openssl genrsa -des3 -out gl4.key 3072
```
- Create request for a certiif from INSAT 
```
openssl req -new  -key gl4.key -out gl4.req 
```
- Generate a Certificate for GL4: 
```
openssl x509 -req -in gl4.req -out gl4.cert -CA INSAT.cert -CAKey INSAT.key -CAcreateserial -CAserial gl4.srl
```
- Send the request 
```
openssl x509 -req -in gl4.dem out gl4.cert -CA INSAT.cert -CAkey INSAT.key -CAcreateserial -gl4.srl
```
- Export the certificate 
```
openssl pkcs12 -export -out gl4.pfx -in gl4.cert -inkey gl4.key -name "certificat de gl4"
```
=> pkcs12 : put the certificate and the keys in the same file "gl4.pfx" so you can import it in the browser

- Import it

|preference -> certificate manager -> my Certificates -> import |
|---|

- Add Authority

| preference -> certificate manager -> Authorities -> import -> choose INSAT.cert |
|---|


