SMs are oversubscribed to threads. There are a couple of resource limitations that each SM has to balance. An A100 can support:
* 32 blocks per SM
* 64 warps (x32 threads each, 2048 threads total)
* 1024 threads per block
* 65,536
However, you can tell that having 32 blocks of 1024 threads each will exceed the 64 warp limit. 
These resource get dynamically partitioned. If you were to launch a grid with a block size of 512 threads, then each block would receive 2048 thread slots / 512 threads per block = 4 blocks. A block size of 256 would yield 8 blocks, etc.

The amount of warps assigned to a device, compared to the max number of warps it can support, is called *occupancy*. 

The alternative to dynamic partitioning is fixed partitioning. Fixed partition wastes threads when a block needs less threads than the fixed partition's maximum, and cannot support blocks that need more slots at all.

**Underutilization:**
Dynamic partitioning can also lead to underutilization.

**Low threads per block cause block oversaturation**
For example, if you assign each block to 32 threads, you would need (2048 max threads / 32 blocks per thread = 64 blocks) to maximize occupancy, whereas the Volta SM can only support 32 blocks, which leads to a 50% occupancy. 

**Max number of threads not divisible by block size**

2048 max threads / 768 threads per block = 3 blocks, with 1536 threads, leading to a utilization of 75%. In this situation, neither the max blocks nor max threads are reached.

**Registers per thread overuse**

If there are 65,536 total registers per SM, this means that each thread can use 32 registers. If you assign 64 registers per thread, then the  SM will be running on 50% occupancy as it ran out of registers. (65,536 / 64 = 1024 threads used).

If a programmer uses only 32 registers per thread, but assigns an automatic variable in the kernel, then this would still exceed the register limit (2048 threads * 33 registers = 2048 more registers than is supported). This could get handled by only assigning 3 blocks of 512 threads to the SM instead of 4, which would lead to an occupancy of 75%. This extra variable bumped us over a "performance cliff", where "a slight increase in resource usage can result in significant reduction in parallelism and performance" (Ryoo et a. 2008). 
