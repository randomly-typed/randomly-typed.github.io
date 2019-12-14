---
layout: "post_1"
title:  "18 - The Halting Problem"
date:   2019-11-09 -0400
categories: podcast
anchor: "https://anchor.fm/randomly-typed/embed/episodes/18---The-Halting-Problem-e8mu7k"
description: "We travel back in time to the 1930s to discuss the mathematical landscape which lead to The Halting problem and how a machine constructed as a mental model for a proof defined modern computers."
permalink: /18.html
---

How easy would it be to write a program that takes a string

# Trivial examples
```
def main(input):
  return true
```
Not too complicated. Basic static analysis can do it.

```
def main(input):
  while(true): print(1)
  return false
```
This one is trivial to prove that it will never halt.
Modern code linters could even warn you that this function will never return.

But there’s more complex examples
```
def main(input):
  main(input)
```
Pretty much the same example, but with recursion.


# Halting problem <span class="footnote"></span>
> the halting problem is the problem of determining, from a description of an arbitrary computer program and an input, whether the program will finish running, or continue to run forever.

# HISTORY
1900: David Hilbert had some fundamental questions about peano arithmatic, upon which most of mathematics depended:
Was mathematics complete? (ie. every true statement can be represented within that system)
Was mathematics consistent? (ie. there are no contradications)
Was mathematics decideable? (ie. theorem are provable in a finite amount of time)

Today we’re dealing with 3. Next episode, we’ll deal with 1 and 2.

Alfonso Church published the first proof of undecideability of first-order logic a year before Alan Turing did, and in a completely different way, but Turing’s proof is more widely known because of the unique way he solved it. It was later determined that both systems express the same “computing power”.
Why can’t you just wait until the program halts?

> Alan Turing proved in 1936 that a general algorithm to solve the halting problem for all possible program-input pairs cannot exist

To do this proof, Alan Turing created a mathematical definition of a computer and a program. This is now known as the Turing machine, which is the conceptual basis for all modern computers.

# Turing’s proof
Alan Turing proof was a proof by contradiction. Let’s say we have a function `f(g)` that returns if `g` halts.
```
def h():
  if f(h):
    while(true)
```
This is impossible. In the if, if `f(h)` returns true (so the program will halt), it calls `while(true)` which will prevent the program from ever halting. And same for the inverse. If `f(h)` returns false (because the program will never halt), the program will halt.

Conclusion: There is a fundamental limitation to the power and expressibility of computing, and therefore logic.

<span class="footnotes">
  <a href="https://en.wikipedia.org/wiki/Halting_problem">[1] https://en.wikipedia.org/wiki/Halting_problem</a> <br/>
</span>
