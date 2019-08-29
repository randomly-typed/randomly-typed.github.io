---
layout: "post_1"
title:  "10 - Prefix Scans"
date:   2019-07-23 -0400
categories: podcast
anchor: https://anchor.fm/randomly-typed/embed/episodes/10---Prefix-Scans-e4neb6
description: "We look at the prefix scan algorithm for the sum operation, and discover how it can be parallelized in a relatively simple but unintuitive way."
---

Input: array of integers
Output: array of integers, representing all partial sums of the elements in the input array

Useful for different sorting algorithms and in a variety of contexts, and scan in fp languages (like fold but with tracing, works for any binary operation, but lets keep it to just sums today)

## Example:
`[1,2,3,4,5,6]` # it doesn’t have to be sorted, btu it probably makes things easier for an audio podcast

Inclusive prefix scan:
`[1,3,6,10,15,21]`

Exclusive prefix scan:
`[0,1,3,6,10,15]`

How would you accomplish this? General algorithm:

Iterate through the input array by index
Take the value of the current and previous element, place in output array

---

Do you think this is parallelizable? Why or why not? (at any points, involves computing all previous elements)

There are tons of parallel algorithms, some more appropriate than other depending on the sort of parallelization we have (shared memory on single computer, GPUs, distributed message passing). Podcast episode on some of this incoming. Here is one:

Divide input array into static chunks (let’s say three).
`[1,2][3,4][5,6]`.
Have 3 worker threads calculate the inclusive prefix scan.
`[1,3][3,7][5,11]`
Collect results in coordinator
`[3,7,11]`
Calculate exclusive prefix scan in coordinator. This is the offset we need to add in each thread
`[0,3,10]`
Have each worker thread apply offset
`[1,3][3,7][5,11] → [1,3][6,10][15,21]`
Collect result in coordinator
`[1,3,6,10,15,21]`

---

Let’s say we get a stream of the input array instead. Is there a better way? Fenwick tree:
