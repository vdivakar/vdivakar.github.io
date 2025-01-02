---
layout: post
title: Notes CUDA
date: 2022-12-11
description: self-notes
selected: true
---

Notes for CUDA

1. Setting grid and block dimensions
    - Un-initialized dimension (.x, .y, .z) is set to 1 by default.
    ```C++
    dim3 grid (1024, 8);
    dim3 block (512, 1);
    myKernel<<<grid, block>>>(d_data);
    ```

2. Don't do this:
    ```C++
    dim3 grid = (1024, 8); // !!!! Wrongly initialised values!!!!
    ```

3. Max of threads in a cuda block: 1024
    - This is the total number of threads, not per dimension!

4. GPU -> many Streaming Multiprocessors (SMs) -> each with a control, Memory and many Cores
    - Each ThreadBlock is assigned (fully) to one of the SMs i.e. all the threads in a ThreadBlock go to the same SM
    - Threads in the same ThreadBlock can collaborate with each other:
        - Barrier synchronization: __syncthreads()
        - Shared memory
    - Threads in different blocks don't synchronize.
        - Hence, blocks can execute in any order say, sequentially or parallely w.r.t each other
        - Hence, same code can run on a different hardware with few or more SMs accordingly.