---
layout: "post_1"
title:  "17 - Applied Cryptography and Security"
date:   2019-10-12 -0400
categories: podcast
anchor: "https://anchor.fm/randomly-typed/embed/episodes/17---Applied-Cryptography-and-Security-e851vp"
description: "JS and Lance discuss the real-world applications and implications of cryptography with topics like key sharing, password keeping and end-to-end encryption."
---
# Usages
##  Communication (PKI / CA)
On the Internet we trust a limited set of Certificate Authorities. They validate and signs other entities that we should trust. They associate public keys with organizations we can trust
Let’sEncrypt makes getting a certificate super easy and automates most of the verifications process. Is this bad?
Revocation process involves a certificate list to no longer trust that needs ot be updated all the time

## End to End encryption
Keys are only known to the communicating parties, not by the intermediary. All encryption is done by communicating parties on their clients (unless there’s a backdoor).
There needs to be some kind of key exchange.
Code update could compromise this

## Centralized key exchange service (iMessage, whatsapp, telegram…) vs GPG, out of bound, depends who’s your adversary

### Secret sharing
Shamir secret sharing (key sharding)
Allows for a minimum threshold of keys shared among any number of people in order to decrypt the secret.
how many straight lines go through one point? infinitely many.
how many straight lines go through two points? only one.
So let your secret be 6. choose a polynomial where f(0) = 6, make the polynomial degree be one more than the required threshold, and pass out random points along the line for any interested party to receive.
Diffie-Hellman to share a symmetric key unknown to two parties in advance over a public channel. After that, use the symmetric key to be able to use faster algorithm to communicate.
There needs to be a global color (yellow)
JS and Lance each have their own secret randomly-generated colors (yellow+red=orange and yellow+blue=green).
They mix their colors with the global color to get a derived random color, which each gets sent to each other over a public unsecure channel.
Upon receiving the other’s random color, you mix your own secret color into the color you received (red + green == brown == orange + blue)
In the real world, the base color needs to be a prime, you mod by a prime p, and the other colors are  just randomly-generated ones.

## Secret keeping
### Password keeping
Hashing + Salting
Needed to protect against dictionary attacks / rainbow tables

### Reversible
Encrypted config file : asymmetric (ejson)
Full disk encryption. 2 different symmetric keys
Where does Vault fit into this?

### Two-factor
Two-factor: combination of something we know, something we have, or something we are. (eg. bank card)
SMS, time-based authy, Yubikey

### Hardware
TPM (Trusted Platform Module)?
