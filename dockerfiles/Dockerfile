FROM ghcr.io/taffish-org/debian:12

LABEL maintainer="taffish@163.com"

WORKDIR /root

RUN apt-get update && apt-get install -y curl git gcc g++ make

RUN apt-get update && apt-get install -y zlib1g-dev libncurses-dev liblzma-dev libbz2-dev libcurl4-gnutls-dev libcrypto++-dev libdeflate-dev

RUN apt-get update && apt-get install -y libsimde-dev libwfa2-dev libhts-dev libvcflib-dev cmake bc parallel meson ninja-build libvcflib-tools vcftools

RUN git clone --recursive https://github.com/samtools/htslib.git && \
    git clone --recursive https://github.com/samtools/samtools.git && \
    git clone --recursive https://github.com/samtools/bcftools.git && \
    cd /root/samtools/ && make && make install && \
    cd /root/bcftools/ && make && make install

RUN cd /root/ && git clone --recursive https://github.com/freebayes/freebayes.git && \
    cd /root/freebayes/ && meson build/ --buildtype release && \
    cp /root/freebayes/contrib/SeqLib/SeqLib/* /usr/include/ && \
    cd /root/freebayes/build/ && ninja && ninja test \
    cp /root/freebayes/build/freebayes    /usr/local/bin/ && \
    cp /root/freebayes/build/bamleftalign /usr/local/bin/
    

ENV TAFFISH_ENV=TAFFISH
ENV TAFFISH_NAME=freebayes
