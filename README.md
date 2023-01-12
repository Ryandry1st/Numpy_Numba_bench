# Numpy Numba bench
Benchmarks for comparing computational operations (in python) across hardware.

This project came out of realizing that AMD and Intel processors are still significantly different in performance even in 2023 when it comes to numpy/BLAS/LAPACK operations. I still find that AMD processors are slower than Intel in this regard, which is a significant disadvantage given market share rise and hardware superiority (in specific cases).

In my case, I find that a desktop 5950x is performing roughly on par with a mobile 10800H when it comes to logic + linalg. This is completely unexpected as CPU and memory benchmarks show almost 2x higher performance in multithreaded operations. Digging into it, I find that although singular linalg is slightly faster (maybe 20%), the gains do not extend when combining linalg with logic. 
