FROM debian:jessie

MAINTAINER IMXQD <ahtlxqd@gmail.com>

ENV DNS_VER 1.3.2
ENV DNS_URL https://github.com/clowwindy/ChinaDNS/releases/download/${DNS_VER}/chinadns-${DNS_VER}.tar.gz
ENV DNS_FILE chinadns.tar.gz
ENV DNS_MD5 f3ece30f2a453d25cc22ef6e1ef579b0

RUN apt-get update \
    && apt-get install -y build-essential curl dnsmasq supervisor \
    && mkdir chinadns \
        && cd chinadns \
        && curl -sSL ${DNS_URL} -o ${DNS_FILE} \
        && echo "${DNS_MD5} ${DNS_FILE}" | md5sum -c \
        && tar xzf ${DNS_FILE} --strip 1 \
        && ./configure \
        && make install \
        && cd .. \
        && rm -rf chinadns \
    && apt-get remove -y build-essential \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/*

RUN curl https://raw.githubusercontent.com/YKilin/ChinaDNS/master/iplist.txt > /etc/iplist.txt

RUN curl http://ftp.apnic.net/apnic/stats/apnic/delegated-apnic-latest \
        | grep ipv4 \
            | grep CN \
                | awk -F\| '{printf("%s/%d\n", $4, 32-log($5)/log(2))}' > /etc/chnroute.txt


EXPOSE 5322/tcp 5322/udp

CMD chinadns -m -c /etc/chnroute.txt -p 5322 -s 114.114.114.114,127.0.0.1:5311