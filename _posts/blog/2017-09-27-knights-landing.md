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
* Use "_mm_malloc()" and "_mm_free"
* use "__assume_aligned(a,64)" before a loop__
* Also "#pragma vector aligned"
* Use after "#pragma omp parallel for"
* Data alignment information on page 181
* Example using assume aligned directive:
{% highlight c %}
void myfunc(double p[])
{
  __assume_aligned(p,64);
  for(int i=0;i<n;i++)
  {
    p[i]++;
  }
}
void myfunc2(double *p2, double *p3, double *p4, int n)
{
  for(int j=0;j<n;j+=8)
  {
    __assume_aligned(p2,64);
    __assume_aligned(p3,64);
    __assume_aligned(p4,64);
    p2[j:8] = p3[j:8]*p4[j:8];
  }
}
{% endhighlight %}
* Example where all data is aligned in loop:
{% highlight c %}
#pragma vector aligned
for(i=0;i<n;i++)
  A[i] = B[i]*C[i]+D[i];
#pragma vector aligned
A[0:n] = B[0:n]*C[0:n]+D[0:n];
{% endhighlight %}

## General Programming Advice
* Manage Domain Parallelism
* Increase Thread Parallelism
* Exploit Data Parallelism
* Improve Data Locality

## Environmental Variables
* KMP_AFFINITY=SCATTER to distribute threads across cores
* KMP_STACKSIZE=16MB instead of standard 12MB
* KMP_BLOCKTIME=Infinite to prevent threads from sleeping
* There are other OMP variables for nested threads, for future reference.

## Vectorization
* Autovectorization using -O2 or -O3
* Compiler optimization report add "-qopt-report -qopt-report-phase=loop,vec"
* Avoid gather/scatter, instead align and pack memory
* Fetch from cache, not memory.  Prefetch to L2, then prefetch from L2 to L1.  Look at "mm_prefetch".
* Re-use data in cache if possible.
* If data is being written out and will not be re-used, use streaming stores to prevent evictions from cache.  Data must occupy linear memory without gaps.
* Avoid manual loop unrolling.
* SIMD directives on page 193
* Vectorization may not produce numerically identical results to scalar operations, especially in reductions.  Use "-fp-model precise" to prevent vectorization of reductions (and other things).

## Prefetching
* Compiler prefetching via "-opt-prefetch=n". Automatically set to n=3 with -Ox.
* Pragma hint "#pragma prefetch var:hint:distance". hint=0 (L1 and L2) or hint=1 (L2)
* "__mm_prefetch(char const *address, int hint)"*__ Loads one cache line of data at address.
* Too many prefetches are problmeatic.  Can disable compiler prefetching with "-opt-prefetch=0"
* Disable compiler preftech with "#pragma noprefetch" within loop.
* Example code on page 184

## Streaming Stores
* Compiler options "-opt-streaming-stores keyword" auto always never, auto default.
* Streaming stores from a loop can only be determined at runtime, so variable loop iterations need "#pragma vector nontemporal"

## Loop Vectorization Requirements
* Inner loop in a loop nest.
* Straight-line code, no jumps or branches, but can mask with if statement.
* Must be countable, with no data-dependent exit conditions.
* No backward loop-carried dependencies. a[i] must be computed before a[i-1] is used.
* No special operators, functions, or subroutines called.
* Intrinsic math functions such as sin(), log(), and fmax() are OK.
* Following math functions OK: sin, cos, tan, asin, acos, atan, log, log2, log10, exp, exp2, sinh, cosh, tanh, asinh, acosh, atanh, erf, erfc, erfinv, sqrt, cbrt, trunk, round, ceil, floor, fabs, fmin, fmax, pow, and atan2.
* Reductions and vector assignments OK.
* Avoid mixed data types.
* Use contiguous memory locations, with unit stride.
* Use ivdep to advise that there are no loop-carried dependencies.
* Use vector always pragma to force vectorization.
* Check vectorization report.

## Compiler options for Vectorization
* "-ansi-alias"
* "-restrict" Allows restrict to be used as a keyword in C.

{% highlight c %}
void vectorize( float *restrict a, float *restrict b, float *c, float *d, int n)
{
  /* Ensure that compiler knows a and b do not overlap*/
  int i;
  for(i=0; i<n; i++)
  {
    a[i] = c[i] * d[i];
    b[i] = a[i] + c[i] - d[i];
  }
}
{% endhighlight %}

## Vector Directives: ivdep
* The following would not vectorize without ivdep since the value of k is not known and could be k<0.
{% highlight c %}
void ignore_vec_dep(int *a, int k, int c, int m)
{
  #pragma ivdep
  for(int i=0;i<m;i++)
  {
    a[i] = a[i+k]*c;
  }
}
{% endhighlight %}

## Vectorization of Random Numbers
* drand48, erand48, lrand48, nrand48, mrand48, and jrand48 can be vectorized.
* Example:

{% highlight c %}
#include <stdlib.h>
#include <stdio.h>
#define ASIZE 1024
int main(int argc, char **argv)
{
  int i;
  double rand_number[ASIZE] = {0};
  unsigned short seed[3] = {155,0,155};
  // Initialize Seed Value for Random Number
  seed48(&seed[0]);
  for(i=0;i<ASIZE;i++)
  {
    rand_number[i] = drand48();
  }
  //Print Sampel Array Element
  printf("%f\n", rand_number[ASIZE-1]);
  return 0;
}
{% endhighlight %}

# Optimization and Profiling
* Use "-xCOMMON-AVX512"
* For profiling, use "-g"
* Survey usage:
- Set environment variable: "source /opt/intel/advisor_xe_2016/advixe-vars.sh"
- Collect Survey data: "advixe-cl --collect-=survey --projectdir=<project_dir> --<target_application>"
- Launch the advisor gui: "advixe-gui <project_directory>"
- Output answer data is usually e000 or something similar.
* Information on Vectorization Advisor on page 217


## AVX-512 Intrinsics

Perform operations on packed 8 doubles or 16 singles in 512 bit chunks. Other data types available, and 4 element w Provides vectorized add, subtract, multiply, divide, and FMA.  See the following code from Jeffers et al.:

{% highlight c %}
#include <stdio.h>
#include "immintrin.h"
void print(char *name, float *a, int num)
{
  int i;
  printf("%s = %6.1f",name,a[0]);
  for(i=1;i<num;i++)
  {
    printf(",%s%4.1f",(i&3)?"":" ",a[i]);
    printf("\n");
  }
}
int main(int argc, char *argv[])
{
  float a[] = {9.9, -1.2, 3.3, 4.1,  -1.1, 0.2, -1.3, 4.4,   2.4, 3.1, -1.3, 6.0,   1.5, 2.4, 3.1, 4.2 };
  float b[] = {0.3,  7.5, 3.2, 2.4,   7.2, 7.2,  0.6, 3.4,   4.1, 3.4,  6.5, 0.7,   4.0, 3.1, 2.4, 1.3};
  float c[] = {0.1,  0.2, 0.3, 0.4,   1.0, 1.0,  1.0, 1.0,   2.0, 2.0,  2.0, 2.0,   3.0, 3.0, 3.0, 3.0};
  float o[] = {0,0,0,0, 0,0,0,0, 0,0,0,0, 0,0,0,0};

  __m512 simd1, simd2, simd3, simd4;
  __mmask16 m16z = 0;
  __mmask16 m16s = 0xAAAA;
  __mmask16 m16a = 0xFFFF;
  print("  a[]",a,16);
  print("  b[]",b,16);
  print("  c[]",c,16);
  if(_may_i_use_cpu_feature(_FEATURE_AVX512F))
  {
    simd1 = _mm512_load_ps(a);
    simd2 = _mm512_load_ps(b);
    simd3 = _mm512_load_ps(c);
    simd4 = _mm512_add_ps( simd1, simd2);
    _mm512_store_ps(o,simd4);
    print("  a+b",o,16);
    simd4 = _mm512_sub_ps(simd1,simd2);
    _mm512_store_ps(o,simd4);
    print("  a-b",o,16);
    simd4 = _mm512_mul_ps(simd1,simd2);
    _mm512_store_ps(o,simd4);
    print("  a*b",o,16);
    simd4 = _mm512_div_ps(simd1,simd2);
    _mm512_store_ps(o,simd4);
    print("  a/b",o,16);
    printf("FMAs with mask 0, then mask 0xAAAA, then mask 0xFFFF:\n");
    simd4 = _mm512_maskz_fmadd_ps(m16z,simd1,simd2,simd3);
    print("a*b+c",(float *)&simd4, 16);
    simd4 = _mm512_maskz_fmadd_ps(m16s,simd1,simd2,simd3);
    print("a*b+c",(float *)&simd4, 16);
    simd4 = _mm512_maskz_fmadd_ps(m16a,simd1,simd2,simd3);
    print("a*b+c",(float *)&simd4, 16);   
  }
  return 0;

}
{% endhighlight %}

Note the casting of the simd 512 bit data types when passing to a function.

## Intel Intrinsics Guide

Here is the [Intel Intrinsics Guide](https://software.intel.com/sites/landingpage/IntrinsicsGuide/).
