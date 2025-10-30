# PageExpm.jl
pageexpm on CPU/GPU

## Quick Start

### Install

```julia
# In Julia REPL
] add https://github.com/draftman9/PageExpm.jl.git

# Or use Pkg API
using Pkg
Pkg.add(url="https://github.com/draftman9/PageExpm.jl.git")
```

### Usage

```julia
using PageExpm

A = randn(2, 2, 3)
E, jPwr = pageexpm(A)                # Standard Precision
E_high, jPwr_high = pageexpm(A, RelTol=1e-15, PadeOrder=9)  # High Precision Suggested

# GPU (Requires CUDA.jl)
# using CUDA
# A_gpu = CuArray(A)
# E_gpu, jPwr_gpu = pageexpm(A_gpu)
```

### Validity on CPU

```julia
using LinearAlgebra
using BenchmarkTools
using PageExpm

# validatiy with cpu
println("\n=== validatiy with cpu ===")
a = rand(2,2,3)
E, _ = pageexpm(a)

diff1 = exp(a[:,:,1]) - E[:,:,1]
diff2 = exp(a[:,:,2]) - E[:,:,2]
diff3 = exp(a[:,:,3]) - E[:,:,3]

t1 = sum(abs.(diff1)) < 1e-12
t2 = sum(abs.(diff2)) < 1e-12
t3 = sum(abs.(diff3)) < 1e-12

println(t1)
println(t2)
println(t3)

display(diff1)
display(diff2)
display(diff3)
```

## TODO

1. ✔ Run on CPU
1. ✔ Verify correctness on CPU
1. Run on GPU
1. Verify correctness on GPU
