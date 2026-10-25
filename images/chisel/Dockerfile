FROM mirror.gcr.io/library/ubuntu:24.04
ARG TARGETARCH
ARG CHISEL_VERSION
SHELL ["/bin/bash", "-o", "pipefail", "-c"]
# hadolint ignore=DL3008
RUN apt-get update \
    && apt-get install -y --no-install-recommends ca-certificates curl git \
    && rm -rf /var/lib/apt/lists/* \
    && curl -fsSL "https://github.com/canonical/chisel/releases/download/v${CHISEL_VERSION}/chisel_v${CHISEL_VERSION}_linux_${TARGETARCH}.tar.gz" \
      | tar -xz -C /usr/local/bin chisel
LABEL chisel.version="${CHISEL_VERSION}"
ENTRYPOINT ["chisel"]
