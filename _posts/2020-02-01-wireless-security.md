---
layout: "post_1"
title:  "24 - Protocols Over The Air, Used And Abused"
date:   2020-02-01 -0400
categories: podcast
anchor: "https://anchor.fm/randomly-typed/embed/episodes/24---Protocols-Over-The-Air--Used-And-Abused-eads92"
description: "On this episode, Lance and JS discuss the evolution of wireless car unlocking technologies. We talk about some different type of attacks and how they were countered."
permalink: /24.html
---

# Old radio fobs <span class="footnote"></span>
## Garage door
Just send a specific signal.
Problems?
Replay attacks
## One way communication rolling code
More ingenious.
Fob contains a seeded pseudo random number generator.
The car contains the same RNG with the same seed.
Every time pressed, send a random number and save a counter
Protects vs replay attack
What if you press but the car is too far?
Test a window
Can get out of sync -> go to car dealership to reset

### Attack
Known attack, but Samy Kamkar was the first to demonstrate it. It was at defcon 23.
Place a device between near the car
Capture a code and jam the signal to prevent the car from receiving it
When the button is pressed a second time, capture it again, jam, send first code and save second code for future usage.

### Breaking the RNG <span class="footnote"></span>
A paper presented at usenix 2016, talks about many car fob vulnerabilities. The Hitag2 rolling code system was used by many different car brands. They were able to reverse engineer the protocol and exploit it. By eavesdropping on 4 to 8 communications plus 1 minute of computing, they were able to extract the cryptographic keys.

# Keyless
Don’t need to press anything. Does it automatically. Many new systems use public cryptography to secure communications.

## Relay attack <span class="footnote"></span> <span class="footnote"></span>
2 devices. 1 close to the house trying to get the signal from the fob.
Transmit it to another device close to the car.
### Protection
Hypothetical, ping the fob every X second. This means that when the criminals try to leave the house the car would stop working. Not sure if it’s legal...
Radio waves travel at the speed of light. This can be used to know how far is actually the fob.

## VW <span class="footnote"></span>
VW has been using public crypto since 1995, but most of their cars were using a small number of private keys. The 2016 usenix paper talked about reverse engineering the cars to extract those keys. Once they had the keys, they could eavesdrop on any car unlocking and extract enough data to clone the fob.

# RFID <span class="footnote"></span>
Many transportation cards and security fobs to enter building uses RFID (Radio-frequency identification). It’s a communication standard. Many of those security devices use Mifare Classic, over 13.56 MHz. This signal should travel between 10cm to 1 meter.

## Mifare classic <span class="footnote"></span>
Contains really limited compute power. Contains multiple memory sectors that are protected by 2 different keys. The encryption has long been compromised. For this reason, it’s really easy to clone or change any value on those cards.

<span class="footnotes">
  <a href="https://en.wikipedia.org/wiki/Remote_keyless_system">[1] https://en.wikipedia.org/wiki/Remote_keyless_system </a> <br/>
  <a href="https://www.usenix.org/system/files/conference/usenixsecurity16/sec16_paper_garcia.pdf">[2] https://www.usenix.org/system/files/conference/usenixsecurity16/sec16_paper_garcia.pdf </a> <br/>
  <a href="https://mashable.com/2017/11/28/protect-your-car-wireless-relay-attack/">[3] https://mashable.com/2017/11/28/protect-your-car-wireless-relay-attack/ </a> <br/>
  <a href="https://www.comparitech.com/blog/information-security/what-is-relay-attack/">[4] https://www.comparitech.com/blog/information-security/what-is-relay-attack/ </a> <br/>
  <a href="https://www.usenix.org/system/files/conference/usenixsecurity16/sec16_paper_garcia.pdf">[5] https://www.usenix.org/system/files/conference/usenixsecurity16/sec16_paper_garcia.pdf </a> <br/>
  <a href="https://en.wikipedia.org/wiki/Radio-frequency_identification">[6] https://en.wikipedia.org/wiki/Radio-frequency_identification </a> <br/>
  <a href="https://en.wikipedia.org/wiki/MIFARE">[7] https://en.wikipedia.org/wiki/MIFARE </a> <br/>
</span>
