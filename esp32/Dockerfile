FROM schmidtandreas/ubuntu-dev

LABEL version="0.0.1"
LABEL description="ESP32 toolchain environment"

WORKDIR /
RUN git clone https://github.com/espressif/esp-idf.git

WORKDIR /esp-idf
RUN git submodule update --init --recursive
RUN IDF_TOOLS_PATH=/toolchain ./install.sh
RUN python -m pip install -r requirements.txt

RUN rm -rf /bin/sh && \
    ln -s /bin/bash /bin/sh

# create user
RUN useradd -G uucp,dialout -ms /bin/bash -p "$(openssl passwd -1 user)" user
RUN chown -R user:user /esp-idf
RUN sed -i "s|^sudo\(.*\)$|sudo\1user|" /etc/group
USER user:user

ENV IDF_TOOLS_PATH=/toolchain
ENV IDF_CCACHE_ENABLE=true

ENV TERM=screen-256color
ENV PWD=/project

WORKDIR /project

CMD []
# vim: ts=4 sw=4 et
