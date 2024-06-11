#BasicsNode  

[[Grids & Blocks & Threads]]
[[Basics of Coding in CUDA]]
The majority of this text is taken from the NVIDIA docs, section 3.

**CUDA:** Compute Unified Device Architecture
**NVCC:** Nvidia C Compiler

CUDA is an extension of C, and therefore cannot be compiled by a C compiler. Instead, it is compiled using NVCC, which compiles both device-specific and host-specific code. Since the executable will be run on multiple processor types (CPU and GPU) and contains instructions for both processors, it is called a "fat binary".

1. **Device Code:** the program is first preprocessed for device (GPU) compilation into CUDA binaries (`cubin`) and/or PTX intermediate code. They are then placed into a `fatbinary`. 
2. **Host Code:** The the program is then preprocessed a second time for host (CPU) compilation. This is where CUDA specific C++ extensions get translated into standard C++, and embedded into the `fatbinary`.
3. Whenever the host program launches device code, the fatbinary is inspected and a fatbinary for the current GPU is obtained at runtime.

Sources (excl. book): https://docs.nvidia.com/cuda/cuda-compiler-driver-nvcc/index.html
