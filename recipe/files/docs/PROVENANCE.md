# Provenance — Mimir (`3.2.6-CE-ubuntu24.04-r1`)

Every item below is copied from a record in this archive; the record is named in brackets.

## Source

- Upstream repository: https://github.com/grafana/mimir
- Revision built: `mimir-3.2.6` (commit `634964f9567675883abf003393e9cd1cafcc584e`)
- Source tree: `4ff4b9b5271611b366e5c3be6dd22eec76c0ec68485970143689094481f18896` over 15564 files [`docs/provenance/SOURCE_TREE_HASH.json`]
- Community Edition only: enterprise code is removed or refused before the build (CE audit at acquire).

## Build

- Method: `source-rebuild-go`; base image `scratch + a chiselled Ubuntu 24.04 runtime (vendored/chisel/slices.txt, packages.tsv)`
- Compiled with `--network=none` from vendored source, dependencies and base images; BuildKit pinned to `moby/buildkit:v0.31.2` (shipped in `toolchain/`).
- SOURCE_DATE_EPOCH: `1795446614` [`SOURCE_DATE_EPOCH.txt`]
- Frozen inputs: [`docs/provenance/FREEZE_MANIFEST.json`], build recipe: [`docs/provenance/BUILD_RECIPE.json`].

## Output

- Published image: `readystack/mimir:3.2.6-CE-ubuntu24.04-r1` — index digest `sha256:7ece3b3dc1d791d948d9d6c866f328c94f74e98c91dbba676091a93a90eaecb7` [`docs/provenance/LOCKED_DIGEST.txt`]
- linux/amd64 image digest `sha256:4c277a1cad1c62194c0a4c95d6a8d7fc5e95a9ee5cb46afab24781e74bcd186d` — reproduced from this archive before publishing [`docs/provenance/REPRO_VERIFICATION.json`].

## Attestations and signature

- SBOM + SLSA provenance attached to the image: attached: an SPDX SBOM and SLSA v1 provenance [`docs/provenance/SCOUT_VERDICT.json`]
- cosign signature by the ReadyStack release key: verified before publishing. Check it: `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/mimir:3.2.6-CE-ubuntu24.04-r1`

## Pinned inputs, and why

- 28 pinned inputs, each with where it came from, why this one, how it was checked and when it was decided: `docs/PINS.md` [`docs/provenance/PINS.json`] (upstream source 2, base and build images 3, image digests 2, dependency versions readystack sets 6, pins in the kit's dockerfiles 8, readystack's build engine 5, dependencies upstream chose 2).

## Build trail

- How this release passed through the ReadyStack harness, record by record (every chain, drive, stage, review round, defect and check, each naming the record it is copied from): `ReadyStack-mimir-3.2.6-CE-ubuntu24.04-r1.trail.json`, published beside this archive and signed with the release key (`ReadyStack-mimir-3.2.6-CE-ubuntu24.04-r1.trail.json.sigstore`), and readable at https://readystack.dev/products/mimir/trail/3.2.6-CE-ubuntu24.04-r1.

