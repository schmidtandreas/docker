FROM schmidtandreas/ubuntu-dev

LABEL version="0.0.2"
LABEL description="ESP8266 toolchain environment"

# get toolchain
ARG TC_VERSION="1.22.0-100-ge567ec7-5.2.0"
ARG TC_TAR_FILE="xtensa-lx106-elf-linux64-${TC_VERSION}.tar.gz"
ARG TC_URL="https://dl.espressif.com/dl/${TC_TAR_FILE}"
RUN cd /tmp && \
    wget $TC_URL

RUN mkdir /toolchain
WORKDIR /toolchain

RUN tar xf /tmp/${TC_TAR_FILE}

# get SDK
RUN mkdir /sdk
WORKDIR /sdk

ARG SDK_NAME="ESP8266_RTOS_SDK"
ARG SDK_URL="https://github.com/espressif/${SDK_NAME}.git"
RUN git clone --recursive ${SDK_URL}
RUN cd ${SDK_NAME} && \
    python -m pip install -r requirements.txt

# enable ccache for xtensa toolchain
RUN ln -s ../../bin/ccache /usr/lib/ccache/xtensa-lx106-elf-gcc && \
    ln -s ../../bin/ccache /usr/lib/ccache/xtensa-lx106-elf-g++

# create user
RUN useradd -G uucp,dialout -ms /bin/bash user
RUN chown -R user:user ${SDK_NAME}
USER user:user

ENV PATH=/usr/lib/ccache:${PATH}:/toolchain/xtensa-lx106-elf/bin
ENV IDF_PATH=/sdk/${SDK_NAME}
ENV TERM=screen-256color

WORKDIR /project

CMD []
# vim: ts=4 sw=4 et
