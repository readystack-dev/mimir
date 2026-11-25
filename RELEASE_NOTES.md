# Mimir 3.2.4 — ReadyStack release `3.2.4-CE-ubuntu24.04-r2`

Generated 2026-11-09 from this release's build records and strategy. Statements that come from a single record name it in brackets; the others come from this release's strategy and build log.

## Release

- **Image:** `readystack/mimir:3.2.4-CE-ubuntu24.04-r2` (linux/amd64). Index digest `sha256:9126a23a1555c034ad7f7b49e51e75782924bf8e7266edf24a5972440fe68070` [`docs/provenance/LOCKED_DIGEST.txt`].
- **Image manifest digest:** `sha256:15b9b2af9b5fcb7c8d3d42df9bca30053e9843326e2f6013100cc1d949c6184b` [`TARGET_DIGEST.txt`].
- **Upstream:** Mimir 3.2.4 built from source at `mimir-3.2.4` of https://github.com/grafana/mimir — upstream notes: https://github.com/grafana/mimir/releases/tag/mimir-3.2.4 [`docs/provenance/BUILD_RECIPE.json`].
- **Base image:** none (`FROM scratch`): a chiselled Ubuntu 24.04 runtime, the files Canonical's chisel cut from Ubuntu's own packages (`vendored/chisel/slices.txt`, `vendored/chisel/packages.tsv`); runtime user `mimir`.
- **Build:** `source-rebuild-go`, compiled offline with `--network=none`.
- **Supersedes:** ReadyStack release `3.2.4-CE-ubuntu24.04-r1`.

## What changed in this release

- Upstream version unchanged (3.2.4); ReadyStack rebuild.
- Minimum dependency versions ReadyStack enforces on top of upstream (raised only where upstream's own version was lower); shipped versions from the SBOM [`docs/sbom/SBOM.json`]:
  - `github.com/go-jose/go-jose/v4` at least `v4.1.6`: not raised, upstream already pins `v4.1.6` (shipped: `v4.1.6`)
  - `golang.org/x/net` at least `v0.62.0`: not raised, upstream already pins `v0.62.0` (shipped: `v0.62.0`)
  - `github.com/klauspost/compress` raised from upstream's `v1.19.0` to at least `v1.20.2` (shipped: `v1.20.2`)
- Grafana Mimir 3.2.4 is unchanged from the release this supersedes (3.2.4-CE-ubuntu24.04-r1); this release rebuilds it on a slim base. Changes: the image no longer starts from the full ubuntu:24.04 image. It is built FROM scratch with a chiselled Ubuntu 24.04 runtime: only the files that Canonical's chisel cut from a few Ubuntu packages (base-files, base-passwd, ca-certificates, tzdata, the dash shell, part of coreutils, GNU tar for a backup of the data volume with --entrypoint tar, and the libraries they need; the list is vendored/chisel/packages.tsv in the release archive). The image has a POSIX shell (/bin/sh) but no bash, curl, grep, ls or id, and its HEALTHCHECK runs /usr/local/bin/rs-probe, a small HTTP probe built from source in the kit, instead of curl. The mimir and mimirtool binaries, the configuration /etc/mimir/config.yaml (-target=all), the ports, the data path /var/mimir and the runtime user (uid 999) are those of 3.2.4-CE-ubuntu24.04-r1: replace the container with this image on the same volume.

## Security status at release (measured 2026-11-09)

- **Docker Scout:** 0 fixable critical/high vulnerabilities; runs as `mimir` (non-root); SBOM + provenance attestations present (SPDX SBOM + SLSA v1) [`docs/provenance/SCOUT_VERDICT.json`].
- **OSV cross-check:** no fixable critical/high vulnerability beyond Docker Scout's findings.
- **Signature:** cosign signature verified by ReadyStack's release gate before publishing; check it yourself with `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/mimir:3.2.4-CE-ubuntu24.04-r2` (signatures are recorded in the public Sigstore transparency log).
- **ReadyStack release check at release:** passed (ReadyStack's own test, not a Docker Scout grade). Vulnerabilities are disclosed every day and the image never changes, so it is re-checked daily, beside Docker Scout's own dated grade, at https://readystack.dev/queue.

## Reproducibility

Rebuilds offline from this archive to the identical image digest `sha256:15b9b2af9b5fcb7c8d3d42df9bca30053e9843326e2f6013100cc1d949c6184b`: run `./BUILD_OFFLINE.sh`, then `./VERIFY_OFFLINE.sh` (add `--online` to confirm the Docker Hub tag holds the same digest). Before publishing, ReadyStack rebuilt the kit with `./BUILD_OFFLINE.sh` and compared the result with the published digest [`docs/provenance/REPRO_VERIFICATION.json`], then ran `./BUILD_OFFLINE.sh` and `./VERIFY_OFFLINE.sh` from this archive (without `--online`).

## Validation

- 6 of 6 use cases passed (6 authored) against the running image [`docs/validation/test-results.json`].

## Known issues

- None recorded.

## Defects fixed

- 25 problems found before release and fixed before it shipped (25 by review); each is listed in `docs/defects/defects.json`.

## Verify this archive

```
sha256sum -c CHECKSUMS.sha256
./BUILD_OFFLINE.sh && ./VERIFY_OFFLINE.sh --online
cosign verify --key https://readystack.dev/keys/cosign.pub readystack/mimir:3.2.4-CE-ubuntu24.04-r2
```

ReadyStack records every signature in the public Sigstore transparency log (Rekor), so the command needs no extra flags.

