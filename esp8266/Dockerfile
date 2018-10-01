FROM schmidtandreas/ubuntu-dev

LABEL version="0.0.1"
LABEL description="ESP8266 toolchain environment"

RUN apt-get update && \
    apt-get install -qqy build-essential gperf libtool-bin \
    python-serial libexpat-dev help2man python-pip python3-pip && \
    apt-get clean && \
    apt-get autoremove

RUN rm -rf /var/lib/apt/lists/*

RUN useradd -ms /bin/bash user

RUN mkdir /toolchain && \
    chown user:user /toolchain && \
    chown user:user /opt

USER user:user

WORKDIR /toolchain

RUN git clone https://github.com/jcmvbkbc/crosstool-NG && \
    cd crosstool-NG && \
    git checkout -b xtenso-1.22.x && \
    ./bootstrap && \
    ./configure --prefix=$(pwd) && \
    make && \
    make install

WORKDIR /toolchain/crosstool-NG

RUN ./ct-ng xtensa-lx106-elf && \
    sed -r -i.org s%CT_PREFIX_DIR=.*%CT_PREFIX_DIR="/opt/xtensa-lx106-elf"% .config && \
    sed -r -i s%CT_INSTALL_DIR_RO=y%"#"CT_INSTALL_DIR_RO=y% .config && \
    ./ct-ng build

USER root:root

WORKDIR /

RUN rm -rf /toolchain && \
    chown root:root -R /opt/xtensa-lx106-elf

ENV PATH=$PATH:/opt/xtensa-lx106-elf/bin

ENV XTENSA_SYSROOT=/opt/xtensa-lx106-elf/xtensa-lx106-elf/sysroot

RUN xtensa-lx106-elf-objcopy --rename-section .text=.irom0.text \
    --rename-section .literal=.irom.literal ${XTENSA_SYSROOT}/lib/libc.a \
    ${XTENSA_SYSROOT}/lib/libcirom.a

RUN git clone https://github.com/tommie/lx106-hal && \
    cd lx106-hal && \
    autoreconf -i && \
    ./configure --host=xtensa-lx106-elf --prefix=${XTENSA_SYSROOT}/usr && \
    make && \
    make install && \
    rm -rf lx106-hal

RUN pip install esptool

RUN git clone https://github.com/espressif/ESP8266_NONOS_SDK.git sdk && \
    cd sdk && \
    sed -i "s|\r||" ld/eagle.app.v6.ld && \
    #sed -i "s|../ld|./ld|" ld/eagle.app.v6.ld && \
    sed -i "s|\r||" ld/eagle.rom.addr.v6.ld

WORKDIR /project

# vim: ts=4 sw=4 et
