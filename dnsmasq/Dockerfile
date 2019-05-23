FROM debian:jessie

MAINTAINER IMXQD <ahtlxqd@gmail.com>

RUN apt-get update && \
    apt-get install -y dnsmasq curl && \
    apt-get autoclean --yes && \
    apt-get clean --yes

RUN cd /etc/dnsmasq.d && \
    curl -O https://raw.githubusercontent.com/cokebar/gfwlist2dnsmasq/master/gfwlist2dnsmasq.sh && \
    bash gfwlist2dnsmasq.sh -p 5311 -o gfwlist2dnsmasq.conf && \
    curl -O https://raw.githubusercontent.com/felixonmars/dnsmasq-china-list/master/accelerated-domains.china.conf && \
    rm -rf gfwlist2dnsmasq.sh

EXPOSE 53 53/udp

CMD dnsmasq -k