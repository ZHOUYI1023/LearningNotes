* faster training
* efficient serving
* lower memory consumption

###Deep Learning System Stack
**User API:**
==Programming API==
==Gradient Calculation (Differentiation API)==

Computation Graph
* nodes represent the operation
* edges represent the data dependency between operations

**System Components**
==Computational Graph Optimization and Execution==
==Runtime Parallel Scheduling==
deadcode elimination
memory planning and optimization
detect and schedule parallelizable patterns

**Architecture**
==GPU Kernels, Optimizing Device Code==
==Accelerators and Hardwares==

### Backpropagation and Automatic Differentiation
- numerical differentiation
    - tool to chcek the correctness of the implementaion
- Backpropagation
    - You always need to keep intermediate data in the memory during the forward pass in case it will be used in the backpropagation
    - Lack of flexibility, e.g. compute the gradient of gradient.
- Automatic differentiation
    - generate gradient computation to entire computation graph
    - better for system optimization

### GPU Programming
CPU Vector Operations (SSE/AVX)
GPU  Architecture
Streaming Multiprocessor(SM)
Memory Hierarchy
CUDA Programming Model: SIMT
- threads are grouped into a block
    - threads within the same block can synchronize execution
- blocks are grouped into a grid
    - blocks are independently scheduled on the GPU, can be executed in any order
- a kernal is executed as a grid of blocks of threads
    - each block is executed by one SM and does not migrate
    - several concurrent blocks can reside on one SM 

GEMM

### Optimize for Hardware Backends