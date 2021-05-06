## Query Optimizer

### Intro

When a query is passed in,

1. Query Parser: checks correctness, authorization; generates a parse tree
2. Query Rewriter: converts queries to canonical form, e.g. flatten views, subqueries into fewer query blocks
3. "Cost-based" Query Optimizer: Optimizes 1 query block at a time, and uses catalog stats to find least-"cost" plan per query block
4. Passed the final query plan to the query executor.

Orthogonal concerns in query optimization:
1. plan space: Based on relational equivalences and different implementation choice
2. cost estimation: based on cost formulas and size estimation (based on catalog information and selectivity)
3. search strategy: how do we "search" in the "plan space" to find the lowest cost option

(Realistic) Goal: find the plan with least estimated cost (and try to avoid really bad actual plans) 

### Plan Space

**Algebra (Logical) Equivalences**

![[algebra-equiv.png]]

**Physical Equivalences**

What algorithms can we swap in

- Base table access with single table selections and projections: heap scan, index scan (if available on ref columns)
- Equijoins: BLNJ, Indexed NLJ (often good if 1 is relatively small, and the other is indexed properly), SMJ (good with small memory, equal-size tables), Grace Hash Join (better than sort if 1 table is small). 

**Heuristics**

1. Selection cascade and pushdown: apply selections as soon as you have the relevant columns
2. Projection cascade and pushdown: keep only the columns you need to evaluate downstream
3. Avoid cartesian products (not always optimal, e.g. when you have 2 very small tables)

**Note**: Pushing a selection into the inner loop (right branch) of a nested loop doesn't save IOs, because it still needs to scan the entire right table on every iteration. That's where materialization might come in handy.

#### Summary

For a SQL query, full plan space include all equivalent relational algebra expressions (join orders, operation orders), and all mixes of physical implementations of those algebra expressions (join algs).

We might prune this space by:
1. Applying heuristics (selection / projection pushdown, avoiding cartesian products)
2. Considering left-deep trees only (a System R heuristics)
3. Taking into account about physical properties (how the data is grouped), because downstream ops may depend on them, and enforcing them later might be expensive. E.g. SMJ groups data based on the group key, BLNJ preserves outer table ordering, hashing groups similar data together, etc.

### Cost Estimation

For each plan considered, we must estimate total cost
- estimate **cost** of each operation in plan tree, which depends on input cardinalities
- estimate **size of result** of each operation in tree
	- because it determines downstream input cardinalities
	- We use information about the input relations
	- Typical assumptions: **uniform distribution** of data, **independence** of predicates, inclusion assumptions for equijoins. 

#### Statistics and Catalogs

Statistics and Catalogs provide information on relations and indexes involved.

Typically it contains at least:
1. NTuples or || R ||: Number of tuples in a table (cardinality)
2. NPages or | R | : Number of disk pages in a table
3. Low / High: Min / Max value in a column
4. Nkeys: Number of distinct values in a column.
5. IHeight: Height of an index
6. INPages: Number of disk pages in an index.

Catalogs are updated periodically, and modern systems usually keep more detailed statistical information on data values, e.g. histograms.

#### Size estimates

Result cardinality = Max number of tuples x product of all selectivity

Assumption 1: Uniformly distributed over all distinct values in a column.

1. col = value -> sel = 1 / NKeys(I)
2. col1 = col2 (handy for joins too) -> sel = 1 / Max(NKeys(I1), NKeys(I2))
3. col > value -> sel = (High(I) - value) / (High(I) - Low(I) + 1)

Assumption 2: Independent Predicates
- Selectivity of AND = product of selectivities of predicates
- Selectivity of OR = sum of selectivities of predicates - product of selectivities of predicates
- Selectivity of NOT = 1 - selectivity of predicates

Assumption 3: Preservation of value sets

For joins $U = R1(A, B) \Join R2(A, C)$, then 
- NKeys(U, A) = min { NKeys(R1, A), NKeys(R2, A) }
- NKeys(U, B) = min { | U | , NKeys(R1, B) }.

#### Histograms

Types:
- Equidepth: each bucket has approximately same number of records
- Equiwidth: each bucket has (almost) equal number of values (same range)

Assumption: Within each bucket, records are uniformly distributed across the range of the bucket

Comment: In reality, most modern DB only maintains histogram for the top 10% of the distinct values, and treat the other buckets as uniformly distributed.

### Search Strategy

**Exhaustive search**

Calculate cost for every plan

**Greedy Algorithms**

Based on heuristic, e.g. smallest relation next, smallest result next

**Randomized techniques**

Randomly move to neighboring states until it reaches either a local minimum / global minimum using local optimization.

Moves are usually swaps between two relation, or cycles of three relations.

Comparison between exhaustive, greedy, and randomized algorithms:
- Search space: Exhaustive (largest, i.e. all), Randomized (has the potential to be large if rules is reasonable), Greedy (smallest)
- Plan Quality: Exhaustive (best), Randomized (probably second, because searching a larger space)
- Optimization overhead: Greedy (fastest), Randomized (allows end user to determine how much optimization by controlling how much time the optimizer get to run or controlling how many plans are compared before deciding that the plan is a local minimum based on the number of joins in query, e.g. more joins, more comparison) 

#### Dynamic Programming (System R)

The algorithm proceeds by considering increasingly larger subset of the set of all relations.
- Builds a plan bottom-up (beginning from 1 table, then to 2, and so on)
- Plans for a set of cardinality $i$ are constructed as extensions of the **best** plan for a set of cardinality $i-1$.

DP may maintain multiple plans per subset of relations to capture interesting orders of physical data, e.g. using SMJ ensures that the data is has been sorted, NLJ preserves orders, hashing groups data, etc.

Time complexity: For left deep trees -> $2^k -1$ entries, for bushy trees -> $O(3^k)$.



## Concurrency Control

Why?
- Increase throughput by increasing processor/disk utilization, e.g. can use CPU while another transaction is writing to disk.
- Increase latency since multiple transactions can run at the same time, so one transaction's latency need not be dependent on another unrelated transaction.

**Anomalies**
1. Dirty read: (WR conflicts) T2 reads an object that has been modified by T1 (which might abort later)
2. Unrepeatable read: (RW conflicts) T2 updates an object that T1 has just read while T1 is still in progress. T1 could get a different value if it reads the object again.
3. Lost update: (WW conflicts) T2 overwrites the value of an object that has been modified by T1 while T1 is still in progress. As a result, T1's update is lost.

### Transactions

- **Transaction** is a sequence of multiple **actions** (reads and writes of database objects) to be executed as an **atomic** unit (batch of work must commit or abort altogether).
- **Transaction manager** controls execution of transactions.


**ACID Properties of transaction**
1. Atomicity: Either execute all its actions or none of them.
2. Consistency: If the DB starts out consistent, it ends up consistent. Consistent = follows declarative integrity constraints, e.g. in `CREATE TABLE` statements.
3. Isolation: Execution of each transaction is not affected by (isolated from) other transactions
4. Durability: The effects of a commited transaction must survive failures.

Concurrency control provides isolation property, e.g. via 2PL
Recovery provides atomicity and durability properties, e.g. via WAL

### Schedules

- A **schedule** is a sequence of actions on data from 1 or more transactions
- A schedule is a **serial** schedule if each transaction runs from start to finish without any intervening actions from other transactions
- 2 schedules are **equivalent** if 
	1. involve the same transactions
	2. each individual transaction's actions are ordered the same
	3. both schedules leave the DB in the same final state.
- Schedule S is **serializable** if S is equivalent to *some* serial schedule.

#### Conflict Serializable Schedules

- Two operations **conflict** if they are by different transactions, acting on the same object, and at least one of them is a write.
- 2 schedules are **conflict equivalent** iff:
	1. They involve the same actions of the same transactions
	2. Every pair of conflicting actions is ordered the same way.
- Schedule S is **conflict serializable** if S is conflict equivalent to *some* serial schedule. 
- Equivalently, a schedule S is conflict serializable if you are able to transform S into a serial schedule by swapping *consecutive non-conflicting* operations of different transactions.
- To rigorously prove serializability, we can construct a **dependency graph** with 1 node per transaction, and an edge from Ti to Tj if an earlier operation Oi of Ti conflicts with an operation Oj of Tj.

**Theorem.** Schedule is conflict serializable iff its dependency graph is acyclic.

Remark: conflict serializable schedules are a subset of all serializable schedules.

#### View Serializable Schedules

- Schedules S1 and S2 are **view equivalent** if:
	1. Same initial reads: if Ti reads the initial value of A in S1, then Ti also reads the initial value of A in S2.
	2. Same dependent reads: if Ti reads the value of A written by Tj in S1, then Ti also reads the value of Tj in S2.
	3. Same winning writes: If Ti writes final value of A in S1, then Ti also writes final value of A in S2.
- Schedule S is **view serializable** if S is view equivalent to *some* serial schedule. 
- View serializable schedules are the set of all conflict serializable schedules, which also allows "blind writes".

Remark: 
- conflict serializability is more commonly used because it can be enforced efficiently.
- serial $\subset$ conflict serializable $\subset$ view serializable $\subset$ serializable schedules.

#### Recoverable Schedules

For correctness, if Ti has read from Tj, then Ti must abort if Tj aborts. This recursive aborting phenomenon is known as **cascading aborts**

- A schedule S is **recoverable** if for each transaction Ti in S, Ti commits after Tj if Ti reads from Tj.
- A schedule S is **cascadeless** if a transaction Ti only reads from a committed transaction Tj.
- A schedule S is **strict** if for every $W_i(O)$ in S, O is not read nor written by another transaction until Ti either aborts or commits.

Remark: 
- Recoverable schedules prevent undoing committed transactions, but still suffer from cascading aborts.
- Cascadeless schedules allow writing to an object previously written by another uncommitted transaction.
- serial $\subset$ strict $\subset$ cascadeless $\subset$ recoverable schedules.

### Pessimistic CC: Locking-based Protocol

The most common scheme for enforcing conflict serializability is 2 phase locking. However, it is a bit pessimistic compared to alternative schemes, e.g. Optimistic or Timestamp-Ordered or Multiversion Concurrency Control.

#### 2 Phase Locking (2PL)

**Rules**
1. Well formed: Transaction must obtain a S (shared) lock before reading and an X (exclusive) lock before writing
2. Legal: Scheduler respects the lock compatibility matrix
3. Two-phase: Transaction cannot get new locks after releasing any lock.

**Lock compatibility matrix**

| | S | X |
| --- | --- | --- |
| S | T | - |
| X | - | - |

2PL guarantees conflict serializability, but does not prevent cascading aborts.

**Why 2PL guarantees conflict serializability?**

When a commiting transaction has reached the end of its acquisition phase, call this the "lock point". At this point, it has everything it needs locked and any conflicting transactions either started release phase before this point, or are blocked waiting for this transaction. Two conflicting transactions will see data in the order that their locked points occur. So, the order of lock points gives us an equivalent serial schedule.

#### Strict 2 PL

As noted previously, 2PL suffers from cascading aborts.

Strict 2PL is similar to 2PL, except all locks are released together when transaction completes, i.e. either transaction has committed (all writes durable) OR aborted (all writes have been undone). As a result, the transaction will be atomically visible in the database, and there is no need for cascading aborts.

Theorem. Strict 2PL schedules are strict and conflict serializable, but might suffer from deadlock.

Comment: Googling says, this is called rigorous 2PL. Strict 2PL only delays releasing X locks.

#### Lock Management

Lock and unlock requests are handled by Lock Manager. LM maintains a hashtable, keyed on names of objects currently being locked, where each entry contains
- granted set: set of transactions currently granted access to the lock
- lock mode: type of lock held
- wait queue: queue of conflicting lock requests.

#### Lock Granularity

**What are the objects that we lock?**

We have a dilemma between locking large objects (e.g. relations) which require few locks but result in low concurrency, and locking small objects (e.g. tuples, fields) which require more locks but result in higher concurrency.

**Multiple Locking Granularity**

- Allows us to not have to make same decision for all transactions, as we allow data items to be of various sizes.
- Define a hierarchy of data granularities, and view it as a tree (DB -> tables -> pages -> records)
- When a transaction locks a node in the tree *explicitly*, it *implicitly* locks all the node's descendants in the same mode.

##### Warning Protocol (Jim Gray)

Idea: We allow transactions to lock at any level, but it must have proper intent locks on all its ancestors in the granularity hierarchy before getting S or X locks.

Intention lock modes:
1. IS: Intent to get S lock(s) at finer granularity
2. IX: Intent to get X lock(s) at finer granularity
3. SIX: Like S and IX at the same time. Useful for typical SQL update command, e.g. `UPDATE employees SET salary = 1000 WHERE name = 'Bob';`

Intention locks allow a higher level node to be locked in S or X mode without having to check all descendant nodes.

How it works:
- Each transaction starts from the root of hierarchy
- To get S or IS on a node, must hold IS or IX on parent node.
- To get X or IX or SIX on a node, must hold IX or SIX on parent node.
- Release locks in bottom-up order.
- Enforce 2 phase and lock compatibility matrix rules.

**Lock compatibility matrix**

| | IS | IX | S | SIX | X |
| --- | --- | --- | --- | --- | --- |
| IS | T | T | T | T | - |
| IX | T | T | - | - | - |
| S | T | - | T | - | - |
| SIX | T | - | - | - | - |
| X | - | - | - | - | - |

Comment: Why IX and SIX is not compatible? If SIX is currently hold, every child node implicitly holds S lock. If I allow IX, the future X request on a child node will be granted as the S lock is only hold implicitly. However, S and X lock are incompatible, so I should not allow IX lock.

**Examples**:
1. T1 scans R and updates a few tuples: gets an SIX lock on R, and get X lock on updated tuples
2. T2 reads only part of R: gets an IS lock on R, and repeatedly gets an S lock on tuples of R
3. T3 reads all of R: gets an S lock on R OR proceed like T2 with lock escalation when too many low level locks are acquired. 

#### Deadlock

Deadlocks are cycle of transactions waiting for locks to be released by each other.

Lock upgrade requests should be prioritized to avoid deadlocks. Even then, multiple lock upgrades would still end up in deadlocks.

Common techniques of deadlock prevention fails:
1. using timeout: what if transactions holds locks for a long time because it is busy doing some computation?
2. resource ordering: we cannot impose an order on the tuples or pages in our files.

##### Deadlock Avoidance

Assign priorities to transactions, e.g. based on age: now - start_time.

Say A wants a lock that B holds. Two possible policies
1. **Wait-Die**: If A has higher priority, A waits; else A aborts
2. **Wound-Wait**: If A has higher priority, B aborts; else A waits

Details:
- These schemes guarantee no deadlocks because there is no cycle of waiting.
- To prevent starvation, if a transaction restarts, it should get its old timestamp.
- We can use other priority schemes, such as measures of resource consumption like number of locks acquired.

##### Deadlock Detection

1. Create and maintain a "waits-for" graph
2. Periodically check for cycles in a graph. 
3. Breaks the deadlock by aborting a transaction in cycle using some priority scheme (random, most "connected", workload/time-based, etc.)

#### Phantom Reads

In the above discussion, we have mechanisms to prevent the dirty read, unrepeatable read and lost update problems. However, it assumes that we are working with a static database. When insert / delete actions are accounted, we might  face the phantom read anomaly.

**Phantom Read** occurs when a transaction *re-executes* a query returning a set of rows that satisfy a search condition and finds that the set of rows satisfying the condition has changed due to another recently committed transaction.

A simple solution would be to lock the logical range that satisfy the search condition.

In practice, we set locks in indexes cleverly, so called "next key locking".

### Optimistic CC: Validation-based Protocol

This protocol is optimistic and lock-free! -> no deadlocks!

Each transaction have 3 phases:
1. Read 
	- Read all DB values that needs to be read / written into a temporary local storage
	- Do all updates / writes on local storage
	- Maintains read-set (RS) and write-set (WS)
2. Validate: Check if schedule so far is serializable by ensuring no conflict between RS / WS of different transactions
3. Write: If validate returns ok, write to DB the values of WS. If not, "roll-back".

**Details:**

- We maintain the timestamps for 
	1. start(T): start of read phase of T
	2. validate(T): start of validate phase of T -> used as the timestamp of transaction ts(T).
	3. finish(T): end of write phase.
- Transactions are serialized using ts(T)
- The resulting schedule are casecadeless. 
- Rolled-back transactions restart with a new timestamp.

**Validation rules for transaction A:**

For each active transaction B such that ts(B) < ts(A), we must have transaction A to satisfy one of the following conditions:
1. finish(B) < start(A) : nothing to check
2. start(A) < finish(B) < validate(A) : check RS(A) $\cap$ WS(B) = $\emptyset$.
3. validate(A) < finish(B) : check (RS(A) $\cup$ WS(A)) $\cap$ WS(B) = $\emptyset$.


### CC for indexes

We don't want to use 2PL on B+ tree pages  because the concurrency would suffer badly. Instead, we use in-memory short locks (latches) in a clever way.

Idea: Upper levels of B+ tree just need to direct traffic correctly.
Possible problems:
1. Two transactions / threads modify the contents of the same node at the same time
2. One transaction / thread traverses the tree while another splits / merges the node.

**Solution**: Latch Coupling / "crabbing". (We have R and W latch)

Suppose we have a latch on a node N, we get a latch on the appropriate child C of N and release latch on N only when we are sure that the node is not going to be splitted / merged when updates happen.

**An alternative latching scheme**

Whenever we insert/delete, we apply a W latch on the root node at the beginning. One possible solution to increase concurrency would be to acquire only R latch until leaf level, and if the leaf is unsafe, then we restart and revert to the basic latch coupling scheme.

**Leaf Traversal**

So far, we have discussed tree traversal (top -> bottom). If the latch of some child node is latched, the transaction will wait.

However, in some cases, we also need to do leaf traversal, e.g. range queries. Here, waiting can create deadlocks, e.g. imagine when 2 transactions do leaf traversal in opposite direction. Therefore, to avoid deadlocks, we **adopt a "no-wait" scheme**, i.e. any transaction that finds the next leaf locked, should abort and restart.

## Recovery

**When do transactions abort?**
- User / application explicitly aborts
- Failed consistency check, i.e. violation of integrity constraint
- Deadlock
- System failure prior to successful commit

**Why do databases crash?** Operator error, configuration error, software failure, hardware failure

Buffer Management plays a key role in recovery.
1. Can a dirty page updated by a transaction T be written to disk before T commits?
	- Yes -> **STEAL** policy. Need to remember the old value of flushed pages to support UNDOing the write to those pages if transaction aborts or system crashes before the transaction can finish.
	- NO -> **NO STEAL** policy. Achieves atomicity without UNDO logging, but can cause poor performance, since pinned pages limit buffer replacement. 
2. Must all dirty pages that are updated by transaction T be written to disk when T commits?
	- Yes -> **FORCE** policy. Provides durability without REDO logging, but can cause poor performance due to lots of random I/O during commit.
	- No -> **NO FORCE** policy.  Flush as little as possible (only flush logs). Need to remember the new value to allow REDOing modifications in case of system crash before dirty page is flushed to DB disk.

### Log-Based Recovery

Idea: For every update, record info to log to allow REDO/UNDO.

#### The Log

**Log**: An ordered list of log records, with a write buffer ("tail") in RAM.
**Log records**: < transaction ID, pageID, offset, length, old data, new data >

- Each log record has a **Log Sequence Number (LSN)**, which is unique and increasing
- Track **flushedLSN** in RAM (LSN of the last log that we flush to disk)
- Each data page in the database contains a **pageLSN**, i.e. the LSN of the most recent log record that updates that page
- To implement Write Ahead Logging: before page X is flushed to DB, it must satisfy pageLSN_X $\leq$ flushedLSN.


#### UNDO logging - STEAL/FORCE

For every action, generate undo log record that contains the OLD value

Logging rules:
1. If T modifies X, then \<T, X, v> must be written to disk before the dirty page contaning X.
2. If T commits, then dirty pages must be written to disk before \<COMMIT T>. 

Recovery rules:
- Construct set S of incomplete transactions
- Undo actions of transactions in S in *backward* order.

Remarks: dirty pages are written early, before commit

#### REDO logging - NO STEAL/NO FORCE

For every action generate redo log record that contains the NEW value

Logging rules:
1. If T modifies X, then both \<T, X, v> and  \<COMMIT T> must be written to disk before the dirty page contaning X.

Recovery rules:
- Construct set S of committed transactions
- Redo actions of transactions in S in *forward* order.

Remarks: dirty pages are written late, after commit

#### UNDO/REDO logging - STEAL/NO FORCE

Logging rules:
1. Log record flushed before corresponding updated page
2. ALL log records (including commit log) flushed at commit

Recovery process:
- Backward pass
	- Construct set S of committed transactions
	- Undo actions of transactions not in S
- Forward pass: Redo actions of transactions in S

Remarks: No restriction on when to write dirty pages.

### Checkpointing

Problem: Recovery can be very, very SLOW because we need to read from the beginning of the log.

Simple Solution: We periodically checkpoint
1. Do not accept new transactions
2. Wait until all (active) transactions to finish
3. Flush all log records to disk (log)
4. Flush all buffers to disk (DB)
5. Write "checkpoint end" record on disk (log)
6. Resume transaction processing

Now, we don't need to examine log records before the most recent checkpoint. However, the database freezes during checkpoint

#### Non-Quiescent Checkpointing

##### Undo Log

- Record all active transactions S at \<START CKPT>
- Wait until all transactions in S to finish. Undo Logging guarantees that all updates made by transactions in S are reflected on disk (DB).

During recovery, we only need to UNDO all uncommitted (including aborted) transactions after the most recent \<START CKPT>.

##### Redo Log

- Write to disk all dirty pages updated by transactions that committed before \<START CKPT>.

During recovery, we only need to REDO all committed transactions after the most recent \<START CKPT>.

##### Undo/Redo Log

- Flush all dirty buffer pages prior to \<START CKPT>.

During recovery, we only need to REDO all committed transactions and UNDO all uncommitted (including aborted) transactions after the most recent \<START CKPT>. 

### Handling Media Failures

Make copies of data
- Triple Modular Redundancy: keep 3 copies on separate disks, and vote for consensus
- DB Dump + log: If active database is lost, restore active database from backup + replay redo entries in log.