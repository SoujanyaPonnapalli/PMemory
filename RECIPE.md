#### RECIPE: Converting Concurrent DRAM Indexes to Persistent-Memory Indexes.

Designing persistent memory indexes from scratch is challenging as these indexes must
provide high performance and concurrency while ensuring crash consistency.

Modern in-memory data structures are carefully designed keeping in mind cache efficiency,
prefetching, concurrency, and parallelism via SIMD instructions. RECIPE leverages the research
on concurrent in-memory indexes to build crash-consistent indexes for persistent memory.

**Goals:**
- To convert concurrent DRAM indexes to crash-consistent PM indexes
- Isolation provided by concurrent indexes can be translated to crash-consistency

**Insights and Findings:**
- Crash consistency bugs in existing PM indexes
- There is a need for both principled design of PM indexes, and testing if PM indexes
recover correctly from crashes.

**Outline:**
- What class of concurrent in-memory indexes can be converted to PM indexes?
- How can a concurrent index be converted into a crash consistent PM index?
- The case study of five PM indexes designed using RECIPE

**RECIPE:**

correctness: No previously inserted key is lost and a search returns the latest value
of the key.



**Results:**

Please revisit the paper to read more about the performance benefits achieved by the
PM indexes built using [RECIPE](https://www.cs.utexas.edu/~vijay/papers/sosp19-recipe.pdf).


**[TODO] PM-indexes:**
  - FAST & FAIR
  - Level Hashing
  - CCEH
  - NV-Tree
  - wB+ tree
  - WOART
  - FPTree
  
 **[TODO] Concurrent in-memory indexes:**
  - latch-free BwTree
  - Adaptive Radix Trees
  - Timeline Index
  - Masstree
  
