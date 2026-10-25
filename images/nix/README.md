# Nix

The official [`nixos/nix`](https://hub.docker.com/r/nixos/nix) image with the `nix-command` and `flakes` experimental
features enabled and the sandbox disabled, so `nix build .#...` works inside container builds.

Tags follow the Nix release series (`2.35`, `2.34`, ...) and point to the latest patch release of that series. The
3 newest major and 15 newest minor versions per major are published; `latest` points to the newest one.

## Usage

```bash
docker run --rm ghcr.io/containerhive/helper-images/nix:latest nix --version
```

```yaml
# image.yml of a ContainerHive image using the nix build backend
nix:
  builder_image: "ghcr.io/containerhive/helper-images/nix:2.35"
```
