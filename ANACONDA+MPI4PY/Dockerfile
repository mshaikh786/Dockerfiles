FROM ubuntu:18.04
RUN apt-get update

# Building GCC
RUN apt-get install --yes wget vim sudo build-essential gfortran

# Building MPICH3
RUN mkdir /software /build
WORKDIR /build
RUN wget http://www.mpich.org/static/downloads/3.1.4/mpich-3.1.4.tar.gz
RUN tar xvf mpich-3.1.4.tar.gz
WORKDIR mpich-3.1.4
RUN bash ./configure 
RUN make -j4 VERBOSE=1
RUN make install
RUN ldconfig
RUN rm -rf /build/*
WORKDIR /build

# Building ACACONDA
RUN wget https://repo.anaconda.com/archive/Anaconda3-5.3.0-Linux-x86_64.sh
RUN bash Anaconda3-5.3.0-Linux-x86_64.sh -b -p /software/anaconda
WORKDIR /
RUN rm -rf /build
WORKDIR /

# So that the anaconda packages including Python3 is on PATH
ENV PATH="/software/anaconda/bin:${PATH}"

# Building MPI4PY linked to container's own MPICH3
RUN env MPICC=/usr/local/bin/mpicc pip install mpi4py

