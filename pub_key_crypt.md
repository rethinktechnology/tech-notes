# Public Key Cryptography

worldofprasanna - Thoughtworks guy took the session

concepts
--------
- symmetric 
  - AES 128, 192, 256 bit
- asymmetric
  - RSA 1024, 2048, 4096 bit
- key can be obtained from private -> public but not vice versa
- only one combination of pub/priv bsaed on math

**Digital Signature**
```
                        public key
  1) encrypted message - - - - - - -> Hash value
 
                 private key
  2) Hash value - - - - - - - > encrypted message 
```
- drawback: 1 GB data + 1 GB signature
- SHA2 -> 512 bit output
- Certificate Authority

tools
-----
Caddy
 - alt ngnix
 - Go lamp server

sites
-----
- https://slides.com/worldofprasanna
- https://github.com/worldofprasanna
- https://github.com/worldofprasanna/everyday-cryptography-hackerearth
- https://godoc.org/golang.org/x/tools/present
- http://worldofprasanna.in

keywords
--------
PEM
mkcert
jwt.io
keychainAccess
AES 256
CBC
base 64 encoding

SSL
---
3 phases
 - client hello
 - server hello
 - key exchange

