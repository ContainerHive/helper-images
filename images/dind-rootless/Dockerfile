ARG DOCKER_VERSION
FROM docker:${DOCKER_VERSION}-dind-rootless
ARG DOCKER_VERSION

USER root

# A pod with hostUsers=false only maps the user IDs 0-65535, so the upstream range 100000:65536
# does not fit. Start the range after the ID of the rootless user (1000).
RUN echo "rootless:1001:64535" > /etc/subuid \
    && echo "rootless:1001:64535" > /etc/subgid

# slirp4netns needs a tap device via `ip tuntap add`, which the CI pod denies with EACCES.
# pasta does not need a tap device and works on the same nodes.
# hadolint ignore=DL3018
RUN apk add --no-cache passt

# dockerd-entrypoint.sh hardcodes --port-driver=builtin, which pasta rejects. These flags are
# appended after it and win. The implicit port driver forwards the listening port 2375 itself, so
# start the daemon with an explicit `dockerd ...` command; the entrypoint default `-p` publish
# conflicts with it. Do not use the pesto port driver; its seccomp filter kills it with SIGSYS.
ENV DOCKERD_ROOTLESS_ROOTLESSKIT_NET="pasta" \
    DOCKERD_ROOTLESS_ROOTLESSKIT_FLAGS="--port-driver=implicit"

USER rootless

LABEL docker.version="${DOCKER_VERSION}"
