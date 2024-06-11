A warp is "the unit of thread scheduling in SMs". Each warp consists of 32 threads, and blocks, once assigned to an SM, divide into warps. If each block contains 256 threads, we can determine that each block divides into 256/32 = 8 warps.

Recall that blocks are arranged into potentially >1 dimensional arrays. A 1 dimensional block of 32 threads (1 warp) would cause the thread indices (`threadIdx`) to be numbered from 0 through 31 inclusive.
TODO: Add img
Multi-dimensional blocks need to be linearized into a row-major layout before being divided into warps. For example, linearizing a 3 dimensional block (x,y,z axes) would first increment the x axis, then the y axis, then the z axis:
```python
for z in range(Z):
	for y in range(Y):
		for x in range(X):
			print(f'{x=} {y=} {z=})
```
If a warp does not contain enough threads for its size (e.g. only 16/32), threads will be used to pad it until it is full.

**Barrier synchronization:**  (4.3)
Sometimes, you want to wait for all threads in a block to finish executing some code before moving on. To do this, you can use `__syncthreads()` . This is called barrier synchronization.

`__syncthreads()` pauses execution of each thread at the call until *all* threads in the same block reach the same `__syncthreads()` call. This also means that threads that take excessively long to execute can delay other threads, and should be a performance consideration.

For example, if you and three other ~~threads~~ friends are shopping at the mall, each of you can shop independently (at different locations) but would need to `__syncfriends()` right before you leave the mall to go back home.

When `__syncthreads()` is placed in an if statement, you risk only some threads reaching the barrier based on the predicate, which could lead to a dead-lock:
```cpp
if (threadIdx.x % 2 == 0) {
	...
	__syncthreads();
} else {
	...
}
```
In the above example, it's easy to see how half the threads will never sync and the kernel will be deadlocked.

Threads can also be deadlocked if they are not assigned enough execution resources to arrive at the barrier. This is avoided by assigning resources to all threads in a block at once (no thread gets left behind). This also helps ensure that thread execution takes a similar time per block (all resources are provided for at the start)

**Whenever you assume that certain threads should execute synchronously with others, you should use barrier synchronization.**

[[Warp scheduling]]