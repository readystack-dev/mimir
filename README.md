# Mimir: ReadyStack build kit

The offline build kit for the Docker image `readystack/mimir:3.2.4-CE-ubuntu24.04-r2`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [3.2.4-CE-ubuntu24.04-r2](https://github.com/readystack-dev/mimir/releases/tag/3.2.4-CE-ubuntu24.04-r2)
- Image: [`docker.io/readystack/mimir:3.2.4-CE-ubuntu24.04-r2`](https://hub.docker.com/r/readystack/mimir/tags), manifest digest `sha256:15b9b2af9b5fcb7c8d3d42df9bca30053e9843326e2f6013100cc1d949c6184b`
- Product page: https://readystack.dev/products/mimir
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=mimir

Mimir is distributed under its upstream licence (AGPL-3.0-only); the kit contains upstream's source under that licence, and each vendored component under its own.

## Download

From the [3.2.4-CE-ubuntu24.04-r2 release](https://github.com/readystack-dev/mimir/releases/tag/3.2.4-CE-ubuntu24.04-r2): `ReadyStack-mimir-3.2.4-CE-ubuntu24.04-r2.tar.gz` (499.0 MB), SHA-256 `b0c12868f06602645cba32e2abe030c0a09b4e3c118142cc6eabe6deb7801e60`.

```sh
sha256sum --check --ignore-missing SHA256SUMS
```

## Verify and rebuild

The rebuild statement is signed with the ReadyStack release key. Check the signature before you rely on it:

```sh
cosign verify-blob --key https://readystack.dev/keys/cosign.pub \
  --bundle ReadyStack-mimir-3.2.4-CE-ubuntu24.04-r2.rebuild.json.sigstore ReadyStack-mimir-3.2.4-CE-ubuntu24.04-r2.rebuild.json
```

Unpack with `-p` so file modes are kept, then follow the kit's own README.md and docs/REBUILD.md:

```sh
tar -xpzf ReadyStack-mimir-3.2.4-CE-ubuntu24.04-r2.tar.gz
cd 3.2.4-CE-ubuntu24.04-r2
less README.md docs/REBUILD.md
```

The build trail (`ReadyStack-mimir-3.2.4-CE-ubuntu24.04-r2.trail.json`, signed the same way, and its Markdown copy) records how this release was built and checked.

## This repository

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/mimir/recipe. The complete kit is the release download. Each release is a tag here.
