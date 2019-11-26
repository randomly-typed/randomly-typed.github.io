---
layout: "post_1"
title: "02 - To the hype train"
date: 2019-03-24 -0400
categories: podcast
anchor: https://anchor.fm/randomly-typed/embed/episodes/To-the-Hype-Train-e3hp2h/a-ac7ape
description: "Are cryptocurrencies just hype? Probably, but let's still talk about how they were created, their merits and their problems."
---

## “Real” currencies
- Used to be backed by gold
  - US abandoned gold standard in 1933 and stop the convertibility of dollars into gold in 1971 <span class="footnote"></span>
- Now, it is backed by trust on the country

## Blockchain
- It’s a fundamental technology
- The “blockchain is an open, distributed ledger that can record transactions between two parties efficiently and in a verifiable and permanent way” <span class="footnote"></span>
- The goal is to have contracts that can’t be lost or tempered with once both every parties agreed on it.
- It’s a list of blocks, which are a batch of transactions
- Data structure : merkle tree
  - A tree (more about these in future episode), node and edges originating from the root node (DAG). Usually binary
  - Every node hash a hash associated with its contents, including child nodes
  - Root hash used for comparison for equality since changes in child node hashes bubble up
  - Why not just hash all the content? Partial verification! Split your content into 4 chunks [a,b,c,d]. To verify that d is a part of the original content, all you need in d, hash(c), and the hash of the left subtree below the root node
- It’s distributed, so there’s not a single server that manages it.
- It’s permissionless. Anyone can participate with proof of work. This means there’s no credential to steal.
- \> 10k nodes
- Having that shared ledger could reduce the number of required “Intermediaries like lawyers, brokers, and bankers”
- It’s not anonymous.

## Bitcoin
- Proposed in october 2008 with the blockchain by someone called Satoshi Nakamoto
  - We still don’t know who he is
- The invention of the blockchain for bitcoin made it the first digital currency to solve the double-spending problem without the need of a trusted authority or central server. <span class="footnote"></span>
  - Double-spending is a potential flaw in a digital cash scheme in which the same single digital token can be spent more than once. Unlike physical cash, a digital token consists of a digital file that can be duplicated or falsified. <span class="footnote"></span>
- The network collectively agrees on every transactions
- Decentralized currencies that rely on blockchain are vulnerable to the 51% attack <span class="footnote"></span>
- The longest chain of blocks is the valid chain

## How <span class="footnote"></span>
1. New transactions are broadcast to all nodes.
2. Each node collects new transactions into a block.
3. Each node works on finding a difficult proof-of-work for its block.
4. When a node finds a proof-of-work, it broadcasts the block to all nodes.
5. Nodes accept the block only if all transactions in it are valid and not already spent.
6. Nodes express their acceptance of the block by working on creating the next block in the chain, using the hash of the accepted block as the previous hash.

- If 2 nodes send a block at the same time during steps 4, the one receiving the most blocks afterward becomes the accepted block.
- At any given time, there could be many different valid blockchain histories.
- Also, this means that we are not guaranteed that a block will remain on the chain.
- Incentives : Every block adds a transaction that creates bitcoins and send them to the creator. Also, transactions can add fee to itself. Those fees will be collected by by the creator of the accepted block.

## Proof-of-work <span class="footnote"></span>
- Distributed consensus
- As the node/miner :
1. You take the previous hash, a random nonce and the list of transactions you want to validate.
2. Hash that blob
  - Operation that attempts to “uniquely” map an input of arbitrary size to an output of known side
  - Collisions will always exist because the number of possible output values is fewer than the number of possible input values. If cryptographic, it represent the unique identity of the object, so finding two input with the same hash invalidates the function
  - Cryptographic hashes make it so that retrieving original data is nearly impossible. Hash shouldn’t be predictable or similar to / varying with input
3. If there’s enough leading 0s, you just found a valid block
4. If not, change the nonce and retry
- The difficulty (aka. Numbers of 0s) changes over time. The goal is to produce on average 1 block every 10 minutes.

## Price of using bitcoin
- Transaction fees
  - You can add satoshis to your transaction. The miner that will add this transaction to the blockchain will win those satoshis. Today on average it will cost $0.15 USD to be in the next block (10 minute wait). In 2018 some days were over $1.00 USD. <span class="footnote"></span>
- Transaction delay. Normally, you wait between 2 to 6 confirmations before being safe. Today, it should take less than 30 minutes to be validated.  At the beginning of 2018, on average it could take more than 3 hours for a transaction to be validated. <span class="footnote"></span>
- Energy consumed by the network. <span class="footnote"></span>
  - Bitcoin's current estimated annual electricity consumption* (TWh)49.5. Which is approximately twice what Scotland consumes.
  - A single bitcoin transaction requires more energy than 250,000 visa transactions.
  - Currently, bitcoin is built around proof-of-work. There’s other consensus algorithms that could replace it, like proof-of-stake. It would greatly reduce the energy consumption.
- There’s no one to bail you out if there’s a problem

## Hype <span class="footnote"></span>
- The question about private blockchain. Why would a blockchain be better than a normal database?
- What protects the bitcoin is that it would take more resource to rewrite/attack the blockchain than what’s on it.
- So, it’s protected by the number of miners on the planet.
- Most private blockchain don’t have the ‘race’ of traditional cryptocurrencies. So there’s no incentives to be faster and spend more money on hardware and energy.
- Most likely the owner of the private blockchain will control 100% percent of the compute power/miner. This means that an attack on those servers could give the attacker the complete control of the blockchain and rewrite the chain as he wish.

# Stablecoins <span class="footnote"></span>
- A cryptocurrency pegged to a stable asset, like gold.
- GMO, Japanese tech giant announced they would release GYEN, which will be a cryptocurrency pegged to the Yen.
- JP Morgan announced JPM Coin which will be backed by the USD.

<span class="footnotes">
  <a href="http://bancroft.berkeley.edu/ROHO/projects/debt/terminationgolddollar.html">[1] http://bancroft.berkeley.edu/ROHO/projects/debt/terminationgolddollar.html</a> <br/>
  <a href="https://mentalfloss.com/article/12715/why-did-us-abandon-gold-standard">[2] https://mentalfloss.com/article/12715/why-did-us-abandon-gold-standard</a> <br/>
  <a href="https://hbr.org/2017/01/the-truth-about-blockchain">[3] https://hbr.org/2017/01/the-truth-about-blockchain</a> <br/>
  <a href="https://hbr.org/2017/01/the-truth-about-blockchain">[4] https://hbr.org/2017/01/the-truth-about-blockchain</a> <br/>
  <a href="https://hbr.org/2017/01/the-truth-about-blockchain">[5] https://hbr.org/2017/01/the-truth-about-blockchain</a> <br/>
  <a href="https://en.wikipedia.org/wiki/Double-spending">[6] https://en.wikipedia.org/wiki/Double-spending</a> <br/>
  <a href="https://en.wikipedia.org/wiki/Double-spending">[7] https://en.wikipedia.org/wiki/Double-spending</a> <br/>
  <a href="https://bitcoin.org/bitcoin.pdf">[8] https://bitcoin.org/bitcoin.pdf</a> <br/>
  <a href="https://en.wikipedia.org/wiki/Blockchain">[9] https://en.wikipedia.org/wiki/Blockchain</a> <br/>
  <a href="https://bitcoin.org/bitcoin.pdf">[10] https://bitcoin.org/bitcoin.pdf</a> <br/>
  <a href="https://bitcoinfees.info/">[11] https://bitcoinfees.info/</a> <br/>
  <a href="https://www.blockchain.com/charts/avg-confirmation-time?daysAverageString=7&timespan=1year">[12] https://www.blockchain.com/charts/avg-confirmation-time?daysAverageString=7&timespan=1year</a> <br/>
  <a href="https://digiconomist.net/bitcoin-energy-consumption">[13] https://digiconomist.net/bitcoin-energy-consumption</a> <br/>
  <a href="https://www.computerworld.com.au/article/606253/understanding-blockchain-hype-why-much-it-nothing-more-than-snake-oil-spin/">[14] https://www.computerworld.com.au/article/606253/understanding-blockchain-hype-why-much-it-nothing-more-than-snake-oil-spin/</a> <br/>
  <a href="https://decryptmedia.com/5173/jp-morgan-coin-cryptocurrency">[15] https://decryptmedia.com/5173/jp-morgan-coin-cryptocurrency</a> <br/>
</span>
