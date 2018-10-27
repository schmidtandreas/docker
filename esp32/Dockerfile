FROM schmidtandreas/ubuntu-dev

LABEL version="0.0.1"
LABEL description="ESP32 toolchain environment"

RUN useradd -ms /bin/bash user

USER root:root

RUN cd /opt && \
    wget https://dl.espressif.com/dl/xtensa-esp32-elf-linux64-1.22.0-80-g6c4433a-5.2.0.tar.gz && \
    tar xzf xtensa-esp32-elf-linux64-1.22.0-80-g6c4433a-5.2.0.tar.gz && \
    rm -rf xtensa-esp32-elf-linux64-1.22.0-80-g6c4433a-5.2.0.tar.gz

ENV PATH=$PATH:/opt/xtensa-esp32-elf/bin

RUN pip install esptool

RUN git clone --recursive https://github.com/espressif/esp-idf.git esp && \
    chown -R user:user /esp

RUN pip install -r /esp/requirements.txt

ENV IDF_PATH=/esp
ENV PWD=/project

WORKDIR /project

CMD []
# vim: ts=4 sw=4 et
