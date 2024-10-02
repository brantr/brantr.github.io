---
layout: post
categories: blog
title: Cholla-PM Tests on Summit
use_math: true
---

* Table of Contents
{:toc}


# Cholla-PM Tests on Summit

This website documents the procedure for performing the Cholla-PM tests on Summit.

## Changes to Cholla-PM for Summit Tests

Currently, we are lacking an initial conditions generator for Cholla for tests
at scale. The issue is that we have been using MUSIC, which does not use MPI
and therefore is limited to a single system memory.

This issue is compounded by the need to run on arbitrary even numbers of processes
without keeping a cubic domain.  We can subdivide a single cubic initial conditions,
but that would require a large number of particles and a reduced timestep (for the
hydro).

The plan instead is to simply replicate either a 128^3 or 256^3 box onto every process
and use a computational domain that maps onto the domain of mpi processes determined
via the usual functions in Cholla.  This would make rectangular domains.

I have gone through the code and added "TILING" preprocessor definitions that
alter the behavior of the code.  Basically I have each process read in a single
snapshot + particle file and replicate it locally, shifting appropriately for the
processor location within the domain.  This also requires simlinks to be created
for each process to the single snapshot files, in the "0.h5.?" and "0_part.h5.?"
formats.

## Installation and Tests on Sparkle

First, I installed and tested Cholla-PM on sparkle. Here is the procedure

### Get Cholla-PM
```
git clone https://github.com/bvillasen/cholla.git
cd cholla
git checkout -b particles
git pull origin particles
```

#### Note we will build from the cholla-pm.tiling.tar.gz tarball on Summit.

### Install FFTW-3.3
```
wget http://www.fftw.org/fftw-3.3.7.tar.gz
tar -zxvf fftw-3.3.7.tar.gz
cd fftw-3.3.7/
./bootstrap.sh
./configure --enable-mpi --enable-openmp --enable-threads --disable-shared (Add a path)
make -j 20
make install
```

### Install PFFT
```
unzip pfft-master.zip
cd pfft-master
autoreconf --install
./configure --disable-fortran (Add a path)
make -j 20
make install
./configure --enable-openmp --disable-fortran --disable-shared (Add a path, remake with openmp)
make -j 20
make install
```

### Install HDF5
```
wget https://support.hdfgroup.org/ftp/HDF5/current18/src/hdf5-1.8.20.tar.gz
tar -zxvf hdf5-1.8.20.tar.gz
cd hdf5-1.8.20/
./configure --enable-cxx --disable-shared (Add a path)
make -j 20
make install
```

### Compile Cholla-PM

On sparkle, I'm using /home/brant/github/bruno/makefile_tiling.
Note we require libz when compiling hdf5 with --disable-shared.  And 
some of the compiling sequences needed to be changed.

### Run simple tests

I have run simple tests with the set of 256^3 ICs that Bruno provided,
using 2 and 4 processes on sparkle. The weak scaling is fine, with each
step taking about 5 seconds.

## Installation and Tests on Summit

Below I detail the process for installing cholla-pm and running tests on Summit.

### Connecting to Summit

There is connection information on the [Summit website](https://www.olcf.ornl.gov/for-users/system-user-guides/summit/).

Currently, you have to connect to an internal OLCF system first, via, e.g., `home.ccs.ornl.gov`. Connection passcode is pin + RSA key.  Note that summit has a different address, `summit.olcf.ornl.gov`.

### Source code location

/ccs/proj/csc275/brantr/cholla-pm/cholla

Also copied at:

/ccs/home/brantr/code/cholla-pm.summit_scaling_tests

### Modules for compilation

```
module load cuda
module load hdf5
module load spectrum-mpi
```

### Compiling FFTW

Well, the FFTW module on Summit does not have mpi enabled!  So we have a harder route.

```
wget http://www.fftw.org/fftw-3.3.7.tar.gz
tar -zxvf fftw-3.3.7.tar.gz
cd fftw-3.3.7/
./bootstrap.sh
./configure --enable-mpi --enable-openmp --enable-threads --disable-shared --prefix=/ccs/home/brantr/code/fftw
make -j 20
make install
```

### Compiling PFFT

First, load modules.  Then:

```
cd ~/code/pfft
unzip pfft-master.zip
cd pfft-master
./bootstrap.sh
./configure --disable-fortran --disable-shared --with-fftw3=/ccs/home/brantr/code/fftw --prefix=/ccs/home/brantr/code/pfft
make -j 20
make install
```

### Compiling Cholla on Summit

I used the makefile at:
```
/ccs/home/brantr/code/cholla-pm.summit_scaling_tests/makefile_tiling_summit
```
which is also at:

```
/ccs/proj/csc275/brantr/cholla-pm/cholla/makefile_tiling_summit
```

#### I had to change N_OMP_THREADS to 6 in global.h.

### Reminders about LSF

To submit a job:
```
bsub scaling.lsf
```

To check on your jobs
```
bjobs
```

To kill a job
```
bkill [jobid]
```

### Running Cholla-PM on Summit

The tests were run out of the directory:
```
/ccs/proj/csc275/brantr/projwork
```

This directory contained the cholla-mp executable, the cosmo_tiling.txt file:
```
##########################################
# number of grid cells in the x dimension
nx=256
# number of grid cells in the y dimension
ny=256
# number of grid cells in the z dimension
nz=256
# output time
tout=10000000000
# how often to output
outstep=10000
times_output=output_list.txt
# value of gamma
gamma=1.66666667
# name of initial conditions
init=Read_Grid
nfile=0
n_parts_initFiles=1
time_max=1000000000
# domain properties
xmin=0.0
ymin=0.0
zmin=0.0
xlen=115000.0
ylen=115000.0
zlen=115000.0
# type of boundary conditions
xl_bcnd=1
xu_bcnd=1
yl_bcnd=1
yu_bcnd=1
zl_bcnd=1
zu_bcnd=1
outdir=./dat/
indir=./ics/ics_256/
```

The output_list.txt file:
```
1.000000000000000000e+00
```

There was a subdirectory ``ics/ics_256/``, which contained the `0.h5` and `0_parts.h5` files. I created symlinks for the process ICs using the following script
```
#!/bin/bash
I=$1
while [ $I -lt $(($2+1)) ]; do
    $BASE `printf "ln -s 0.h5 0.h5.%d" $I`
    $BASE `printf "ln -s 0_parts.h5 0_parts.h5.%d" $I`
    I=$(($I+1))
done
```

An ICs symlink needs to be made for each process.  

To run the test, I used the following LSF script:

```
#!/bin/bash
#BSUB -P CSC275robertson
#BSUB -W 0:30
#BSUB -nnodes 1
#BSUB -alloc_flags gpumps
#BSUB -J scaling_6
#BSUB -o scaling_6.%J
#BSUB -e scaling_6.%J

module load cuda
module load hdf5
module load spectrum-mpi

date

cd /ccs/proj/csc275/brantr/projwork
export OMP_NUM_THREADS=6
jsrun -n6 -r6 -a1 -g1 -c6 -b packed:6 -d packed -l GPU-CPU ./cholla-pm cosmo_tiling.txt
mv tiling_timing.txt tiling_timing.6.txt
```

