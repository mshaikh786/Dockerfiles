FROM krccl/openmpi_base:403
RUN apt-get update && apt-get install -y git autoconf wget libudunits2-dev libgsl-dev libantlr-dev flex
ENV PATH /software/bin:$PATH
ENV LD_LIBRARY_PATH /software/lib:$LD_LIBRARY_PATH
ENV PKG_CONFIG_PATH /software/lib/pkgconfig:$PKG_CONFIG_PATH
WORKDIR /software
# Install dependencies for NCO
RUN git clone -b v1.2.11 https://github.com/zlib-ng/zlib-ng.git && \
    cd zlib-ng && \
    ./configure --prefix=/software --sharedlibdir=/software/lib && \
    make && make install && \
    cd /software && \
    git clone -b hdf5-1_12_2 https://github.com/HDFGroup/hdf5.git && \
	cd hdf5 && \
    ./configure --prefix=/software --enable-parallel --with-zlib=/software && \
    make VERBOSE=1 && make install && \
	cd /software && \
    curl https://parallel-netcdf.github.io/Release/pnetcdf-1.12.3.tar.gz -o /tmp/pnetcdf-1.12.3.tar.gz && \
    tar xvf /tmp/pnetcdf-1.12.3.tar.gz && \
    cd pnetcdf-1.12.3 && \
    ./configure --prefix=/software --enable-shared  && \
    make VERBOSE=1 && make install  && \
    cd /software && \
    git clone -b v4.9.0 https://github.com/Unidata/netcdf-c.git && \
    cd /software/netcdf-c && \
    autoconf && \
    ./configure --enable-pnetcdf --with-pic --enable-shared --prefix=/software CPPFLAGS=-I/software/include LDFLAGS=-L/software/lib LIBS=-lz && \
    make && make install
RUN rm -rf zlib-ng hdf5 pnetcdf-1.12.3 netcdf-c /tmp/*

# Install NCO
RUN wget https://github.com/nco/nco/archive/refs/tags/4.8.1.tar.gz && \
    tar xvf 4.8.1.tar.gz && \
    cd nco-4.8.1/ && \
    ./configure --enable-udunits --enable-ncap2 --prefix=/software CPPFLAGS=-I/software/include LDFLAGS=-L/software/lib && \
    make VERBOSE=1 && make install && \
    cd /software
RUN rm -rf 4.8.1.tar.gz nco-4.8.1

