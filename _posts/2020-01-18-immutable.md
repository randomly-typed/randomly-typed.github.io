---
layout: "post_1"
title:  "23 - Immutable Data Structures"
date:   2020-01-18 -0400
categories: podcast
anchor: "https://anchor.fm/randomly-typed/embed/episodes/23---Immutable-Data-Structures-ea4drm"
description: "Most data structure are only useful if you can modify them. Today, JS and Lance talk about immutable data structure which don't allow for direct modification but instead encourage extension. We consider the situations in which these could be useful and how to build one from scratch."
permalink: /23.html
---

# What is it?

Immutable (or persistent) data structures are “append-only” data structures. All representations of it throughout time are kept and accessible through a specific reference.

# Partially-persistent vs Fully-persistent
Partially-persistent data structures only allow “modification” of the data structure from the most recent version. This ensures a linear ordering of events.  Fully-persistent can modify any reference but can lead to multiple branches / timelines.

# Simple examples: Singly-linked list

# Why are these useful?
- They handle concurrency very well
- Avoids full copy-on-write

# Fat Node
Storing all versions of values in the nodes themselves + having a way of differentiating the version

# Path Copying
Making new nodes representing the path to new value, while making sure all previous nodes are accessible

# Let’s build an Immutable Hash Map!

First, let’s build a regular hash/map/associative array with a trie/prefix tree

- Advantages
  - Possibly less memory consumption
    - Radix tree
    - Bust also possibly more if no radix and lots of keys and not hashing
  - More structured data
    - Not necessary to hash
    - Full text search

- Disadvantages
  - Faster lookup in the worst case but slower lookup in the average case

Now let’s make the immutable version!
