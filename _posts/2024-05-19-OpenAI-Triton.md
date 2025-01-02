---
layout: post
title: OpenAI Triton
date: 2024-05-19
description: Triton language
selected: true
---

1. **Simple Vector addition**
    - One limitation of Triton: `BLOCK_SIZE` must be a power-of-2

    ```python
    ''' Simple Vector addition '''
    import torch
    import triton
    import triton.language as tl

    @triton.jit
    def add_kernel(x_ptr,
                   y_ptr,
                   output_ptr,
                   n_elements,
                   BLOCK_SIZE: tl.constexpr): # 'constexpr' so it can used as a shape value. ??
        
        pid = tl.program_id(axis=0)
        print(pid) # refer to image below for total number of prints

        block_start = pid * BLOCK_SIZE
        offsets = tl.arange(0, BLOCK_SIZE)
        mask = block_start + offsets < n_elements

        x = tl.load(x_ptr + block_start + offsets, mask=mask)
        y = tl.load(y_ptr + block_start + offsets, mask=mask)
        output = x + y
        tl.store(output_ptr + block_start + offsets, output, mask=mask)

    size = 10
    x = torch.rand(size, device='cuda')
    y = torch.rand(size, device='cuda')
    output = torch.empty_like(x)

    # grid = lambda meta : (tl.cdiv(size, meta['BLOCK_SIZE']), ) # Error: cannot call @triton.jit'd outside of the scope of a kernel
                                                                 # tl.cdiv cannot be compiled outside the kernel without @triton.jit
    grid = lambda meta : (triton.cdiv(size, meta['BLOCK_SIZE']), )
    add_kernel[grid](x, y, output, size, BLOCK_SIZE=4, num_warps=1)

    print(output)

    ```
    ```python
    print("pid: ", pid)

    # Total number of programs = 3
    # Each program will be printed: num_warps * warp_size
    # Total number of prints: num_programs * (num_warps * warp_size)
    ```
    Vector add illustration:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/openAI-Triton/vector_add.jpg" title="vector_add image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>


2. **Simple Matrix Multiplication**
    - 4x4 Matrix: `tl.arange(0,4)[:, None] + tl.arange(0,4)[None, :]`
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/openAI-Triton/matmul.jpeg" title="vector_add image" class="img-fluid rounded z-depth-1" %}
        {% include figure.html path="assets/img/openAI-Triton/stride.jpeg" title="vector_add image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

3. Que: How to print tensor's shape from inside the triton kernel?
