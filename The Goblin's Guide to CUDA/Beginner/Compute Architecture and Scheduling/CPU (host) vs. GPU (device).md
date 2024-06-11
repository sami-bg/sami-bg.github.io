#HighLevelNode

**CPU:**
The CPU is a serial machine, and its goal is to execute serial instructions very quickly. This involves  executing conditional logic, scheduling processes, interrupting processes, and more. Because of this, much of the design of CPU chips involves deep cache hierarchies, branch prediction, fast clock speed, and comparatively little arithmetic (done by ALUs: arithmetic logic units).

**GPU:**
In comparison, the GPU is a high throughput and high bandwidth machine. It has an abundance of ALUs and comparatively few caches.

The "device" and "host" operate asynchronously, with the programmer explicitly moving data between the two. This is often a key optimization consideration, as moving bytes to and from GPU memory is expensive. The programmer is responsible for allocating memory to both the device and the host (e.g. malloc and cudaMalloc) either statically or dynamically.

The CPU, being the host (the "central" processing unit), queues kernel tasks on the device. Once the task is complete, the host can copy data back from the device (cudaMemCpy).

Another key difference is in how both CPUs and GPUs handle thread scheduling. When multiple threads share a single processor in a CPU, context switching between threads requires restoring the program counters, register contents, and memory, which incurs significant overhead.

GPUs allow for "zero overhead scheduling" -  which allows GPUs to put to sleep/awaken threads with no overhead, by storing execution states of groups of threads (warps) in hardware registers instead of memory. An important consequence of this is that it enables GPU cores to oversubscribe to threads, which is crucial for latency tolerance. See 

https://www.youtube.com/watch?v=lGmPy8xpT4E&ab_channel=ArgonneMeetings%2CWebinars%2CandLectures 
Links:
[[GPU Architecture]]
[[SIMD in GPUs]]
