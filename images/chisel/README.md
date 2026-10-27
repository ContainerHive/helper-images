# Chisel

[Canonical Chisel](https://github.com/canonical/chisel) on Ubuntu 24.04, with `ca-certificates` and `git`.
Use it to cut slices from [chisel-releases](https://github.com/canonical/chisel-releases) in CI or in a multi-stage
build.

Tags follow the Chisel release series (`1.5`, `1.4`, ...) and point to the latest patch release of that series. The
3 newest major and 10 newest minor versions per major are published; `latest` points to the newest one.

## Usage

```bash
docker run --rm ghcr.io/containerhive/helper-images/chisel:latest version
```

```dockerfile
FROM ghcr.io/containerhive/helper-images/chisel:1.5 AS cut
RUN chisel cut --release ubuntu-26.04 --root /rootfs base-files_base ca-certificates_data
```
