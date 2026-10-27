# dind-rootless

Rootless [Docker-in-Docker](https://docs.docker.com/engine/security/rootless/), based on the official
[`docker:X.Y.Z-dind-rootless`](https://hub.docker.com/_/docker) image, tuned for unprivileged CI pods:

- The subuid and subgid range is `1001:64535`, because a pod with `hostUsers=false` only maps the user IDs 0-65535.
- [`passt`](https://passt.top) provides pasta networking. slirp4netns can not create its tap device in such a pod.
- RootlessKit uses the pasta network driver and the implicit port driver. Start the daemon with an explicit
  `dockerd ...` command; the upstream entrypoint default publish conflicts with the implicit driver.

Tags follow the Docker Engine release series (`29.9`, `29.8`, ...) and point to the latest patch release of that
series. The 3 newest major and 10 newest minor versions per major are published; `latest` points to the newest one.

## Usage

Start the daemon as the container command. Other containers in the same pod reach it on `tcp://localhost:2375`.

```yaml
spec:
  containers:
    - name: docker
      image: ghcr.io/containerhive/helper-images/dind-rootless:29.9
      command: ["dockerd", "--host=tcp://0.0.0.0:2375"]
```
