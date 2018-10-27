FROM schmidtandreas/esp32-toolchain

ENV ZEPHYR_BASE=/zephyr
ENV ZEPHYR_TOOLCHAIN_VARIANT=espressif
ENV ZEPHYR_SDK_INSTALL_DIR=/opt/zephyr-sdk
ENV ESP_IDF_PATH=${IDF_PATH}
ENV ESPRESSIF_TOOLCHAIN_PATH=/opt/xtensa-esp32-elf

# Zephyr SDK
ENV ZEPHYR_SDK_VERSION=0.9.3
ENV ZEPHYR_SDK_URL=https://github.com/zephyrproject-rtos/meta-zephyr-sdk/releases/download/${ZEPHYR_SDK_VERSION}
ENV ZEPHYR_SDK_SETUP=zephyr-sdk-${ZEPHYR_SDK_VERSION}-setup.run
RUN wget -O /tmp/zephyr_sdk_setup ${ZEPHYR_SDK_URL}/${ZEPHYR_SDK_SETUP} && \
    chmod 755 /tmp/zephyr_sdk_setup && \
    /tmp/zephyr_sdk_setup --quiet && \
    rm /tmp/zephyr_sdk_setup

# Zephyr
RUN git clone https://github.com/zephyrproject-rtos/zephyr.git ${ZEPHYR_BASE}

RUN pip3 install --user -r ${ZEPHYR_BASE}/scripts/requirements.txt

WORKDIR ${ZEPHYR_BASE}

RUN echo "source ${ZEPHYR_BASE}/zephyr-env.sh" >> /etc/bash.bashrc

# vim: ts=4 sw=4 et
