FROM ubuntu:18.04

LABEL version="18.04"
LABEL description="Ubuntu 18.04 based image with development packages"

ENV TERM xterm-256color

RUN apt-get update && \
    apt-get install -qqy --no-install-recommends apt-utils

RUN apt-get install -qqy --no-install-recommends \
        automake autoconf \
        bc bison bzip2 build-essential \
        chrpath cmake curl ccache cpio \
        debianutils diffstat dialog dfu-util device-tree-compiler \
        fakeroot file flex \
        gawk gcc-multilib g++-multilib gcc g++ gettext git gperf \
        help2man \
        iputils-ping \
        libconfuse-dev libtool-bin libexpat-dev \
        libncurses-dev libmpfr-dev libxml-parser-perl \
        lzop \
        make \
        ninja-build \
        patch pkg-config python-dev python3-dev \
        python3 python-setuptools python-serial \
        python3-setuptools python-pip python3-pip \
        python3-wheel \
        sudo socat\
        texinfo \
        unzip \
        wget \
        xz-utils \
        zip

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y locales

RUN apt-get clean && \
    apt-get autoremove -y

# delete all the apt list files since they're big and get stale quickly
RUN rm -rf /var/lib/apt/lists/*

# change default shell to bash
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# configure locale
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    dpkg-reconfigure --frontend=noninteractive locales && \
    update-locale LANG=en_US.UTF-8

ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8

# vim: ts=4 sw=4 et
