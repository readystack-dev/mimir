# Provenance — Mimir (`3.2.4-CE-ubuntu24.04-r2`)

Every item below is copied from a record in this archive; the record is named in brackets.

## Source

- Upstream repository: https://github.com/grafana/mimir
- Revision built: `mimir-3.2.4` (commit `4380c3492730d7fca3bc90e292aefe7fb6e8c42e`)
- Source tree: `c72aaf5b55bf2d3c82728908b33d3d70148399c3571b41d10a10673e456afe82` over 15473 files [`docs/provenance/SOURCE_TREE_HASH.json`]
- Community Edition only: enterprise code is removed or refused before the build (CE audit at acquire).

## Build

- Method: `source-rebuild-go`; base image `scratch + a chiselled Ubuntu 24.04 runtime (vendored/chisel/slices.txt, packages.tsv)`
- Compiled with `--network=none` from vendored source, dependencies and base images; BuildKit pinned to `moby/buildkit:v0.31.2` (shipped in `toolchain/`).
- SOURCE_DATE_EPOCH: `1793383897` [`SOURCE_DATE_EPOCH.txt`]
- Frozen inputs: [`docs/provenance/FREEZE_MANIFEST.json`], build recipe: [`docs/provenance/BUILD_RECIPE.json`].

## Output

- Published image: `readystack/mimir:3.2.4-CE-ubuntu24.04-r2` — index digest `sha256:9126a23a1555c034ad7f7b49e51e75782924bf8e7266edf24a5972440fe68070` [`docs/provenance/LOCKED_DIGEST.txt`]
- linux/amd64 image digest `sha256:15b9b2af9b5fcb7c8d3d42df9bca30053e9843326e2f6013100cc1d949c6184b` — reproduced from this archive before publishing [`docs/provenance/REPRO_VERIFICATION.json`].

## Attestations and signature

- SBOM + SLSA provenance attached to the image: attached: an SPDX SBOM and SLSA v1 provenance [`docs/provenance/SCOUT_VERDICT.json`]
- cosign signature by the ReadyStack release key: verified before publishing. Check it: `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/mimir:3.2.4-CE-ubuntu24.04-r2`

## Pinned inputs, and why

- 28 pinned inputs, each with where it came from, why this one, how it was checked and when it was decided: `docs/PINS.md` [`docs/provenance/PINS.json`] (upstream source 2, base and build images 3, image digests 2, dependency versions readystack sets 6, pins in the kit's dockerfiles 8, readystack's build engine 5, dependencies upstream chose 2).

## Build trail

- How this release passed through the ReadyStack harness, record by record (every chain, drive, stage, review round, defect and check, each naming the record it is copied from): `ReadyStack-mimir-3.2.4-CE-ubuntu24.04-r2.trail.json`, published beside this archive and signed with the release key (`ReadyStack-mimir-3.2.4-CE-ubuntu24.04-r2.trail.json.sigstore`), and readable at https://readystack.dev/products/mimir/trail/3.2.4-CE-ubuntu24.04-r2.

