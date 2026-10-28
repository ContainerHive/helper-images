# buildkit

[BuildKit](https://github.com/moby/buildkit) based on the official `moby/buildkit` image. It runs `buildkitd` as root
and needs a privileged container.

Tags follow the BuildKit release series with the upstream `v` prefix (`v0.34`, `v0.33`, ...) and point to the latest
patch release of that series. The 3 newest major and 10 newest minor versions per major are published; `latest`
points to the newest one.

## Usage

```bash
docker run -d --name buildkitd --privileged -p 8372:8372 \
  ghcr.io/containerhive/helper-images/buildkit:v0.34 --addr tcp://0.0.0.0:8372
```
