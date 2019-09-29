## Building a Bw-Tree Takes More Than Just Buzz Words

Bw-Tree (Buzz Word Tree) is a lock-free index that provides
high throughput for transactional database workloads,
originally proposed by Microsoft Research in 2013.

### Problems Identified

Building lock-free indexes is notoriously difficult as
- It requires identifying all possible race conditions
- Incorrect implementations result in busy-waiting loops
- Requires safe memory reclamation and
- Careless use of atomic primitives introduce bottlenecks

### Contributions

Bw-Tree is a data structure that uses an indirection layer
(that allows mapping logical identifiers to physical pointers
for the tree's internal components) and per-node delta records
to allow concurrent accesses to the data without locks.
This paper:
- Discusses the design and implementation of a BwTree,
open sourced at [Open-BwTree](https://github.com/wangziqi2013/BwTree#open-bwtree--)
- Evaluates the overheads of the indirection layer and
delta records placing it in context with lock-based indexes.

### Outline

1. BwTree: Design
2. Implementation Details
3. Optimizations
4. Evaluation

### Bw-Tree: Design and Implementation

The prominent differences between Bw-Tree and other
B+Tree-based indexes is that the Bw-Tree

- Stores modifications to a node (e.g., insert, update, delete),
in a delta record and maintains a chain of such records,
called the **delta chain**, per node to
avoid cache line invalidations due to inplace node updates,
and to perform atomic updates via Compare and Swap (CaS).

- Has an indirection layer with a **mapping table** that maps
logical node IDs to physical pointers, making atomic updates
of several references to a tree node possible.


- Node has the base nodes: (key, nodeID) array or (key, value),
and the delta chain. Delta chain is a singly linked list of
chronologically-ordered history of modifications to base nodes.
The entries in the delta chain are connected using physical
pointers with the tail pointing to the base node.

- Bw-Tree nodes and delta records store additional node metadata
as shown ![Table-1](https://github.com/SoujanyaPonnapalli/PMemory/blob/master/Figures/BwTree/Table1.png).

- Has centralized mapping table and centralized garbage collection.

### Implementation Details

- Add support for unique keys
- Iterators for traversing Bw-Tree
- Mapping Table resize

### Optimizations

- Delta record pre-allocation
- Epoch based GC to decentralized GC
- Fast delta chain consolidation
- Node search shortcuts

### Evaluation

Please refer the paper for the complete evaluation of [Bw-Trees](https://db.cs.cmu.edu/papers/2018/mod342-wangA.pdf).
