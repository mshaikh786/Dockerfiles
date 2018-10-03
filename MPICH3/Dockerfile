FROM ubuntu:18.04
RUN apt-get update
RUN apt-get install --yes wget vim sudo build-essential gfortran
WORKDIR /tmp
RUN wget http://www.mpich.org/static/downloads/3.2.1/mpich-3.2.1.tar.gz
RUN tar xvf mpich-3.2.1.tar.gz
WORKDIR mpich-3.2.1
RUN bash ./configure
RUN make -j4 VERBOSE=1
RUN make install
WORKDIR /
RUN rm -rf /tmp/*


