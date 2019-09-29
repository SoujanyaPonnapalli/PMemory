## Building a Bw-Tree Takes More Than Just Buzz Words

BwTree (Buzz Word Tree) is a lock-free index that provides
high throughput for transactional database workloads,
originally proposed by Microsoft Research in 2013.

### Problems Identified

Building lock-free indexes is notoriously difficult as
- It requires identifying all possible race conditions
- Incorrect implementations result in busy-waiting loops
- Requires safe memory reclamation and
- Careless use of atomic primitives introduce bottlenecks

### Contributions

BwTree is a data structure that uses an indirection layer
(that allows mapping logical identifiers to physical pointers
for the tree's internal components) and per-node delta records
to allow concurrent accesses to the data without locks.
This paper:
- Discusses the design and implementation of a BwTree,
open sourced at [Open-BwTree](https://github.com/wangziqi2013/BwTree#open-bwtree--)
- Evaluates the overheads of the indirection layer and
delta records placing it in context with lock-based indexes.

### Outline

1. BwTree: Design and Implementation
3. Evaluation
