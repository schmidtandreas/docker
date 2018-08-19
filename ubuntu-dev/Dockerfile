FROM ubuntu:18.04

LABEL version="18.04"
LABEL description="Ubuntu 18.04 based image with development packages"

ENV TERM xterm-256color

RUN apt-get update && \
    apt-get install -qqy dialog \
        automake autoconf bc bison bzip2 \
        fakeroot file flex gawk gcc g++ \
        gettext git libconfuse-dev make \
        libncurses-dev patch pkg-config \
        python-dev python3-dev texinfo \
        wget curl python3 python-setuptools \
        python3-setuptools xz-utils libmpfr-dev \
        zip unzip lzop && \
    apt-get clean && \
    apt-get autoremove -y

# delete all the apt list files since they're big and get stale quickly
RUN rm -rf /var/lib/apt/lists/*

# vim: ts=4 sw=4 et
