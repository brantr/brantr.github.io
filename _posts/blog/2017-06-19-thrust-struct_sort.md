---
layout: post
categories: blog
title: Using Thrust to Sort Structures
use_math: true
---

* Table of Contents
{:toc}


## Using Thrust to Sort Structures

{% highlight C %}
#include <thrust/host_vector.h>
#include <thrust/device_vector.h>
#include <thrust/sort.h>
#include <thrust/copy.h>
#include <cstdlib>

struct tracer
{
  long id;
};

struct tracer_comp_by_id
{
  __host__ __device__
  bool operator()(const tracer& a, const tracer& b)
  {
    return (a.id < b.id);
  }
};

int main(int argc, char **argv)
{
  const int N = 6;
  thrust::host_vector<tracer>    A(N);
  thrust::device_vector<tracer> dA;

  //populate host vector
  A[0].id = 9;
  A[1].id = 8;
  A[2].id = 7;
  A[3].id = 6;
  A[4].id = 5;
  A[5].id = 4;

  //copy to device
  dA = A;

  //sort
  thrust::sort(dA.begin(), dA.end(), tracer_comp_by_id());

  //transfer back
  thrust::host_vector<tracer>    B = dA;

  for(int i=0;i<N;i++)
    printf("A[%d].id = %ld\n",i,B[i].id);

  return 0;

}
{% endhighlight %}
