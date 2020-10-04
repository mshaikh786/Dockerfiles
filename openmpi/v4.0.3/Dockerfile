FROM ubuntu:18.04
RUN apt-get update && apt-get install -y \
    build-essential \
    gcc-4.8 curl make libnuma-dev libnl-3-200
WORKDIR /tmp
COPY MLNX_OFED_LINUX-5.0-2.1.8.0-ubuntu18.04-x86_64.tgz /tmp
RUN tar xvf MLNX_OFED_LINUX-5.0-2.1.8.0-ubuntu18.04-x86_64.tgz
RUN echo "deb file:/tmp/MLNX_OFED_LINUX-5.0-2.1.8.0-ubuntu18.04-x86_64/DEBS/UPSTREAM_LIBS ./" > /etc/apt/sources.list.d/mlnx_ofed.list 
RUN curl -L http://www.mellanox.com/downloads/ofed/RPM-GPG-KEY-Mellanox | apt-key add -
RUN apt-get update

RUN apt-get install -y mlnx-ofed-basic-user-only
RUN rm -rf /tmp/MLNX_OFED_LINUX*

#Building OpenMPI 

WORKDIR /tmp
RUN curl -o /tmp/openmpi-4.0.3.tar https://download.open-mpi.org/release/open-mpi/v4.0/openmpi-4.0.3.tar.gz
RUN tar xvf /tmp/openmpi-4.0.3.tar 
WORKDIR /tmp/openmpi-4.0.3
RUN ./configure --prefix=/usr/local --with-verbs 
RUN make -j 8 VERBOSE=1
RUN make install
WORKDIR /
RUN rm -rf /tmp/openmpi-4.0.3.tar /tmp/openmpi-4.0.3
RUN ldconfig 
ENV LD_LIBRARY_PATH /usr/local/lib:/usr/lib/x86_64-linux-gnu:$LD_LIBRARY_PATH
ENV PATH /usr/local/bin:$PATH




