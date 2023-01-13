# Numpy Numba bench
Benchmarks for comparing computational operations (in python) across hardware.

This project came out of realizing that AMD and Intel processors are still significantly different in performance even in 2023 when it comes to numpy/BLAS/LAPACK operations. I still find that AMD processors are slower than Intel in this regard, which is a significant disadvantage given market share rise and hardware superiority (in specific cases).

In my case, I find that a desktop 5950x is performing roughly on par with a mobile 10800H when it comes to logic + linalg. This is completely unexpected as CPU and memory benchmarks show almost 2x higher performance in multithreaded operations. Digging into it, I find that although singular linalg is slightly faster (maybe 20%), the gains do not extend when combining linalg with logic. 








EDIT: After some significant digging, I found that SIMD instructions in numpy are to blame. Switching to using intel MKL on AMD hardware still was advantageous (~20% improvement), but the real benefit came from switching MKL to only single-threaded, which provided about 3x speedup. Then, the loops can be parallelized with Numba to achieve another ~6x additional speeds. Note that tuning the number of threads with Numba is critical as using more than about 8-12 threads actually slowed the results down by a fair margin (maybe reduces gains to about 4x vs 6x).
