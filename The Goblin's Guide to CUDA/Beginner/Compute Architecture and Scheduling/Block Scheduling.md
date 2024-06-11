4.2
In most cases, multiple blocks will be assigned to the same SM (streaming multiprocessor) for execution. Since a block is assigned to 1 SM, threads in the same blocks can interact in ways that threads on different blocks can, for example, using [[Warps & barrier synchronization]] and [[Shared memory]]. 

Blocks are part of a larger execution concept called a "grid", and a grid can contain many more blocks than the total number of blocks that a GPU can handle. The CUDA runtime is responsible for assigning new blocks to SMs as they complete execution.

By preventing different blocks from interacting with each other, the CUDA runtime can execute blocks in any order. This also means you can execute an arbitrary number of blocks on an arbitrary device size (e.g. smaller or larger GPUs), with no change of code.

Each block is divided into multiple warps. A warp is "the unit of thread scheduling in SMs" (book), and each warp contains 32 threads.

[[Dynamic partitioning and occupancy]]
