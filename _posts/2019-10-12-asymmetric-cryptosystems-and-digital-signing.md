---
layout: "post_1"
title:  "16 - Asymmetric Cryptosystems and Digital Signing"
date:   2019-10-12 -0400
categories: podcast
anchor: "https://anchor.fm/randomly-typed/embed/episodes/16---Asymmetric-cryptosystems-and-digital-signing-e6p9ae/a-ap0q00"
description: "JS and Lance continue their cryptography explorations by working through an example of RSA, an asymmetric cryptosystem, while discovering its surprising relationship to the concept of digital signatures."
---

## Asymmetric Cryptosystems
- Much slower than symmetric, but no need to share a decrypting (private) key with anyone.
- Relies on one-way trapdoor functions:  easy to encrypt, difficult to decrypt without some prior knowledge

### RSA
- Rivest-Shamir-Adleman, in 1977, one of the first asymmetric cryptosystems.
- It relies on prime factorization (an NP problem) as a one-way trapdoor function

```
Public key: (n=14, e=5)
Private key: (n=14, d=11)
Message : 2

Encryption = c = m^e (mod n) = 2^5 (mod 14) = 32 (mod 14) = 4
Decryption = c^d (mod n) = 4^11 (mod 14) = 4194304 (mod 14) = 2
```

`n`, `e` and `d` are all derived based on multiplying two random prime numbers, and factoring things so that it works with the modulus. In practice, these numbers are also totally random and really big so they are not brute-forceable.

Go read about how the keys are generated! It's miraculously cool.

### Signing

In real life, you sign a document as a proof of acknowledgement that something originates from you (not Fred, unless you are Fred). You can’t do that in the digital world since anyone could copy anyone else’s scribbles and put them onto their document.

Digital signing works by “encrypting’ a message with your _private_ key, so that you generate what seems to be gibberish, which will let others verify that “decrypting” it with your public key works and yields the original message.

```
Public key: (n=14, e=5)
Private key: (n=14, d=11)
Document I want to sign : 2

Signing = c = m^d (mod n) = 2^11 (mod 14) = 2048 (mod 14) = 4 // by happenstance!
Verification = c^e (mod n) = 4^5 (mod 14) = 1024 (mod 14) = 2
```

Since I’m the only one that has my private key and I never shared it, no one else can easily create another signature exactly like mine.

In real workloads, we should
- Hash the message:
    - Make document shorter & harder to forge by generating random signature that works for the message
- Add some padding
    - Prevents forgeries based on knowing the contents or length of the original message
