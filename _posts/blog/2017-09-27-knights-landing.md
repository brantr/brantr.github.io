---
layout: post
categories: blog
title: Knights Landing Notes
use_math: true
---

* Table of Contents
{:toc}


## Transformation for Performance

Quoting from Jeffers, Reinders, and Sodani:

* Memory access and loop transformations (e.g., cache blocking, loop unrolling, prefetching, tiling, loop interchange, alignment, affinity).
* Vectorization works best on unit-stride vectors (the data being consumed is contiguous in memory). Data structure transformations can increase the amount of data accessed with unit-strides (such as Array of Structures to Structure of Arrays transformations or recoding to use packed arrays instead of indirect accesses).
* Use of full (not partial) vectors is best, and data transformations to accomplish this should be considered.
* Vectorization is best with properly aligned data.
* Large page considerations (we recommend the widely used Linux libhugetlbfs library).
* Algorithm selection (change) to favor those that are parallelization and vectorization friendly.

## Turning off and on vectorization

* To turn off vectorization: -no-vec-no-simd
* When using vectorization, use at least: -O2 -xhost

## Architecture notes
* Each processor consists of dozens of tiles.
* Each tile has 2 cores, 2 vector processing units per core, and 1MB L2 cache. And a caching/home agent.
* L2 cache is coherent across tiles.
* Aggregate bandwith on 2D mesh interconnect is 700 GB/s.
* Cluster modes may affect performance when using more than 1 MPI rank per processor.
* There are 8 MCDRAM devices, each with 2GB. Aggregate bandwidth is 450GB/s.
* MCDRAM can be cache, flat (standard memory), or hybrid.
* Aggregate DDR bandwidth from 6 channels is 90GB/s.

## MCDRAM and Cluster Modes
* MPI+OpenMP may run faster with SNC-4 cluster mode than Quadrant
* Hard to beat performance in MCDRAM Cache mode
* Many applications will run fine in Quadrant+Cache
* Most applications will benefit from parallelism more than cluster and mcdram mode fiddling.
* Key difference in Quadrant vs. SNC is whether MCDRAM and DDR are UMA or NUMA.
* For SNC, applications must be NUMA aware and divided into multiple MPI ranks per processor.
* Two-way modes have higher latency.  Use quadrant or SNC-4.
* When using more than 16GB, using MCDRAM as non-cache might be better.
* Memory usage model summary on page 29.
* numactl -H will print information on memory mode
* numastat can provide additional information
* setKNLmodes script on page 59 can help with setting the cluster and memory modes
* SNC-4 is analogous to a 4-socket Intel Xeon system (p75)

## Cache performance
* L1 cache is 16KB per core
* L2 cache is 1MB per tile, or about 512KB per core.
* Performance degrades exponentially across each cache memory utilization (L1->L2->MCDRAM)
* DDR is exponentially worse than MCDRAM (see figure 3.4 on page 32)

## NUMACTL and memory allocations
* numactl -m 1 program will force a program to run in MCDRAM
* numactl -p 1 program will enable a program to run in MCDRAM
* See page 38 for an example
* memkind enables C++ to override new to allocate directly into MCDRAM
* In cache mode, memkind cannot be used because hbw_check_available() will return 0.

## Tile Architecture
* Each VPU can execute 512-bit vector multiply-add instructions per cycle
* Each core can therefore do 32 dual-precision FP ops per cycle
* Cores share the L2 cache read and write bandwidth
* AVX-512 registers are 8 DP wide (512 bits)
* Using two threads per core usually provides maximum performance

## Performance recommendations
* Use static libraries
* Put "export LD_PREFER_MAP_32BIT_EXEC=1" in bashrc
* Use 2M or 1G pages.
* Avoid SSE instructions.
* Reference multiple pointers before deferencing the first.
* Use AVX-512 instructions.

## Vector Operation Costs
* Simple math, load, and stores have cost 1
* Gather for 8 or 16 elements have 14 or 20 cost
* Horizontal reductions have cost 30
* Division or square roots have cost 15
* See examples on pages 122-123.

## Data Alignment
* [Data Alignment to Assist Vectorization](https://software.intel.com/en-us/articles/data-alignment-to-assist-vectorization)
* Use "_mm_malloc()" and _mm_free
* use "__assume_aligned(a,64)" before a loop
* Also "#pragma vector aligned"
* Use after "#pragma omp parallel for"


## General Programming Advice
* Manage Domain Parallelism
* Increase Thread Parallelism
* Exploit Data Parallelism
* Improve Data Locality





