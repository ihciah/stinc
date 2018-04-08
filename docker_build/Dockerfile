FROM alpine
MAINTAINER ihciah

ENV SS_URL https://github.com/shadowsocks/shadowsocks-libev/archive/v3.1.3.tar.gz
ENV SS_DIR shadowsocks-libev-3.1.3
ENV KCP_URL https://github.com/xtaci/kcptun/releases/download/v20180316/kcptun-linux-amd64-20180316.tar.gz
ENV CHINADNS_URL https://github.com/shadowsocks/ChinaDNS/releases/download/1.3.2/chinadns-1.3.2.tar.gz

RUN set -ex \
    && apk add --no-cache c-ares \
                          libcrypto1.0 \
                          libev \
                          libsodium \
                          mbedtls \
                          pcre \
                          tinc \
                          iptables \
                          ipset \
                          dnsmasq \
                          supervisor \
                          bash \
    && apk add --no-cache \
               --virtual TMP autoconf \
                             automake \
                             build-base \
                             c-ares-dev \
                             curl \
                             gettext-dev \
                             libev-dev \
                             libsodium-dev \
                             libtool \
                             linux-headers \
                             mbedtls-dev \
                             openssl-dev \
                             pcre-dev \
                             tar \
                             musl-dev \
                             gcc \
                             gawk \
                             make \
                             libtool \
    && curl -sSL $SS_URL | tar xz \
    && cd $SS_DIR \
        && curl -sSL https://github.com/shadowsocks/ipset/archive/shadowsocks.tar.gz | tar xz --strip 1 -C libipset \
        && curl -sSL https://github.com/shadowsocks/libcork/archive/shadowsocks.tar.gz | tar xz --strip 1 -C libcork \
        && curl -sSL https://github.com/shadowsocks/libbloom/archive/master.tar.gz | tar xz --strip 1 -C libbloom \
        && ./autogen.sh \
        && ./configure --disable-documentation \
        && make install \
        && cd .. \
        && rm -rf $SS_DIR \
    && mkdir /kcp && mkdir /chinadns \
    && curl -sSL $KCP_URL | tar xz -C /kcp client_linux_amd64 \
    && curl -sSL $CHINADNS_URL | tar xz --strip 1 -C /chinadns \
    && cd /chinadns && ./configure && make && make install && cd / && rm -rf /chinadns \
    && echo "no-resolv" > /etc/dnsmasq.conf \
    && echo "listen-address=127.0.0.1" >> /etc/dnsmasq.conf \
    && echo "conf-dir=/etc/dnsmasq.d/,*.conf" >> /etc/dnsmasq.conf \
    && echo "server=127.0.0.1#5353" >> /etc/dnsmasq.conf \
    && apk del TMP



EXPOSE 8388/tcp
EXPOSE 8388/udp

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf"]
