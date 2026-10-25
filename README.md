# helper-images

Helper images for [ContainerHive](https://github.com/ContainerHive/ContainerHive), built with ContainerHive itself and
published to `ghcr.io/containerhive/helper-images`.

| Image                                                                 | Contents                                  | Tracked versions                                  |
|:----------------------------------------------------------------------|:------------------------------------------|:--------------------------------------------------|
| [`chisel`](images/chisel/README.md)                                   | [Canonical Chisel](https://github.com/canonical/chisel) on Ubuntu 24.04 | last 3 majors, 10 minors each, latest patch |
| [`nix`](images/nix/README.md)                                         | [Nix](https://nixos.org) with flakes enabled | last 3 majors, 15 minors each, latest patch (Nix 2.4+) |

Tags are resolved from the upstream releases by `tag_ranges` (see each `image.yml`), so new series show up without
editing the repository.

## How the CI works

- `.github/workflows/build.yml` is generated with `ch template ci --provider github`. Do not edit it by hand.
- `.github/workflows/sync-ci.yml` runs daily, regenerates the build workflow and opens a PR when the resolved tag
  ranges changed it. It needs a `CI_SYNC_TOKEN` secret (fine-grained PAT or GitHub App token with `contents`,
  `pull-requests` and `workflows` write access), because `GITHUB_TOKEN` cannot push workflow files.
- The build workflow needs the `CONTAINER_HIVE_REGISTRY_USERNAME` and `CONTAINER_HIVE_REGISTRY_PASSWORD` secrets
  and GitHub Pages enabled with the source set to "GitHub Actions" (for the report).

## Local development

```bash
ch generate   # renders images to dist/
ch lint
```
