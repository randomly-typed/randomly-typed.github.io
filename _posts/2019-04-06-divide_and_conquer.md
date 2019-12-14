---
layout: post_1
title: 03 - Divide and Conquer
date: 2019-04-06 -0400
categories: podcast
anchor: https://anchor.fm/randomly-typed/embed/episodes/Divide-and-Conquer-e3ll9h/a-acqg7c
description: "In this episode, we discuss divide and conquer algorithms like merge sort, and see why it's more challenging to analyze their complexity."
permalink: /3.html
---

## Divide-and Conquer:
often then in recursive algorithms. They break down the problem into similar subproblems recursively until you hit a trivial base case, and then combine the results.

3 steps:
- Divide the problem by breaking it into smaller subsets
- Conquer the subproblem by solving it recursively or just solving the trivial base case
- Combine the result of the subproblem

## Merge sort:
A relatively performant sorting algorithm.
- Input: an unsorted array of things
- Output: a sorted array of things
- Let’s assume we’re dealing with integers for this problems


- Divide: take the array you’re given. Split it in two halfs.
- Conquer: Call merge sort on each half and trust that you’ll get back two sorted but separate arrays.
  - Recurring theme in divide and conquer algorithms. You have to “trust” that your algorithm will “just work”, until you deal with the base deal, then you know it’ll work.
- Combine: use a “merge” function which takes two sorted arrays and gives you back one sorted array

Merge is a separate function. It is `O(n)`. Let’s say you have two piles of face-up, sorted cards on the table. You need to sort them. How did you do it? Did you need to look at all cards more than once?

Back to merge sort. Divide into two, merge sort each half, then merge. We know how to divide and merge now. We can trust that mergesort will work for larger cases if we can show it works for the base case. What’s the base case for merge sort? Merge sorting an array of 1 element!  So if merge works for 1 card, 2 cards, 3 cards, it’ll work for any number of cards, and merge sort by association will work for any number of cards.

Divide and conquer algorithms tend to them themselves well to parallelism. The divide step usually involves two distinct subsets of data operated on independently.

---

Now that we know how it works, let’s analyze the running time of merge sort

- Divide the input into two: `O(1)`
- Mergesort on the left half: `O(???)`
- Mergesort on the right half: `O(???)`
- Merge the two halves: `O(n)`

So we know that it’s currently bounded by `O(n)`, it can’t possibly be faster than that.

Similarly to how we use recursion to solve the problem, it’s only natural that we can use recursion to describe the running time too.

Think of the merge sort problem as a tree. At the root, we have the entire input array as the data set. Every node represents calling the merge sort function on an input of a particular size. Then, we sum the cost of each level or depth of the tree, then figure out how deep the tree goes relative to the input size.

Because it takes `O(n)` time to merge the two subarrays into the final output array., let’s say that for this call to merge sort, (excluding the recursive calls because we’ll analyze those on their own), it takes `T(n)` complexity. The `T(n)` analysis is called a recurrence, and its where we describe the complexity of a function based on calling it on smaller inputs.

Now let’s look how long it would take to do a merge operation twice, once for the first two quarters of the input array to form the sorted first half, and once for the last two quarters of the input array to form the sorted second half. We have the solve the problem twice, so it maight be tempting to say that the complexity of this is `2 T(n)`. But n is supposed to represent our input size, and each of the merge sorts had half the original input amount. So this “depth” of recursive calls would be `2T(n/2)`. But you can see at least in this example that if you run merge twice but on two halves, it’s equivalent to just running merge sort once on the entire input

Now we know that every time you recurse down a level into the tree, it’ll take a total of `O(n)` time complexity to solve for the merge. All that’s left is figuring out how many time we’ll need to recurse through the input. Since we divide our input set in half every time mergesort is called, we’re recursing through it `log2(n)` times. So in the end, all we have to do is `O(n) * O(log n) == O(n log n)`.

This sort of analysis is using something called a recursion tree. Not every problem ends up being simple (where every level is just `O(n)`), but it can always be described by some sort of equation.

The master method is  a special shortcut you can take. If after the analysis of your first run of your function, you end up with a relation which looks like: `aT(n/b) + f(n)`. Remember that `aT(n/b)` represents the cost of dividing a problem of size n into a subproblems, each of size n/b, and `f(n)` represents the arbitrary amount of work required to divide and combine the subproblems back into a meaningful result.

There’s a rigorous proof here which can’t go into because of audio format, but intuitively, what it means is that if `f(n) >> aT(n/b)` for some constant you define/care about, then the complexity is `f(n)`. The inverse is true, where if `f(n)` is insignificant, the recursive calls dominate the complexity and become an exponential factor of n, which depends how many times you need to recurse on smaller subproblems. And if they’re approximately equal, you can multiply the cost of the combine step `f(n)` with the logarithm of how long it takes to reduce your problem, but i’ll be `n log n`.
This part is much more complex and is especially hard to convey over audio, so take it on faith that it works, and if you don’t want to, go check it out and cry after reading all that math.
