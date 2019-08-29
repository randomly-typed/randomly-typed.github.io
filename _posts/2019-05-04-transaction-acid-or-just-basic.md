---
layout: post_1
title: 05 - Transactions, ACID or just basic?
date: 2019-05-04 -0400
categories: podcast
anchor: https://anchor.fm/randomly-typed/embed/episodes/5-Transactions--ACID-or-Just-Basic-e3u9ib/a-aecihe
description: "In this episode, we discuss the different kinds of database transactions, how they are implemented, and what guarantees they provide."
---

# Transaction <span class="footnote"></span>
- In the world of databases (and other things too)
- Dealing with persisted data and how it is managed
- One unit of work
  - Can be multiple queries

From Wikipedia:

  Transactions in a database environment have two main purposes:

1. To provide reliable units of work that allow correct recovery from failures and keep a database consistent even in cases of system failure, when execution stops (completely or partially) and many operations upon a database remain uncompleted, with unclear status.
2. To provide isolation between programs accessing a database concurrently. If this isolation is not provided, the programs' outcomes are possibly erroneous.

## Example
- Bank example
- Double spending problem (just like with cryptocurrencies)

# ACID <span class="footnote"></span>
The acronym was coined in 1987 (which is pretty much as old as the Internet)

## Durable
If a transaction completes, it will stay committed. Won’t lose data once the system says it’s safe.

### Example
A transaction was accepted by the DB, the power goes out, the transaction should still be there.

## Atomic
Everything or nothing gets applied from a transaction. If transaction fails, the database is left unchanged. All or nothing in the case of failure scenarios.

### Example
A transaction contains 10 modifications, either all the modifications get applied or none.

## Isolation <span class="footnote"></span>
In a traditional environment, multiple transactions will be executed concurrently.

Isolation ensures that concurrent execution of transactions leaves the database in the same state that would have been obtained if the transactions were executed sequentially

In other words, no one should ever be able to read or write on partially-applied data.

### Isolation levels
A higher isolation guarantee has a higher performance cost, both in terms of the amount of work needed to be done under the hood (rollback segments, copying data around, checking data) and/or the number of locks you need to place on rows. Most DBMSes support most of these separately on a per-transaction basis.

#### Serial
- No two transactions can run at the same time. This has perfect isolation, but has no concurrency at all.

#### Serializable
- With a lock-based, requires read and write locks (acquired on selected data) to be released at the end of the transaction. Also range-locks must be acquired
- each SQL-transaction executes to completion before the next SQL-transaction begins.

#### Repeatable reads
- With a lock-based, keeps read and write locks (acquired on selected data) until the end of the transaction.
- If you read the same data twice, you are sure to get the same value
- You still get phantom reads: if someone commits new row in a different transactions while yours is running, and you do a range select on an entire table, the rows you read the first time never changed, but you get more data back.

#### Read committed
- With a lock-based keeps write locks until the end of the transaction, but read locks are released as soon as the SELECT operation is performed
- It simply restricts the reader from seeing any intermediate, uncommitted, 'dirty' read. It makes no promise whatsoever that if the transaction re-issues the read, it will find the same data; data is free to change after it is read. → unrepeatable read.

#### Read uncommitted
- This is the lowest isolation level. In this level, dirty reads are allowed, so one transaction may see not-yet-committed changes made by other transactions.

#### Dirty read
A dirty read (aka uncommitted dependency) occurs when a transaction is allowed to read data from a row that has been modified by another running transaction and not yet committed.

## Consistent
The database must always stay in a valid state, doesn’t break any invariant.

### Example
- In double spending example, it could be that no one has less than 0$.
- All foreign keys need to point to a viable row.

# How to achieve ACID
## System with locks
More locking means more waiting on rows and less concurrency, less throughput. In most traditional relational databases, higher isolation level means more locking.

Granularity of locks can happen on
- Individual rows
- Pages (a group of adjacent rows)
- Entire tables

Deadlocks can also happen, where one transaction locks row A but needs to get B to proceed, and simultaneously another locks B and needs to get A to proceed. Death spiral.

### Pessimistic
- “Real locking”
- Prevents two people modifying the same row.

#### Read locks
- Read locks are acquired by reading a row
- Multiple transactions can share a read lock
- On read lock, the row can’t be updated

#### Write locks
- Other transactions can’t read over write locks

### Optimistic
- A system for knowing whether you should have locked something without actually locking anything. If you should  have locked, fail instead
- Good for higher throughput, but bad for concurrent-write-heavy workloads (worst case is that no writes happen at all). Use when it’s unlikely that there are any write conflicts.
- Every time data is written to, it increments a counter on the row.
- Right before you’re about to commit data, check that the row is the same as when you modified it.
- No data loss, no weird partial states, but it means transaction will need to be retried at a different time.
- Transactions are all-or-nothing. If it fails 100% of the tme, it’s still a valid transaction because we didn’t impart any bad state (or any state at all)

# Multiversion concurrency control
An alternative means to achieving isolation without the downsides of locking. It can’t rely on blocking, so it is optimistic. It provides a snapshot of the database at a particular instant in time.

Instead of overwriting original data, make a copy of the data with applied modifications, change the commit pointer to that branch. Append-only history.

Downside is the cost of storing multiple copies of data throughout time.

<span class="footnotes">
  [1] https://en.wikipedia.org/wiki/Database_transaction <br/>
  [2] https://en.wikipedia.org/wiki/ACID_(computer_science) <br/>
  [3] https://en.wikipedia.org/wiki/Isolation_%28database_systems%29 <br/>
</span>
