---
layout: "post_1"
title:  "33 - Two Generals' Problem"
date:   2020-12-07
categories: podcast
anchor: "https://anchor.fm/randomly-typed/embed/episodes/33---Two-Generals-Problem-endt8b"
description: "Lance and JS talk about the Two Generals' Problem and try to understand its real impacts on networked systems."
permalink: /33.html
---
# Two Generals Problem

## Scenario

Imagine a large castle in a valley between two hills.
On each hill, there is an army for the nation of Podcastia
The castle is controlled by enemy nation
The only way for both armies to communicate is to send a messenger through the valley into enemy territory
Armies must launch a coordinated attack from both sides simultaneously if they hope to win the castle: truth table
How can both armies agree on a time to attack and be 100% certain in the time?

### No shared knowledge
1 -> 2 = okay, ack by 2
1 <- 2 = never arrives

From perspective of 1, it’s equivalent to simply:
1 -> 2 = ok

Unaware of whether 2 actually received the message, but whether they received it could influence the attack’s success

### Attempt to find a strategy with a guaranteed win

Given constraints: a general can either commit to:
Always attack without confirmation:
can never guarantee it will work because messenger could get lost
Always wait for an ack to attack:
Now general 2 is in same position as general 1, must attack without confirmation


This is an unsolvable problem with the current constraints.

# Mitigations:

Give up! Accept that the communications channel is untrusted and no shared knowledge can ever occur.
Send lots of messengers, lots of acks:
Increases probability of success but will never _guarantee_ it
Make assumption about the time it takes for a messenge to got though:
Absence of messengers increases probability
Use idempotency key: not available in every situation
May not be possible to retry, or get back into a safe state
