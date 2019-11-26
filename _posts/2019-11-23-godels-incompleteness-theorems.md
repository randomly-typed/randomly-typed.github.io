---
layout: "post_1"
title:  "19 - Gödel's incompleteness theorems"
date:   2019-11-23 -0400
categories: podcast
anchor: "https://anchor.fm/randomly-typed/embed/episodes/19---Gdels-incompleteness-theorems-e8vdgv"
description: "Some of the toughest problems in mathematics went unsolved for long periods of time, only for them to be proven hundreds of years later. Can anything and everything eventually be proven with the right level of ingenuity? Gödel's shocking proofs tells us that there are some statements which just aren't provable, even if they appear to be true."
---
# Previous episode
## Nix
purely functional. It has no concept of sequential steps being executed, any dependency between operations is established by depending on data from previous operations.

Strongly inspired by lambda calculus and look similar to haskell. Is Turing complete.

## Ethereum solidity
Seems to be a complete language too. Tho, there’s a concept of gaz which represents how long the script can run. If the script runs out of gaz the transaction is rollbacked but the money paid for the gaz still go to the workers.

# Gödel's incompleteness theorems <span class="footnote"></span>

## On the nature of truth
Is Fermat’s Last Theorem true?
No three positive integers a,b,c satisfy the equation a^n + b ^n = c^n where n > 2
It “seems” true, but was unproven for nearly 400 years until 1995.
Is the Goldbach conjecture true?
Every even integer can be expressed as the sum of two primes
It “seems” true (we tried to for all integers up to 4x10^18), but it still remains unproven.

For most of history, we assumed that any true statement about mathematics will have a proof if we try hard enough to find one. David Hilbert began to question this in the 1900s:
Is mathematics consistent? (ie. every true statement can be represented within that system)
Is mathematics complete? (ie. there are no contradications)
Is mathematics decideable? (ie. theorem are provable in a finite amount of time)

Today, we’ll explore 1 and 2 and how they are intertwined.

The best way to get happiness is to give happiness to others. This is a verbal paradox, but we’re fine with it. Why?

Mathematics avoids paradoxes and inconsistency by relying on axioms, which we assume are true by their very nature. From these we can prove every true statement. If ever we find that we can’t, we can adopt that as a new axiom.

This system specifically disallows inconsistency, in that if we can prove that a false statement is true, then our axioms are wrong and need to be revisited, because anything can be proven as a result: the principle of explosion.

# The proof

Godel’s proof states that all math systems must be either incomplete or inconsistent, because a consistent math system cannot prove its own consistency, which is an example of incompleteness.

Let’s assume that all statements about mathematics, whether true or false, are given their own unique number (eg. an encoding). Let’s have an axiom in our meta-system that says that something is provable if the number of a statement is divisible by all base axioms.

“This statement cannot be proved from the axioms”: this has a number.

Let’s assume it is false: “This statement is provable from the axioms”. But a provable statement must be true! Contradiction.

So now we know that since it’s not false, it _must_ be true! Then that means “This statement can’t be proved from the axioms” is true. So it’s a true statement and we know it because we proved it in the “metasystem”, but we can’t prove it from within the system.

What is something that we can see is true, but can’t proven? An axiom! We have a new system of mathematics with a new axiom, and we can repeat this process infinitely.

They’ve “extracted” this problem and applied it to our mathematical system and have shown that some known problems don’t seem to be provable.

# Practical implications

What is a type system? It’s a program (system and set of rules) about determining whether other programs (statements) are valid, and programs are just logic.

By extension, we can reason that there are some programs that while they seem true in practice, a type system could never verify that it is.

Soundness is proving the absence of errors. If a program is accepted by the type system, then it has no errors
Completeness is proving the presence of errors. If a program is rejected by the type system, then it has errors.

Since we know that no mathematical system is guaranteed to be complete, we know that no type system is guaranteed to be fully complete (or sound).

<span class="footnotes">
  <a href="https://en.wikipedia.org/wiki/G%C3%B6del%27s_incompleteness_theorems">[1] https://en.wikipedia.org/wiki/G%C3%B6del%27s_incompleteness_theorems</a> <br/>
</span>
