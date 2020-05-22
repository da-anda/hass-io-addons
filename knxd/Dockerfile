ARG BUILD_FROM
FROM ${BUILD_FROM}

ENV LANG C.UTF-8
ARG KNXD_VERSION
RUN set -xe \
    && apk update \
    && apk add --no-cache --virtual .build-dependencies \
                build-base \
                gcc \
                git \
                abuild \
                binutils \
                automake \
                autoconf \
                libtool \
                argp-standalone \
                linux-headers \
                libev-dev \
                libusb-dev \
                cmake \
                dev86 \
     && apk add --no-cache \
                udev \
                libusb \
                libev \
     && git clone --branch "${KNXD_VERSION}" --depth 1 https://github.com/knxd/knxd.git \
     && cd knxd \
     && ./bootstrap.sh \
     && ./configure --disable-systemd --enable-tpuart --enable-usb --enable-eibnetipserver --enable-eibnetip --enable-eibnetserver --enable-eibnetiptunnel \
     && mkdir -p src/include/sys && ln -s /usr/lib/bcc/include/sys/cdefs.h src/include/sys \
     && make \
     && make install \
     && make clean \
     && cd .. \
     && rm -rf knxd \
     && apk del --purge .build-dependencies

# Copy data for add-on
COPY run.sh /
RUN chmod a+x /run.sh
RUN dos2unix /run.sh

CMD [ "/run.sh" ]