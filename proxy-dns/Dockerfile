FROM debian:jessie

MAINTAINER IMXQD <ahtlxqd@gmail.com>

ADD https://bin.equinox.io/c/VdrWdbjqyF/cloudflared-stable-linux-amd64.deb /cloudflare.deb

RUN apt-get update && \
    apt-get install -y ca-certificates && \
    dpkg -i /cloudflare.deb && \
    apt-get install -f && \
    apt-get autoclean --yes && \
    apt-get clean --yes && \
    rm -rf /cloudflare.deb

COPY config.yaml /etc/cloudflared/config.yaml

ENV LOCAL_PORT 5311

EXPOSE $LOCAL_PORT/tcp $LOCAL_PORT/udp

CMD  cloudflared proxy-dns --port $LOCAL_PORT --address 0.0.0.0