FROM schmidtandreas/ubuntu-dev:latest

LABEL version="2018.02"
LABEL description="OSELAS.Toolchain image based on ubuntu-dev image"

ARG TOOLCHAIN_VERSION=v2018.02.0
ARG PTXDIST_VERSION=2018.02.0
ARG TOOLCHAIN_PTXCONFIG=arm-v7a-linux-gnueabihf_gcc-7.3.1_glibc-2.27_binutils-2.30_kernel-4.15-sanitized.ptxconfig

RUN mkdir /workspace

WORKDIR /workspace

RUN git clone git://git.pengutronix.de/ptxdist && \
    cd ptxdist && \
    git checkout ptxdist-${PTXDIST_VERSION} -b ptxdist-${PTXDIST_VERSION} && \
    ./autogen.sh && \
    ./configure && \
    make && \
    make install && \
    cd .. && \
    rm -rf ptxdist

WORKDIR /

RUN rm -rf /workspace

RUN useradd -ms /bin/bash andreas

RUN chown andreas:andreas /opt

USER andreas:andreas

WORKDIR /home/andreas

RUN git clone git://git.pengutronix.de/OSELAS.Toolchain && \
    cd OSELAS.Toolchain && \
    mkdir -p src && \
    cd src && \
    wget https://public.pengutronix.de/oselas/toolchain/upstream/gcc-7-20180201.tar.xz && \
    wget https://src.fedoraproject.org/lookaside/extras/chrpath/chrpath-0.16.tar.gz/2bf8d1d1ee345fc8a7915576f5649982/chrpath-0.16.tar.gz

RUN cd OSELAS.Toolchain && \
    git checkout ${TOOLCHAIN_VERSION} -b ${TOOLCHAIN_VERSION} && \
    ptxdist select ptxconfigs/${TOOLCHAIN_PTXCONFIG} && \
    ptxdist go && \
    cd .. && \
    rm -rf OSELAS.Toolchain

USER root

RUN chown -R root:root /opt

# vim: ts=4 sw=4 et
