# Mimir: ReadyStack build kit

The offline build kit for the Docker image `readystack/mimir:3.2.6-CE-ubuntu24.04-r1`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [3.2.6-CE-ubuntu24.04-r1](https://github.com/readystack-dev/mimir/releases/tag/3.2.6-CE-ubuntu24.04-r1)
- Image: [`docker.io/readystack/mimir:3.2.6-CE-ubuntu24.04-r1`](https://hub.docker.com/r/readystack/mimir/tags), manifest digest `sha256:4c277a1cad1c62194c0a4c95d6a8d7fc5e95a9ee5cb46afab24781e74bcd186d`
- Product page: https://readystack.dev/products/mimir
- Source and build recipe: https://readystack.dev/products/mimir/recipe
- Build trail: https://readystack.dev/products/mimir/trail/3.2.6-CE-ubuntu24.04-r1
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=mimir

## The image

ReadyStack Mimir Community Edition build kit.

## Who uses Mimir and why

Platform and SRE teams who need to keep and query metrics from many clusters and teams over long periods.

Grafana Mimir is horizontally scalable, highly available, multi-tenant long-term storage for Prometheus and OpenTelemetry metrics, with queries that aggregate series from many sources into a global view.

A typical use: A company runs a Prometheus server in each of its clusters, each keeping only recent data. They all send metrics to Mimir, which keeps them durably in object storage, and engineers query months of history across every cluster at once from one place.

From the upstream project's own description: https://github.com/grafana/mimir, https://grafana.com/docs/mimir/latest/.

## This release

- Docker Scout policy grade at release: **A** (94%), graded 2026-11-25 with `docker scout policy` (CLI 1.26.0, docker-default configuration).
  - Docker Scout counts 10 packages with copyleft licences (GPL, LGPL, MPL), all of them operating-system packages (it counts only packages whose licence it can read; the SBOM lists every component).
- Signed with ReadyStack's release key (fingerprint `04daa92344a52dbc`): https://readystack.dev/keys/cosign.pub.
- Runs as a non-root user (`mimir`).
- Attestations on the image: an SPDX SBOM and SLSA provenance v1.
- Rebuilt from this kit with network egress blocked on 2026-11-25; the rebuilt image digest is the published one.
- Base: Ubuntu 24.04.

The current grade, measured again every day, is on https://readystack.dev/products/mimir.

Mimir is distributed under its upstream licence (AGPL-3.0-only); the kit contains upstream's source under that licence, and each vendored component under its own.

## Download

From the [3.2.6-CE-ubuntu24.04-r1 release](https://github.com/readystack-dev/mimir/releases/tag/3.2.6-CE-ubuntu24.04-r1): `ReadyStack-mimir-3.2.6-CE-ubuntu24.04-r1.tar.gz` (499.7 MB), SHA-256 `a87c6535494edd209593ee4afd8b21b1fb5436dccd78084e00e59de1275edd49`.

```sh
sha256sum --check --ignore-missing SHA256SUMS
```

## Verify and rebuild

The rebuild statement is signed with the ReadyStack release key. Check the signature before you rely on it:

```sh
cosign verify-blob --key https://readystack.dev/keys/cosign.pub \
  --bundle ReadyStack-mimir-3.2.6-CE-ubuntu24.04-r1.rebuild.json.sigstore ReadyStack-mimir-3.2.6-CE-ubuntu24.04-r1.rebuild.json
```

Unpack with `-p` so file modes are kept, then follow the kit's own README.md and docs/REBUILD.md:

```sh
tar -xpzf ReadyStack-mimir-3.2.6-CE-ubuntu24.04-r1.tar.gz
cd 3.2.6-CE-ubuntu24.04-r1
less README.md docs/REBUILD.md
```

The build trail (`ReadyStack-mimir-3.2.6-CE-ubuntu24.04-r1.trail.json`, signed the same way, and its Markdown copy) records how this release was built and checked.

## This repository

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/mimir/recipe. The complete kit is the release download. Each release is a tag here.

— ReadyStack · https://readystack.dev
