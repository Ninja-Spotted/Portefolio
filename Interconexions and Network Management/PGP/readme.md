---
title: "PGP"
parent: Interconexions and Network Management
permalink: "/interconexions_network_management/pgp"
layout: default
---

### PGP (Pretty Good Privacy)

It combines the best cryptographic algorithms tto achieve secure e-mail comunication.

PGP applies compression after signing and before encryption.

#### Symmetric Keys

Same key used in encryption and Decryption. If A wants to send encrypted messages to B, they must have the same key (so one of them must send it unencrypted to the other **not safe**).


##### AES (Advanced Encryption Standard)

Symetric keys using the Rijndael algorithm.

#### Asymmetric Encryption

Two related keys (one private key known only to the individual and a public key available to anyone). It implements confidentiality by enciphering using public key and deciphering using private key and interity/authentication using private key to encipher and public to decipher.

Private keys must be infeasible to derive from public keys. 

##### RSA

Best known & widely used public-key scheme.

#### Direct Digital Signature

- Encrypt-Sign: Signatures can be easily replaced
- Sign-Encrypt: Recipient knows who wrote the message but not who encrypted it
