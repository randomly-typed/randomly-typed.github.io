---
layout: "post_1"
title:  "01 - The Simple Complexity Episode"
date:   2019-03-13 21:24:37 -0400
categories: podcast
anchor: https://anchor.fm/randomly-typed/embed/episodes/1-The-Simple-Complexity-Episode-e3f0om/a-abn86n
description: "An overview of computational complexity theory."
---

## What are some properties of a good algorithm?
- Low time complexity
- Low space complexity
- Memoizability
- Immutability & purity
- Concurrent / async / parallel
- General applicability (map reduce, actor model)
- “Elegant”
  - Easy to understand/teach/talk about

## Why is it interesting to formally define complexity?
- Let you compare algorithms
- Help you estimate how your system should behave in the real world

## Asymptotic analysis
- Always defined in terms of the size of the input (n), which can sometimes be unobvious (eg. multiplication)
- Informally defined as:
  - For f(n) starting at some constant n, you will never cross the upper/lower bound function as n trends towards infinity
- Omega(n): lower bound
  - Best case: in practice rarely considered:
    - It’s uncommon (eg. sorting a sorted list)
    - Often isn’t interesting when we consider scaling n
    - Could it represent our “real world” price?
- Theta(n): bounded by two functions
  - Average case: in practice rarely considered:
    - Hard to quantify unless using probabilistic or randomized algorithms
    - Often the average case is very close to the worst case
- O(n): Upper bound
  - Worst case: often considered
    - More interesting to analyze as n gets larger
    - Happens more often than we would think (Searching a list for an element that doesn’t exist)
- Keep in mind that algorithmic complexity is defined in the context of what current computers can do. If processors had a SUM or SORT instruction, we’d count things differently
- Since these are just regular functions, they exhibit cool mathematical properties too, like reflexivity and transitivity!

## How do I calculate this?
- Go through every statement of your algorithm, calculate how long that operation takes (in terms of n). Ignore all constant factors.
- Once done, add everything up to get a polynomial function. BE CAREFUL OF NESTING THINGS
- Note: This works for non-recursive algorithms. Recursive ones have their own way of calculating it and we should totally make a separate episode about it, there’s some cool shiet here!

## A different kind of complexity: Kolmogorov complexity!
- Aka. algorithmic entropy
- The length of the shortest computer program needed to produce a specific output.
- Example time!
- TIL: Calculating the lower bound for finding the algorithm to describe the kolmogorov complexity is impossible

## Gotcha
- Sometimes, comparing asymptotic growth won’t cover the whole story. <span class="footnote"></span>
  - On an infinitely large data set, a linear algorithm `(f(n) = n + p)` should always be better than a quadratic one `(g(n) = n^2 + q)`, but in medium sized data set, the quadratic algorithm could be faster.
    - q could be much smaller than p

<span class="footnotes">
  <a href="http://www.cs.cornell.edu/courses/cs312/2004fa/lectures/lecture16.htm">[1] http://www.cs.cornell.edu/courses/cs312/2004fa/lectures/lecture16.htm</a>
</span>
