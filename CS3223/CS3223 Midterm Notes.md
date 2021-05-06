## Disks and Access Times

**Disk Anatomy**

- Disk is composed of stacked platters spinned by a central spindle.
- Arm assembly is moved in or out to position a **head** on a desired **track**
    - Tracks under heads make a "cylinder"
- Block size is a multiple of (fixed) **sector** size.

**Disk Access**

1. Seek time (moving arms to position disk head on track): ~0.3-10 ms
2. Rotational delay (waiting for block to rotate under head) : ~0-4 ms
3. Transfer time (moving data to/from disk surface) : ~0.05 ms / 8KB page

**Page**: Unit of transfer for disk read / write , usually 4KB - 1MB these days

**Blocks**: consecutive number of pages. Typical block size: 1MB - 64MB.

### Key Things to Note while calculating access time

- Smallest read is 1 page! -> 1 or more sector (NOT 1 tuple!) ?
- Random or sequential access
    - Random -> seek + rotational delay per records
    - Sequential -> seek (first time) + track-to-track delay (subsequent head movement) + rotational delay (every new track)
- Gaps between sector: No need to read last gap!

## Disk Space Management 

**Free Space Management** -> Not-yet-allocated pages

- Bitmap: Free block -> 0, Allocated block -> 1. To allocate, scan for 0 in bitmap.
- Linked List: Link all free disk blocks together. DBMS maintain a free space list head (FSLH)

**Free Space Allocation**

- Granularity: **pages** vs **blocks** (multiple consecutive pages) vs **extents** (multiple consecutive blocks). Smaller (Fragmented) vs Larger (low space utilization tradeoff)
- Allocation methods. **Contiguous** (need to reclaim space frequently) vs** linked list** (fragmented)

**Allocated Space Management** -> From hardware POV, these pages has been allocated to a DB file, but some pages might still contain no data yet. The following section elaborates on how these allocated pages are managed.

Header pages may contain: number of records, how much free space is on the page, pointer to next page, bitmaps / slot tables to find free space on the page

Implementation 

- List : Header page maintain 2 pointers (1 to a chain of full / used pages, 1 to a chain of free pages) + additional metadata
- Page Directory: The directory is a collection (say, linked list) of header pages. The entry of a header page include pointers to many data page and the number of free bytes on the referenced page. The head of the page directory is stored in the database catalog.

## Buffer Space Management 

Motivation: Files and Index Management expects data to be in RAM. 
10k feet view: Buffer Management is in a sense very, very similar to cache.

- Buffer Manager manages a **buffer pool**, large range of RAM allocated for DBMS on server boot time. 
- Buffer Pool is partitioned into page-sized partitions called **frames**. 
- Metadata: Table of <frameid, pageid, dirty flag, pin count> pairs are maintained.
    - Pin count represent the number of queries that is using the page. +1 on every request, and caller must immediately unpin page on query completion

#### Page Replacement Policy

- FIFO: good only if the page access behaviour is sequential.
- Least Recently Used (LRU), usually approximated by Clock policy.
- Most Recently Used (MRU): outperform LRU/Clock on sequential scans.

Improvement: prefetching.

### Files as Pages of Records

Tables are stored in logical **DB files**: a collection of pages, each containing a collection of records.

Pages are managed on disk by disk space manager, and in main memory by the buffer manager. Each DB file could span multiple OS files and even machines.

API for higher layers of DBMS:
- Insert/delete/modify record
- Fetch a particular record by **record id**: a pointer encoding pair of (**pageID, location** on page)
- Scan all records

#### Record Formats

Assume the schema and field types is stored in **System Catalog**. The goal is to have fast access to fields and compact records both in memory and in disk format.

- Fixed length
- Variable Length: Have a field count, and delimit the data with a special character (e.g. `$`)

#### Page Formats

- Fixed-length record (Unpacked) 
    - Use number of slots field + a bitmap to denote "slots" status (valid / deleted records). Record id: <page id, slot number>. Insertion: Find first free slot. Deletion: Toggle bitmap "slot" status.
    - cannot move around records w/o updating record id
- Variable-length record
    - Introduce slot directory in footer
        - number of slots in slot directory (to keep track if we need to add more slots)
        - pointer to start of free space
        - each entry stores length + pointer to beginning of record (arranged in reverse order)
    - Can move around records with updating record id

## Indexes

- **data entries** (items stored in the index : pair of keys and heap file pointers)

### Tree Based Indexes (B+-tree)

- order dependent
- Based on **sorting of search key**.
- Leaf nodes stored in **sorted** data entries.  
- Leaf nodes are either **singly** or doubly linked list
- Each data record has an entry in the leaf node **(dense index)**
- d <= \#records <= 2d -> d is called **order**. 
    - Note: Number of keys stored must be an even number (2d).
    - Fanout : 2d + 1.
- The range for internal nodes are left-inclusive and right-exclusive. No duplicate keys amongst internal nodes. 
- Each node corresponds to a page. So, accessing a node might cost I/O.
- Unless otherwise stated, data entry format is <key, pointer to data record> (format 2).

**Insertion**

- Always insert to leaf, then update index recursively
- Note: copy up on *leaf* node split, but push up on *internal* node split.

**Deletion**

- Delete from entry. If *leaf* node underflows, try borrowing from sibling, else merge siblings. If *internal* node underflows, pull parent down (+ re-split, similar to insertion, if it the result of the merge overflows)

**Clustered index**

- Index in which heap file records are kept mostly ordered according to search keys in index (order need not be perfect). 
- There are at most 1 such index / table.

#### Notes on counting tree-index accesses

- Calculate order! Max keys is even! Don't forget fill factor if specified
- Single access queries: height of tree + 1 (record lookup, assuming format 2)
- Range queries: (height of tree - 1) + number of data entries (leaf nodes) to traverse + 1 for every matching fecord (record lookup, worst case, assuming format 2)

### Hash-based Indexes

- Key k, hash function h, h(k) returns the pageID that stores record with *search key* k.
- Best for equality selections, inefficient for range searches (depends on hash function used).
- Performance degenerate for skewed data distributions
- Buckets consists of 1 primary data page, and 0+ chain of overflow pages. 
- Each data entry may contain **the records directly** or pointers to data records. 

**Static Hashing** -> order independent

- Data stored in M (a fixed number) buckets

**Dynamic Hashing: Linear Hashing** -> order dependent

```
0 1 ... next - 1 | next ... N_i - 1 | N_i ... N_i + next - 1 
uses h_(i + 1)       uses h_i             uses h_(i + 1)
```

- Hash file grows linearly (**1 bucket at a time**, i.e. $B_i$ should be split before $B_j$ if $i < j$). 
    - At the end of each **splitting round**, the size of hash file would have doubled, and the hash function should be changed. 
    - Instead of doubling the number of buckets at once, splitting only 1 bucket at a time minimize the number of record redistributions that is needed, thus the operation that triggers this splitting is minimally affected.
- Use the last $\lceil \log N(i) \rceil + 1$ bits of h(k) to split records between $B_j$ and $B_{N(i) + j}$
- Maintain a "next" pointer to indicate which bucket to split next.
- When to split a bucket? Split whenever **some** bucket overflows 
    - This will increment the "next" pointer (or increment level and set "next" <- 0)
    - It might be the case that the current bucket we split is not overflowing. 
- When to delete a bucket? Only when the last bucket is empty. 
    - Decrement "next" (or decrement level and set "next" <- last bucket in prev level)
- Linear hashing is **dependent** on the order of insertion / deletion.

On average for uniformly distributed data, 1.2 disk I/O is needed.

#### Notes on counting hash-index accesses

- Calculate number of primary data pages needed! Don't forget fill factor if specified.
- Single access queries: 1.2 (assuming format 1)
- Range queries: 1.2 x number of matching record.

## External Sort

![[external-sort.png]]

Sort a file with $N$ pages using $B$ buffer pages.

1. Pass 0: (Internal) sort each page in RAM. Produce $\lceil N / B \rceil$ sorted runs of $B$ pages each.
2. Pass 1, ... : merge $B - 1$ runs at a time (one buffer is used as the output buffer) using streaming

Number of passes: $1 + \lceil \log_{B - 1}\lceil N / B \rceil \rceil$
Cost: $2N \times$ number of passes. With big values of $B$, this cost is easily linear time.

Memory requirement for 2 pass sort: $\sim \sqrt{N}$ memory to sort $N$ pages.

**On internal sort algorithm**
 
- We can use replacement selection instead to further reduce the number of passes (and generate longer runs than memory size)
- In practice the run length of replacement selection is generally $2B$.

Replacement Selection Algorithm

- Read B blocks into memory. For each iteration, move the smallest record to output buffer then read in a new record. If the new record < last record in output buffer, freeze block. Keep looping until all blocks are freezed. 
- Worst case: produce runs of length B. Best case: produce 1 run of length N.

**Is minimizing pass always optimal?** (sequential IO vs random IO)

Not always. For example in the merge step, assuming we have $B$ input buffer pages and a run fits in a track, we have 2 alternatives.
1. Merging $B$ runs of $N$ pages at once will incur a cost of a seek every time we read a page from a run. Total number of seek: $BN$
2. We will need 2 steps. If in the first step, we were to merge $\frac{B}{K}$ runs of $N$ pages at a time ($K$ times), we can read $K$ pages at once, thus for each run we only need $\frac{N}{K}$ seeks. As we have $\frac{B}{K}$ runs and we need to repeat this merging $K$ times, we ended up with $\frac{BN}{K}$ seeks for the first step. In the second step, we merge $K$ runs of $\frac{BN}{K}$ pages, we can read $\frac{B}{K}$ pages at once, thus for each run, we only ended up with $N$ seeks. We ended up with $KN$ seeks for the second step. In total this is only $\frac{BN}{K} + KN$ (or to be simplistic, number of passes  $(2) \times \frac{BN}{K}$) seeks, smaller than $BN$.

*The intended formula is just number of pass x ((number of data page / number of page per read op) x read cost + (number of data page / number of page per write op) x write cost) + pass 0 cost.*

**Using B+-tree for sorting**

A clustered B+-tree index is good for sorting, while unclustered tree index in general performs worse than external sort (on reasonably sized buffer page), it can be useful in scenario where initial fast response is needed (e.g. to upstream operator).

## Evaluating Operations

Notation: 
- $|R|$ :  the number of pages of relation R
- $p_R$ : tuples per page

### Equality join on 1 column

Always try to make the outer loop smaller in size then the inner loop. :D

#### Simple (Tuple-based) Nested Loop Join

```
for tuple r in R do
    for tuple s in S do
        if r.sid == s.sid then add <r,s> to result
```

Cost: $|R| + (|R| \times p_R) \times |S|$

#### Block Nested Loop Join

```
for page P_R of R do
    for page P_S of S do
        for tuple r of P_R do
            for tuple s of P_S do
                if r.sid == s.sid then add <r,s> to result
```

Cost: $|R| + |R| \times |S|$
Memory: 3 pages.

We can improve on this if we have more than 3 pages.
Cost: $|R|  + \left\lceil \frac{|R|}{B - 2} \right\rceil \times |S|$
Memory: $B$ pages

#### Sort-Merge Join

1. Sort R and S on the join column -> $2|R| \times (1 + \lceil \log_{B - 1}\lceil |R| / B \rceil \rceil)$ each
2. Scan them to do a "merge" on join column and output result tuples. -> $(|R| + |S|)$

Cost: Sort cost + Merge cost

Note: To sort R and S in two passes each, then $B > \sqrt{\max(|R|, |S|)}$

#### Grace Hash Join

![[external-hash.png]]

1. Partition phase: **number of partition passes** $\times 2 \times (|R| + |S|)$.
    1. Partition relation R (on join attribute) using hash fn h. <- at most $B-1$ partition.
    2. Partition relation S using the same hash fn h
    3. R tuples in partition i will only match S tuples in partition i
2. Join phase: $|R| + |S|$
    1. Read in a partition of R -> partition should fit in $\leq B - 2$ pages.
    2. Build a hash table for the partition using hash fn h2
    3. Scan matching partition of S, search for matches (using hash fn h2)

Need to check whether $\min(|R|, |S|) \leq (B-1)(B -2)$. If not, apply the hash-join partition step recursively.

Cost: partition cost + join cost.

#### Index Nested Loops Join

Precondition: There is an index on the join column of one relation (S) -> put it as the inner relation to exploit the index.

```
for tuple r in R do
    search index of S on sid using S_{search-key} = r.sid
    for each matching key
        retrieve s
        add (r,s) to result
```

Cost: $|R| + (|R| \times p_R) \times \text{tuple search cost}$

Tuple search cost:
1. B+-tree: 
    - Clustered index:  tree height + 1 I/O (typical)
    - Unclustered: tree height + upto 1 I/O per matching S tuple
2. Hash index: 1.2 + cost of finding S tuples (1 I/O per matching tuple)

### General Join

**Multiple equality conditions**
- SMJ, HJ -> sort / partition on combination of the join columns
- Index NJ -> use existing index on one of the columns, or build a new index on both columns

**Inequality conditions**
- SMJ, NJ -> fine
- HJ -> not suitable

### General Selections

**Terminology**

- **Selectivity** = size of result / $(| R | \times p_R)$. Selectivity of access path: num of pages accessed. Most selective -> lowest selectivity
- **Access path**: ways of accessing data records/entries
    - table scan
    - index-only scan
    - index-search -> might be followed by data records lookup
    - index intersection -> combine result of multiple index traversal
- An index I is a **covering index** of a query Q if Q can be performed using index-only scan on I, i.e. all attributes referenced in Q is in I.
- Index I **matches** predicate p if p have equality conditions on a prefix of I (order matters, no attribute skipped), and at most 1 range condition for a B+-tree index.

**Strategy**

1. Find most selective access path, retrieve tuples using it, then apply remaining conditions that don't match the index
2. If we have more than 1 matching index. Get set of rids using both matching index, intersect, retrieve records, then apply remaining conditions.

### Projection (DISTINCT)

**Sort-based approach**

Optimized step:
1. Create sorted runs with attribute L
2. Merge sorted runs while removing duplicates

$|\pi^*_L(R)| = |R|$ x  size of L / original size of tuple
Unoptimized cost: $|R| + |\pi^*_L(R)|$ + cost of sorting $|\pi^*_L(R)|$ pages + $|\pi^*_L(R)|$
Optimized cost: $|R| + |\pi^*_L(R)|$ (first phase) + $|\pi^*_L(R)| \times \lceil \log_{B - 1}\lceil |\pi^*_L(R)| / B \rceil \rceil$ (second phase)

**Hash-based approach**

1. Partitioning phase: Project out unwanted attribute: t -> t', then apply hash function similar to hash join
2. Joining phase: Read in 1 partition. For each tuple t in partition, insert t into hash table only if it doesn't exist yet. Write out tuples in hash table.

To avoid partition overflow, we need $\large \frac{|\pi^*_L(R)| \times f}{B - 1} < B$, where $f$ is a fudge factor for the hash table. 

Cost: $|R| + |\pi^*_L(R)|$ (partitioning) + $|\pi^*_L(R)|$ (duplicate elimination phase)

**Comment**: Both hash-based and sort-based has same cost if $B > \sqrt{|\pi^*_L(R)| \times f}$

**Using index**

- If the index covers the projection, we can replace table scan with index scan
- If the index is ordered (e.g. B+-tree index), we can scan data entries, and remove adjacent duplicates.

### Set Operations

- Intersection and Cross Product are special cases of join
- Union (Distinct) and Difference are similar
    - Sort based approach similar to external sort. 
    - Hash based approach similar to external hashing / hash join.

### Aggregates

**Without grouping**

Generally involves table scan. If there is a covering index, we can replace with index-only scan.

**With Grouping**

- Sort/Hash on groupby-attributes, then compute aggregates for each group
- If there is a **covering tree** index, we can do an index-only scan.
    - If group-by attributes form prefix of index search key, we can retrieve data entries/records in group-by order.