FROM schmidtandreas/oselas-toolchain:latest

LABEL version="2018.12.0"
LABEL description="PTXDIST image based on osales-toolchain image"

ARG PTXDIST_VERSION=2018.12.0

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

USER andreas:andreas

ENV TERM=screen-256color

WORKDIR /home/andreas/project

ENTRYPOINT [ "ptxdist" ]

CMD []
# vim: ts=4 sw=4 et
