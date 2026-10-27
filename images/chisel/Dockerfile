FROM mirror.gcr.io/library/ubuntu:26.04
ARG TARGETARCH
ARG CHISEL_VERSION
# hadolint ignore=DL3008
RUN apt-get update \
    && apt-get install -y --no-install-recommends ca-certificates git \
    && rm -rf /var/lib/apt/lists/*
ADD https://github.com/canonical/chisel/releases/download/v${CHISEL_VERSION}/chisel_v${CHISEL_VERSION}_linux_${TARGETARCH}.tar.gz /tmp/chisel.tar.gz
RUN tar -xzf /tmp/chisel.tar.gz -C /usr/local/bin chisel \
    && rm /tmp/chisel.tar.gz
LABEL chisel.version="${CHISEL_VERSION}"
ENTRYPOINT ["chisel"]
