# dind

[Docker-in-Docker](https://hub.docker.com/_/docker) based on the official `docker:X.Y.Z-dind` image. It needs a
privileged container, which GitHub-hosted runners and most self-managed GitLab runners allow. For unprivileged
Kubernetes pods use [`dind-rootless`](../dind-rootless/README.md) instead.

Tags follow the Docker Engine release series (`29.9`, `29.8`, ...) and point to the latest patch release of that
series. The 3 newest major and 10 newest minor versions per major are published; `latest` points to the newest one.

## Usage

Start the daemon as the container command with TLS disabled. Other containers on the same network reach it on
`tcp://dind:2375`.

```bash
docker run -d --name dind --privileged -e DOCKER_TLS_CERTDIR="" \
  ghcr.io/containerhive/helper-images/dind:29.9 dockerd --host=tcp://0.0.0.0:2375
```
