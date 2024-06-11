 #HighLevelNode 
 [[Basics of Coding in CUDA]]
 
 Phenomena where computation can be done on one part of the data independently of other parts of the data.

Parallel programming exploits this property to execute tasks much faster, by using threads & processes to execute said computations in parallel.

Data parallelism is when 1 task can be decomposed into many of the same operation, and thus executed in parallel.
Task parallelism is when multiple tasks can be done independently, and thus executed in parallel.

**Task parallelism:**

I/O streams and data transfer while data is being processed.
A family cook-out.
Assembling a bed frame.

**Data parallelism:**


Pair-wise operations on two vectors.
Image filters (e.g. grayscaling)
Matrix multiplication
Ray tracing across multiple pixels
Frying 100 eggs
If it takes 1 chicken 24 hours to lay an egg, how long would it take 10 chickens to lay 10 eggs?

No data parallelism:

If it takes 1 chicken 24 hours to lay an egg, how long would it take 10 chicken to lay 1 egg?

No task parallelism:

Database write transactions. 
Baking a cake.
Turn based games

---
Often it is less clear how tasks can be decomposed to become task or data parallel.

[[CPU (host) vs. GPU (device)]]