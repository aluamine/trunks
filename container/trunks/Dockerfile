FROM golang:1.14 AS builder
LABEL maintainer="youssouf.drif"

RUN go get -d github.com/aluamine/trunks
WORKDIR /go/src/github.com/aluamine/trunks
RUN go install github.com/aluamine/trunks

FROM debian:buster-slim
WORKDIR /trunks
RUN apt-get update && DEBIAN_FRONTEND=non-interactive apt-get install -qy --no-install-recommends --no-install-suggests \
    iproute2 iptables procps tcpdump iputils-ping \
    && rm -rf /var/lib/apt/lists/*
COPY --from=builder /go/bin/trunks /usr/local/sbin/trunks
ENTRYPOINT [ "trunks" ]
CMD [ "--help" ]
