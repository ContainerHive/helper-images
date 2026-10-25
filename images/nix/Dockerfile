ARG NIX_VERSION
FROM nixos/nix:${NIX_VERSION}
ARG NIX_VERSION
COPY nix.conf /etc/nix/nix.conf
LABEL nix.version="${NIX_VERSION}"
