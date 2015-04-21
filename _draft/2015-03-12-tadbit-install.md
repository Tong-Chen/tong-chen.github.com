---
title: Install TAD-bit
author: Chen Tong
layout: post
categories:
  - bash
  - bioinfor
tags:
  - bash
--

1. Install IMP
		* Prerequires
** Install mpfr (needed by CGAL) **

wget http://www.mpfr.org/mpfr-current/mpfr-3.1.2.tar.gz -o mpfr-3.1.2.tar.gz

tar xvzf mpfr-3.1.2.tar.gz

cd mpfr-3.1.2

./configure --prefix=/home/baowen/trash/mpfr

make

make install

** INstall CGAL **

wget https://gforge.inria.fr/frs/download.php/file/34512/CGAL-4.5.2.tar.gz

tar xvzf CGAL-4.5.2.tar.gz

cd CGAL-4.5.2

cmake . -DCMAKE_INSTALL_PREFIX=/home/baowen/trash/CGAL

make

make install

Modify source file: include/CGAL/Mpzf.h

Possibly easier alternative, edit the file include/CGAL/Mpzf.h, find the 
line that says: 

// GMP before 5.0 doesn't provide mpn_copyi. 

And just before it, insert: 

// GMP-4.3.0 is missing mpn_sqr. 
#ifndef mpn_sqr 
#define mpn_sqr(dest,a,n) mpn_mul_n(dest,a,a,n) 
#endif 


** Install SWIG 2.0 series **

First remove SWIG 3.0 by 

mv ~/baowen/software/swig-3.0.5 ~/baowen/software/swig-3.0.5.bak

wget http://downloads.sourceforge.net/project/swig/swig/swig-2.0.12/swig-2.0.12.tar.gz

tar xvzf swig-2.0.12.tar.gz

cd swig-2.0.12

./configure --prefix=/home/baowen/trash/swig

make && make install

** INSTALl boost (not 1.4.1)

Follow instructions

** Install log4cxx **

wget http://mirrors.hust.edu.cn/apache/logging/log4cxx/0.10.0/apache-log4cxx-0.10.0.tar.gz

tar xvzf apache-log4cxx-0.10.0.tar.gz

./configure --prefix /home/baowen/trash/log4cxx

make

------------unsucessed log4cxx-----------------------------------


** Install ANN **

wget http://www.cs.umd.edu/~mount/ANN/Files/1.1.2/ann_1.1.2.tar.gz

tar xvzf ann_1.1.2.tar.gz

make linux-g++


** Install Eigen **

wget http://bitbucket.org/eigen/eigen/get/3.2.4.tar.gza -o Eigen.3.2.4.tar.gz
mkdir eigen
mv Eigen.3.2.4.tar.gz eigen
cd eigen
tar xvzf Eigen.3.2.4.tar.gz
cmake eigen-eigen-10219c95fe65 -DCMAKE_INSTALL_PREFIX=/home/baowen/trash/eigen.3.2.4

------------unsucessed Eigen-----------------------------------

** Install FFTW ** 
wget ftp://ftp.fftw.org/pub/fftw/fftw-3.3.4.tar.gz
tar xvzf fftw-3.3.4.tar.gz
/configure --prefix=/home/baowen/trash/fftw
make && make install

** Install libTAU **

wget http://integrativemodeling.org/libTAU/libTAU-1.0.1.zip
unzip libTAU-1.0.1.zip
cd libTAU-1.0.1
cp lib/RedHat6.x86_64/libTAU.so.1 lib/
cd lib
ln -s libTAU.so.1 libTAU.so

---ff--------------------------------------------------------------------------------

** Add following liens to .bash_profile **

export PATH=${PATH}:~/baowen/software/hdf5-1.8.9-linux-x86_64-shared:/home/baowen/trash/mpfr:/home/baowen/trash/CGAL:/home/baowen/trash/CGAL/bin:/home/baowen/trash/swig:/home/baowen/trash/swig/bin:~/trash/ann_1.1.2:~/trash/ann_1.1.2/bin:~/trash/fftw:~/trash/fftw/bin:~/trash/libTAU-1.0.1

export CGAL_DIR=~/trash/CGAL/lib/CGAL

export LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:~/trash/libTAU-1.0.1/lib:~/trash/fftw/lib

** Add following lines to imp-2.0.1/CMakeLists.txt to recognize python-dev ** 

set(PYTHON_LIBRARIES "~/baowen/software/anaconda/lib")
set(PYTHON_INCLUDE_DIRS "~/baowen/software/anaconda/include/python2.7/")

set(PYTHON_LIBRARIES "~/baowen/software/anaconda/lib")
set(PYTHON_INCLUDE_DIRS "~/baowen/software/anaconda/include/python2.7/")
set(CMAKE_INCLUDE_PATH "~/trash/boost157" "~/trash/ann_1.1.2" "~/trash/fftw" "~/trash/libTAU-1.0.1" ${CMAKE_INCLUDE_PATH})
set(CMAKE_LIBRARY_PATH "~/trash/boost157/lib" "~/trash/ann_1.1.2/lib" "~/trash/fftw/li" "~/trash/libTAU-1.0.1/lib" ${CMAKE_LIBRARY_PATH})

set(BOOST_ROOT "~/trash/boost157")
set(BOOST_INCLUDEDIR "~/trash/boost157/include")
set(BOOST_LIBRARYDIR "~/trash/boost157/lib")
set(Boost_NO_SYSTEM_PATHS ON)

set(FFTW3_ROOT "~/trash/fftw")
set(FFTW3_INCLUDEDIR "~/trash/fftw/include")
set(FFTW3_LIBRARYDIR "~/trash/fftw/lib")

set(libTAU_ROOT "~/trash/libTAU")
set(libTAU_INCLUDEDIR "~/trash/libTAU/include")
set(libTAU_LIBRARYDIR "~/trash/libTAU/lib")


** imp-2.0.1

mkdir imp

cd imp

cmake -DCMAKE_INSTALL_PREFIX=/home/baowen/trash/imp5/imp -DCMAKE_BUILD_TYPE=Release -DIMP_MAX_CHECKS=NONE -DIMP_MAX_LOG=SILENT ../imp-2.0.1

** Modify source code of imp-2.0.1

* /home/baowen/trash/imp5/imp-2.0.1/modules/cgal/src/internal/polyhedrons.cpp
        * Delete // CGAL::make_skin_surface_mesh_3(p, l.begin(), l.end(), 1.0) --- << std::distance(p.facets_begin(), p.facets_end()) << std::endl);*/

* /home/baowen/trash/imp5/imp/include/IMP/domino/internal/maximal_cliques.h
        * tie --> boost::tie  (line 88) 


		* Path recognition
				```
include_directories($ENV{INCLUDE_PATH})
link_directories($ENV{LD_LIBRARY_PATH})

				```
