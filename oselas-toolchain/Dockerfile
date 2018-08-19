FROM schmidtandreas/ubuntu-dev:latest

LABEL version="2018.02"
LABEL description="OSELAS.Toolchain image based on ubuntu-dev image"

ARG TOOLCHAIN_VERSION=v2018.02.0
ARG PTXDIST_VERSION=2018.02.0

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
    rm -rf OSELAS.Toolchain/src

ADD --chown=andreas:andreas src OSELAS.Toolchain/src

RUN cd OSELAS.Toolchain && \
    git checkout ${TOOLCHAIN_VERSION} -b ${TOOLCHAIN_VERSION} && \
    ptxdist select ptxconfigs/arm-v7a-linux-gnueabihf_gcc-7.3.1_glibc-2.27_binutils-2.30_kernel-4.15-sanitized.ptxconfig && \
    ptxdist go && \
    cd .. && \
    rm -rf OSELAS.Toolchain

USER root

RUN chown -R root:root /opt

# vim: ts=4 sw=4 et
