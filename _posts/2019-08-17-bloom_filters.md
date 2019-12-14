---
layout: "post_1"
title:  "12 - Bloom filters"
date:   2019-08-17 -0400
categories: podcast
anchor: "https://anchor.fm/randomly-typed/embed/episodes/12---Bloom-filters-e50gua"
description: "We talk about Bloom filters, a probabilistic data structure for set membership queries, how they work, and what all the fuss is about."
permalink: /12.html
---

Scenario: email as a username as a service.

What would be a good data structure for this? Array? Hashmap? Bloom filter?

## Bloom filters:
- Probabilistic: can only reason about it’s characteristics with some degree of probability
- False positives possible, but not false negatives: definitely not in set, probably in set.

## Traditional operations:
- Insert
- Exists?

## Algorithm:
- Initialization: a bit array, & A few hash functions. The size of bits and number of hash functions varies on a few factors (false positive rate desired, number of elements expected to be stored)
- Add an element: hash the element with all your hash functions, get a number for each one. Set the bit for each hash output to one.
- Query for an element: hash the element with all your hash functions, get a number for each one. Check the bit at each of these values. If any of these bits are not set, it is definitely not in the set. If all are 1, then either the element is in the set, or all those bits of been set to 1 previously through hash collisions: false positive.
- more hash functions requires more space but reduces the probability of collision since a match need to match the output of all hash outputs

## Hacks:
- Instead of using many hash functions, use a good hash function with wide evenly-distributed output and slice it into multiple fields.
- Hash multiple times with the same hash instead of choosing multiple different ones.

## Removal:
- Is removal possible with the traditional bloom filter? Why? Unsetting a bit may remove a bit which multiple input value hashed to, which would introduce a false negative.

## Analysis:
- Compared to other ways for testing for set membership, Bloom filters are awesome because they don’t need to store any data about each input individually (Tries are a little bit like this too).
- Array will be faster for small number of items
- Hash maps are slower in they store the value, which means they be placed in a linked list in a bucket which takes space and may take time to traverse through.
- Really nice for parallelization for both insertion and looking up.
- Adding an element never fills up the data structure, only increase the probability of collision.
- Two bloom filters can be intersections / unioned with they have the same hash functions and the same bit array, but it affects the false positive rate.

## Uses:
- Increased cache efficiency by detecting whether a resource has only been requested once.
- Significantly reduce database calls for rows we know are non-existent
- Anytime we have a finite set of things and want to quickly determine whether a new thing is in that set.

## Supporting deletion:
- How?
- What’s the downside?

## So many variations since its inception in 1970:
- Scalable bloom filter: ability to grow dynamically to number of elements being stored to maintain a certain false positive rate. Works by having sequences of ordinary bloom filters, with increasing capacity and thus smaller false positive probability, so we can maintain that the series of probability is below a certain threshold.
- Stable bloom filter: For use with infinite streams of data that aren’t being stored anywhere. Stale elements are being evicted for more recent ones like a cache. As soon as eviction happens, false negatives begin to appear.

## Similar data structure:
- Quotient filter. Same thing but allows for merging without changing the false positive rate. Apparently slightly faster but consumes slightly more memory because it only requires a single hash function
- Cuckoo filter: uses a different hasing scheme and uses a hash table under the hoode. Apparently, better data locailty, less space and faster lookups  & ability delete elements as a separate data structure
