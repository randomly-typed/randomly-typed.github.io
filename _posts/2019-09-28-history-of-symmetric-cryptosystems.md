---
layout: "post_1"
title:  "15 - History of Symmetric Cryptosystems"
date:   2019-09-28 -0400
categories: podcast
anchor: "https://anchor.fm/randomly-typed/embed/episodes/15---History-of-Symmetric-Cryptosystems-e5kuhi"
description: "JS and Lance are reunited! We go back in time to discover how the earliest cryptosystems worked and cover some ground on the basics of cryptography."
---

# Why cryptography?
- Confidentiality
- Data integrity
- Authentication of a person or message
- Nonrepudiation

# What is a cipher

cipher is an algorithm for performing encryption or decryption (https://en.wikipedia.org/wiki/Cipher)

# Quick history <span class="footnote"></span>
- transposition/shift ciphers
  - plaintext (which are commonly characters or groups of characters) are shifted according to a regular system <span class="footnote"></span>
  - (X + K) mod 26 = Y
  - Rot13
-  substitution ciphers
  - Caesar cipher
- Steganography
  - Hidden messages
  - An early example, from Greece, was a message tattooed on a slave's shaved head and concealed under the regrown hair

## Problems <span class="footnote"></span>
- Relatively small problem space == brute-forceable
- Statistical analysis
  - Frequency analysis
  - Homophonic substitution tries to reduce that by letters are mapped together. One letter can map to multiple characters. Can use n-gram analysis against that.
- Essentially all ciphers remained vulnerable to cryptanalysis using the frequency analysis technique until the development of the polyalphabetic cipher. 14th century
  - Vigenère cipher used multiple Caesar ciphers in sequence with different shift values.
  - In 1863, Friedrich Kasiski was the first to publish a successful general attack on the Vigenère cipher
  - Enigma from WWII was also using a polyalphabetic cipher

# Basics
## Symmetric
One key is used to encrypt and decrypt. Analogous to using a key with a lock. All primitive ciphers are symmetric.
Downside is you need to trust the person at the other end, and everyone managing N keys for each person they interact with = N^2 keys

### XOR (One-Time-Pad)
With all the perfect conditions, XOR is a really strong solutions. It actually provides provably perfect secrecy (ciphertext is no different from total randomness) if key is random, used only once as is as long as the message.
