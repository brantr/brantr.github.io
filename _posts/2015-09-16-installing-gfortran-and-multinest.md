---
layout: post
title: Installing gfortran and Multinest
---

---

Install GMP
-----------

cd ~/code/gmp
curl -0 https://ftp.gnu.org/gnu/gmp/gmp-6.0.0a.tar.bz2
tar -zxvf gmp-6.0.0a.tar.bz2 
cd gmp-6.0.0
CC=clang CXX=clang++ CXXFLAGS="-stdlib=libstdc++" LDFLAGS="-stdlib=libstdc++" ./configure --prefix=/Users/brant/code/gmp
make -j 8
make install
make check

Install MPFR
------------

<http://www.mpfr.org/mpfr-current/#download>
cd code/mpfr
curl -O http://www.mpfr.org/mpfr-current/mpfr-3.1.3.tar.bz2
tar -xvf mpfr-3.1.3.tar.bz2
mkdir build
cd build
CC=clang CXX=clang++ CXXFLAGS="-stdlib=libstdc++" LDFLAGS="-stdlib=libstdc++" ../mpfr-3.1.3/configure --prefix=/Users/brant/code/mpfr --with-gmp=/Users/brant/code/gmp
make -j 8
make install

Install MPC
-----------

<http://www.multiprecision.org/index.php?prog=mpc>

cd code/mpc
curl -O ftp://ftp.gnu.org/gnu/mpc/mpc-1.0.3.tar.gz
tar -xvf mpc-1.0.3.tar.gz 
mkdir build
cd build
CC=clang CXX=clang++ CXXFLAGS="-stdlib=libstdc++" LDFLAGS="-stdlib=libstdc++" ../mpc-1.0.3/configure --prefix=/Users/brant/code/mpc --with-gmp=/Users/brant/code/gmp --with-mpfr=/Users/brant/code/mpfr
make -j 8
make install

Installing gfortran
-------------------
cd code/gfortran
cd gcc-5.2.0
curl -O http://gnu.mirror.iweb.com/gcc/gcc-4.9.3/gcc-4.9.3.tar.bz2
tar -zxvf gcc-4.9.3.tar.bz2
mkdir build
cd build
<https://gcc.gnu.org/wiki/GFortranBinaries>
curl -O http://coudert.name/software/gfortran-5.1-Yosemite.dmg
 sudo hdiutil attach gfortran-5.1-Yosemite.dmg 
 cp -r /Volumes/gfortran-5.1-Yosemite/gfortran-5.1-Yosemite/gfortran.pkg .
 sudo installer -pkg gfortran.pkg -target /
 sudo hdiutil detach /Volumes/gfortran-5.1-Yosemite

Puts gfortran in /usr/local/bin/gfortran.

Install gsl
-----------

mkdir code/gsl
cd code/gsl
get it from http://ftpmirror.gnu.org/gsl/gsl-1.16.tar.gz
cd gsl-1.16
CC=clang CXX=clang++ CXXFLAGS="-stdlib=libstdc++" LDFLAGS="-stdlib=libstdc++" ./configure
make -j 8
make install

Install gsl globally.

Building the source
-------------------

cd ~/code/multinest
tar -xvf multinest.tar
Comment out the mpi lines.
Then make.
