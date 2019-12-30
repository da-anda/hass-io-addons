ARG BUILD_FROM
FROM ${BUILD_FROM}

ENV LANG C.UTF-8

RUN set -xe \
    && apk update \
    && apk add --no-cache --virtual .build-dependencies \
                jq \
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
     && git clone -b stable https://github.com/knxd/knxd.git \
     && cd knxd \
     && ./bootstrap.sh \
     && ./configure --disable-systemd --enable-tpuart --enable-usb --enable-eibnetipserver --enable-eibnetip --enable-eibnetserver --enable-eibnetiptunnel \
     && mkdir -p src/include/sys && ln -s /usr/lib/bcc/include/sys/cdefs.h src/include/sys \
     && make \
     && make install \
     && apk del --purge .build-dependencies

# EXPOSE 3672 6720

# VOLUME /etc/knxd
#COPY docker-healthcheck /home/docker-healthcheck
#RUN chmod +x /home/docker-healthcheck
#CMD ["knxd","/etc/knxd/knxd.ini"]


# Copy data for add-on
COPY run.sh /
RUN chmod a+x /run.sh

CMD [ "/run.sh" ]
