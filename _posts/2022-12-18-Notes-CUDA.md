---
layout: post
title: Notes CUDA
date: 2022-12-11
description: self-notes
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