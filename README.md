# EPCC-OpenMP-micro-benchmarks
A fork of the EPCC OpenMP micro-benchmark suite with some improvements

If you just want the original, you can download it here:
https://www.epcc.ed.ac.uk/research/computing/performance-characterisation-and-benchmarking/epcc-openmp-micro-benchmark-suite

## Some notes on parameter tuning for `schedbench`

To truly measure the overheads of for-loop scheduling, it is important that most of the time is spent inside the parallel for-loop. and that not too many loops are created. The default parameters had a tendency to create too many parallel for-loops, which meant that the overhead of creating loops dominated the overhead of chunk scheduling. To check if this is happening to you, one method is to see if there is any significant difference between the overheads measured for dynamic loops with chunk-size 1 and 2. The loop with chunk-size 1 should consistently get a higher overhead, as seen in the results of [1].

If you believe that your current parameters do not allow accurate measurements of scheduling overheads, you can try:
- Increasing `itersperthr`, found in `schedbench.c` and rebuild
- Use a lower delay time via the command line argument `--delay-time`. For instance, try 0.1.

# References
- [1] Bull, J. Mark. "Measuring synchronisation and scheduling overheads in OpenMP." *Proceedings of First European Workshop on OpenMP*. Vol. 8. 1999.