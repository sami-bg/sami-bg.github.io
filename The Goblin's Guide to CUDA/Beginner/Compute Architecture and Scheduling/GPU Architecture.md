#HardwareNode  

GPUs are a throughput-maximization machine, while CPUs are a serial execution machine. GPUs have been designed for the data/task parallel problem regime.

Modern GPUs are organized into arrays of 'streaming multiprocessors' (SMs), each of which contain multiple streaming processors, also called CUDA cores. 
Each GPU also has memory (DRAM).

| GPU  | SMs | CUDA Core per SM | core per SM |
| ---- | --- | ---------------- | ----------- |
| 4090 |     |                  |             |
| A100 | 108 | 6912             | 64          |
| H100 |     |                  |             |
|      |     |                  |             |


[[CUDA and NVCC]]
[[SIMD in GPUs]]
[[Grids & Blocks & Threads]]
[[Block Scheduling]]
