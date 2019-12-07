---
layout: "post_1"
title:  "20 - Voting Systems & The Condorcet Paradox"
date:   2019-12-08 -0400
categories: podcast
anchor: "https://anchor.fm/randomly-typed/embed/episodes/20---Voting-Systems--The-Condorcet-Paradox-e93v44"
description: "Lance and JS examine the social sciences to see what it means to have a fair voting system, and how every system we’ve come up with so far has some fatal flaws."
---
# Arrow’s Theorem

Did you vote in the latest Canadian Federal election? Do you feel that your vote mattered?

We want fairness in our electoral system in order to best represent our interests through democracy. Can we devise a system that will guarantee that we can combine everyone’s individual ranking into a total group ranking fairly?

# Ranked voting systems

The Canadian election is complicated. We have ridings, with different number of people in them based on their location, so we prefer some people’s votes over others (the popular vote). Something called gerrymandering plays a role here, in which the riding boundaries are drawn in order to favour one party over another. Let’s treat this as a social issue and pretend that everyone’s vote counts equally.

Let’s say we’re electing the best programming language: C, Javascript, or PHP

# Plurality method, or First Past the Post

The winner is the one with the most singular votes. Plurality is *not* the majority, since it depends on the number of entries. This is bad for a few reasons:
This is how we just elected a minority government.
This leads to strategic voting, and given enough time, this electoral system ultimately encourages a two-party system.
This leads to the spoiler effect, or fragmentation: The better a third-party candidate does, the more it takes away from the more similar party in the two-party system

# Ranked ballots and the Condorcet condition

Ranked ballots are much better, since we have all the possible relevant information available from all voters. This _should_ be enough to devise a fair system since we have all available information up front, right?

Things are simple when we only have two options. We can select the winner based on majority rule.

Not so simple when we have three options. Let’s pretend three people voted:

| Language | Person 1 | Person 2 | Person 3 |
|----------|----------|----------|----------|
| JS       |  1       |    2     |    3     |
| C        |  3       |    1     |    2     |
| PHP      |  2       |     3    |    1     |

Let’s look at everyone’s favorite language: it’s a tie
Let’s look at everyone’s favorite pair of language:
More people prefer JS to PHP
More people prefer C to JS
More people prefer PHP to C


# The Condorcet Paradox and Criterion

This is the Concordet paradox! We have every individual’s rankings, but there is no group ranking. The Condorcet criterion is that if one candidate beats any other candidate, assuming there were only those two options, then they should be the winner. Why can we say this?

It’s because we are able the totality of everyone’s rankings for all options at once. We need for the problem to be reduced to a complete group ranking for it to work.

# Back to the Spoiler Effect & Fragmentation

This happens when you’re forced to distribute the vote between two very similar parties, whether we’re using a plurality or a ranked system. In some ways, it’s similar to the Condorcet paradox. If there are more than two options and we’re using a ranked voting system, this can’t be solved since we can’t prove that an arbitrary measure about the similarity of two parties is accurate. But if we’re reducing the problem down to two parties, your vote can never be lost. The alternative is to use a different voting system we’ll talk about in the next episode, called cardinal voting.

# Finding the complete group ranking: Two-Round Runoff

Do a plurality vote once. If the result is a majority, they win. If not, all those two didn’t vote for the top two must revote in another plurality vote.

Doing two plurality votes is better than doing only one because it considers some degree of ranking, but it doesn’t satisfy the condorcet criterion since it’s not a total group ranking, and it still fragments the vote.

# Finding the complete group ranking: Instant Runoff

Do a plurality vote once. Find the language with the least amount of votes, cross it off, and ask voters to vote again without that option. Repeat until there’s only one choice left. It does not meet the Condorcet criterion.

# Finding the complete group ranking: Borda count

Give every ranking a point value, and count the points at the end. This only partially solves the fragmentation problem since point values are arbitrary. And it doesn’t solve the Condorcet criterion

# The best way?
Also notice that all of these methods can be used in the same election only to give different winners, even when we have all possible information about each individual’s preferences.. How can we tell what’s the best result? Let’s define these systems more rigorously.
