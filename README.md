🚀 HPC-RadixSort: Non-Atomic Parallel Radix Sort for C++

A High-Performance, Linear-Time Sorting Solution for 64-bit Integers

HPC-RadixSort is a specialized C++ library designed for performance-critical applications that require the fastest possible sorting of large arrays of fixed-width integers (specifically long long). This implementation leverages OpenMP for highly efficient parallel execution, achieving near-linear time complexity $O(n)$ with minimal synchronization overhead. 

Key Technical Advantages

This is not a general-purpose library sort. It is engineered for low latency and high throughput in HPC and Big Data environments.

Non-Atomic Distribution (Zero Lock Contention):

Unlike many parallel sorting algorithms that rely on expensive atomic operations or critical sections during the distribution phase, this implementation uses a sophisticated block-partitioning and prefix-sum-based offset calculation.

This ensures that each thread writes to a guaranteed non-overlapping section of the output array, achieving true parallelism in the final step.

Linear Time Complexity:

Since Radix Sort is a non-comparison algorithm, its complexity is $O(k \cdot n)$, where $k$ (the number of passes/chunks) is a small constant for 64-bit integers.

By dividing the work across $p$ cores, the effective runtime scales as $O(k \cdot n / p)$, making it exceptionally fast for massive datasets.

Optimization Focused:

Utilizes a base $B=512$ (9 bits) to minimize the number of passes required.

Employs manual loop unrolling (UNROLL = 4) during the counting phase to maximize instruction-level parallelism.

📦 Usage and Compilation

Prerequisites

A C++ compiler supporting the C++11 standard or later (e.g., GCC, Clang).

OpenMP support enabled in the compiler.

Compilation

Compile the source file (chunked_radix_sort.cpp) using the OpenMP flag:

# Compile with g++
g++ -std=c++17 -O3 -fopenmp chunked_radix_sort.cpp -o hpc_radix_sort

# Run the executable
./hpc_radix_sort


API Reference

The core sorting function is a single, in-place utility:

void chunked_radix_sort(vector<long long>& arr);


Parameter

Type

Description

arr

std::vector<long long>&

The vector of non-negative 64-bit integers to be sorted. Sorting is performed in-place.

(Note: The current version supports non-negative integers only. A commercial update is planned for full signed integer support.)

📈 Performance Benchmarks (Placeholder)

NOTE: These are representative performance goals. Actual data to be updated after rigorous testing.

Dataset Size (N)

Algorithm

Average Time (Seconds)

Speedup vs. std::sort

$10^7$ Random Integers

std::sort (1 Thread)

0.85s

$1.0x$

$10^7$ Random Integers

HPC-RadixSort (8 Threads)

0.15s

$5.6x$

$10^8$ Random Integers

HPC-RadixSort (8 Threads)

1.45s

TBD

⚖️ Licensing

HPC-RadixSort is available under a Dual Licensing Model to suit various development needs:

Open Source License: Available for educational use, non-commercial research, and internal company evaluation.

Commercial License: Required for all companies and organizations integrating this code into proprietary, closed-source products intended for distribution or sale. Please contact us for pricing on Perpetual, Annual Subscription, and Site Licenses.
