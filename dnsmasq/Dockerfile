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
    rm -rf gfwlist2dnsmasq.sh && \
    echo 'server=10.5.0.3#5322' >> /etc/dnsmasq.conf && \
    curl https://raw.githubusercontent.com/googlehosts/hosts/master/hosts-files/hosts -o /etc/googlehosts && \
    echo 'addn-hosts=/etc/googlehosts' > /etc/dnsmasq.d/hosts.conf && \
    echo 'interface=lo' >> /etc/dnsmasq.conf && \
    echo 'interface=eth0' >> /etc/dnsmasq.conf && \
    echo 'interface=docker0' >> /etc/dnsmasq.conf && \
    echo 'user=root' >> /etc/dnsmasq.conf && \
    echo 'conf-dir=/etc/dnsmasq.d/,*.conf' >> /etc/dnsmasq.conf

EXPOSE 53 53/udp

CMD dnsmasq -k
