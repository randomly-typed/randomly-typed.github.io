---
layout: post_1
title: 08 - Distributed Systems Introduction
date: 2019-06-22 -0400
categories: podcast
anchor: https://anchor.fm/randomly-typed/embed/episodes/8---Distributed-Systems-Introduction-e4dntb/a-ahhft4
description: "We go over the fundamentals of distributed systems and get to the bottom of buzzwords like scalability, availability and transparency."
---

## What is distributed systems?
- how systems of distinct & autonomous computing nodes interact & communicate.
- Eg. application server talking with a database, sending an HTTP request, even multiple processes through IPC

Every actor in the system is a node, just like in graph theory, and they form a network when connected.

Perhaps the biggest problem to solve in distributed computing (and is a general assumption we make) is that communication between nodes (the edges in our graph) are slow & unreliable. A great example is TCP.
- Slow: no need to serialize data, communicate it across a channel you don’t control
- Unreliable: no control over channel, may break, may arrive in wrong order
Can’t even rely on something as primitive as the CPU clock speed!

## Transparency
Distributed systems are *transparent*, in that the system as a whole can be interacted with as if it was a single system. For example, when you interact with the GitHub API, you don’t care whether some or all their servers are running on Linux or BSD. Distribution transparency is nice because it allows for us to abstract away some system properties, eg.
- Localization: When you send an HTTP request to Google, it will probably to a server geographically close us to for a faster response time, but we don’t have to know.
- Replication: We could be reading off of one of a thousand read replicas, which will provide reliability & performance, but we don’t have to know.
- Concurrency: An application server or database will serve thousand of requests simultaneously, but we don’t have to know.
- Scalability: We don’t have to know whether GitHub’s DB is sharded or not.

## Scalability
A scalable system is one that can perform as effectively as it begins to expand. Examples: more data, more users, more requests, more nodes, etc.

### The scalability dimensions:
- size: more users should mean the same performance
- geography: users further away should get the same experience
- Management: more nodes shouldn’t require more human intervention

### Some solutions:
- Scale up/vertically: Get beefier machines.
- Scale out/horizontally: Get more nodes

### A few things make scaling properly difficult:
- Achieving asynchronous communication
- Partitioning centralized information
- Replicate/Cache for read reliability & performance, but that may lead to inconsistent state (mo copies mo problems)

## Availability & Fault-Tolerance
A system is available if a user can always access it and it behaves as intended. Uptime measures this. 

What causes downtime?:
- External factors: networks
- Internal factors: our own faults

Faults are anything which may cause unexpected behaviour. A failure is a fault which has happened and is affecting the system.

Fault-tolerant systems are ones that can always handle system failures: so 100% availability. In practice this doesn’t exist as we can’t expect to prevent faults we are not even aware of.

## Want to explore CAP? <span class="footnote"></span>
### Brewer's theorem

- Consistency: Every read receives the most recent write or an error
- Availability: Every request receives a (non-error) response – without the guarantee that it contains the most recent write
- Partition tolerance: The system continues to operate despite an arbitrary number of messages being dropped (or delayed) by the network between nodes

## PACELC <span class="footnote"></span>
In theoretical computer science, the PACELC theorem is an extension to the CAP theorem. It states that in case of network partitioning (P) in a distributed computer system, one has to choose between availability (A) and consistency (C) (as per the CAP theorem), but else (E), even when the system is running normally in the absence of partitions, one has to choose between latency (L) and consistency (C).

<span class="footnotes">
  [1] https://en.wikipedia.org/wiki/CAP_theorem <br/>
  [2] https://en.wikipedia.org/wiki/PACELC_theorem <br/>
</span>
