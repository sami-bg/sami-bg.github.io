**SIMD**: Single instruction, multiple data. Each one instruction fetched is executed multiple pieces of data.

In the context of a GPU, it is executed on multiple threads, and the thread's indices map it to the relevant data. 

In a GPU, 8 CUDA cores in an SM are grouped into 1 processing block and share 1 instruction.

Because the control hardware (fetch/dispatch unit) is shared across multiple cores, a smaller percentage of GPU hardware is dedicated to control and more are dedicated to ALUs (Arithmetic Logic Units):

TODO Show photo




































fetch/dispatch unit.
