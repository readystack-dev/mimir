[![ReadyStack](https://readystack.dev/logo.svg)](https://readystack.dev)

**Stable, Open-source Releases, Automated** · [readystack.dev](https://readystack.dev)

[![Docker Hub](https://img.shields.io/badge/Docker%20Hub-readystack%2Fmimir-2496ED?logo=docker&logoColor=white)](https://hub.docker.com/r/readystack/mimir) [![Docker pulls](https://img.shields.io/docker/pulls/readystack/mimir)](https://hub.docker.com/r/readystack/mimir) [![Grade at release](https://img.shields.io/badge/grade%20at%20release-A%20%2894%25%29-2ea44f)](https://readystack.dev/products/mimir) [![Signed: cosign](https://img.shields.io/badge/signed-cosign-2ea44f)](https://readystack.dev/keys/cosign.pub) ![SBOM: SPDX](https://img.shields.io/badge/SBOM-SPDX-2ea44f) ![Provenance: SLSA v1](https://img.shields.io/badge/provenance-SLSA%20v1-2ea44f) ![Offline rebuild: verified](https://img.shields.io/badge/offline%20rebuild-verified-2ea44f)

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

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/mimir/recipe. The complete kit is the release download. Each release is a tag here. How to report a vulnerability: [SECURITY.md](SECURITY.md).

## About ReadyStack

**Stable, Open-source Releases, Automated.** ReadyStack releases popular open-source apps every week with every available critical and high security fix applied, plus full documentation, reference data, tests and a build recipe that recreates each release bit-for-bit. Each release is rebuilt from its pinned inputs with the network off, checked against its published digest, signed, and scanned and graded again every day. The images and build kits are free, and ReadyStack is soon to be a nonprofit.

[readystack.dev](https://readystack.dev) · [All products](https://readystack.dev/products.html) · [Build kits on GitHub](https://github.com/readystack-dev) · [Defect log](https://readystack.dev/defects.html) · contact@readystack.dev

— ReadyStack · https://readystack.dev
