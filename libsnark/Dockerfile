FROM ubuntu:16.04

WORKDIR /root

RUN apt-get update && \
    apt-get install -y \
    wget unzip curl \
    build-essential cmake git libgmp3-dev libprocps4-dev \
    python-markdown libboost-all-dev libssl-dev pkg-config
#如果访问github速度慢，可以使用这个地址加速：
RUN git clone https://github.com.cnpmjs.org/scipr-lab/libsnark/ 
#RUN git clone https://github.com/scipr-lab/libsnark/ 

RUN cd libsnark \
  && git submodule init && git submodule update \
  && mkdir build && cd build && cmake .. \
  && make \
  && DESTDIR=/usr/local make install \
    NO_PROCPS=1 NO_GTEST=1 NO_DOCS=1 CURVE=ALT_BN128 \
    FEATUREFLAGS="-DBINARY_OUTPUT=1 -DMONTGOMERY_OUTPUT=1 -DNO_PT_COMPRESSION=1"

ENV LD_LIBRARY_PATH $LD_LIBRARY_PATH:/usr/local/lib

VOLUME ["/root/projects"]
WORKDIR /root/projects