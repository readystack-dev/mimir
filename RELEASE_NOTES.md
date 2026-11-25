# Mimir 3.2.6 — ReadyStack release `3.2.6-CE-ubuntu24.04-r1`

Generated 2026-11-25 from this release's build records and strategy. Statements that come from a single record name it in brackets; the others come from this release's strategy and build log.

## Release

- **Image:** `readystack/mimir:3.2.6-CE-ubuntu24.04-r1` (linux/amd64). Index digest `sha256:7ece3b3dc1d791d948d9d6c866f328c94f74e98c91dbba676091a93a90eaecb7` [`docs/provenance/LOCKED_DIGEST.txt`].
- **Image manifest digest:** `sha256:4c277a1cad1c62194c0a4c95d6a8d7fc5e95a9ee5cb46afab24781e74bcd186d` [`TARGET_DIGEST.txt`].
- **Upstream:** Mimir 3.2.6 built from source at `mimir-3.2.6` of https://github.com/grafana/mimir — upstream notes: https://github.com/grafana/mimir/releases/tag/mimir-3.2.6 [`docs/provenance/BUILD_RECIPE.json`].
- **Base image:** none (`FROM scratch`): a chiselled Ubuntu 24.04 runtime, the files Canonical's chisel cut from Ubuntu's own packages (`vendored/chisel/slices.txt`, `vendored/chisel/packages.tsv`); runtime user `mimir`.
- **Build:** `source-rebuild-go`, compiled offline with `--network=none`.
- **Supersedes:** ReadyStack release `3.2.4-CE-ubuntu24.04-r2`.

## What changed in this release

- Upstream version 3.2.4 → 3.2.6.
- Minimum dependency versions ReadyStack enforces on top of upstream (raised only where upstream's own version was lower); shipped versions from the SBOM [`docs/sbom/SBOM.json`]:
  - `github.com/go-jose/go-jose/v4` at least `v4.1.6`: not raised, upstream already pins `v4.1.6` (shipped: `v4.1.6`)
  - `golang.org/x/net` at least `v0.62.0`: not raised, upstream already pins `v0.62.0` (shipped: `v0.62.0`)
  - `github.com/klauspost/compress` at least `v1.20.2`: not raised, upstream already pins `v1.20.2` (shipped: `v1.20.2`)
- This release moves Mimir from 3.2.4 to 3.2.6, a newer release of upstream's 3.2.x line. Upstream's release notes list what changed: https://github.com/grafana/mimir/releases/tag/mimir-3.2.6 Upstream's 3.2.6 moves OpenTelemetry Go to 1.47.0 and its OTLP log exporter to 0.23.0, which fixes the medium advisories ReadyStack's daily scan found in 3.2.4's mimir and mimirtool binaries (GHSA-q7gw-24fr-5p69, GHSA-hjf4-fphr-2h65, GHSA-w34q-cm8f-9c5x); it builds on Go 1.26.11. Settings, ports and data volumes are those of 3.2.4: replace the container with this image on the same volumes.

## Security status at release (measured 2026-11-23)

- **Docker Scout:** 0 fixable critical/high vulnerabilities; runs as `mimir` (non-root); SBOM + provenance attestations present (SPDX SBOM + SLSA v1) [`docs/provenance/SCOUT_VERDICT.json`].
- **OSV cross-check:** no fixable critical/high vulnerability beyond Docker Scout's findings.
- **Signature:** cosign signature verified by ReadyStack's release gate before publishing; check it yourself with `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/mimir:3.2.6-CE-ubuntu24.04-r1` (signatures are recorded in the public Sigstore transparency log).
- **ReadyStack release check at release:** passed (ReadyStack's own test, not a Docker Scout grade). Vulnerabilities are disclosed every day and the image never changes, so it is re-checked daily, beside Docker Scout's own dated grade, at https://readystack.dev/queue.

## Reproducibility

Rebuilds offline from this archive to the identical image digest `sha256:4c277a1cad1c62194c0a4c95d6a8d7fc5e95a9ee5cb46afab24781e74bcd186d`: run `./BUILD_OFFLINE.sh`, then `./VERIFY_OFFLINE.sh` (add `--online` to confirm the Docker Hub tag holds the same digest). Before publishing, ReadyStack rebuilt the kit with `./BUILD_OFFLINE.sh` and compared the result with the published digest [`docs/provenance/REPRO_VERIFICATION.json`], then ran `./BUILD_OFFLINE.sh` and `./VERIFY_OFFLINE.sh` from this archive (without `--online`).

## Validation

- 6 of 6 use cases passed (6 authored) against the running image [`docs/validation/test-results.json`].

## Known issues

- None recorded.

## Defects fixed

- 28 problems found before release and fixed before it shipped (28 by review); each is listed in `docs/defects/defects.json`.

## Verify this archive

```
sha256sum -c CHECKSUMS.sha256
./BUILD_OFFLINE.sh && ./VERIFY_OFFLINE.sh --online
cosign verify --key https://readystack.dev/keys/cosign.pub readystack/mimir:3.2.6-CE-ubuntu24.04-r1
```

ReadyStack records every signature in the public Sigstore transparency log (Rekor), so the command needs no extra flags.

