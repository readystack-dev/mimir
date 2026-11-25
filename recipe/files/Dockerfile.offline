# GENERATED L-009 hermetic build (--network=none, SBOM+SLSA-attestation-producing).
# Pinned bases from BASE_IMAGE_DIGESTS.lock; vendored Go tree + debs from Dockerfile.vendor.
FROM golang:1.26.10-bookworm@sha256:632dff7351799a5a9954a48dc06670ade72ee44e8c351cdc0e5a57af2fea21af AS build_mimir
WORKDIR /src
COPY vendored/mimir-src/ .
ENV CGO_ENABLED=0 GOTOOLCHAIN=local GOWORK=off GOFLAGS="-mod=vendor -buildvcs=false" GOPROXY=off SOURCE_DATE_EPOCH=1793383897
RUN go build -trimpath -tags "netgo stringlabels" -ldflags='-s -w -X github.com/grafana/mimir/pkg/util/version.Version=3.2.4 -X github.com/grafana/mimir/pkg/util/version.Branch=HEAD -X github.com/grafana/mimir/pkg/util/version.Revision=4380c349' -o /mimir ./cmd/mimir && /mimir -version && \
    { readelf -lW /mimir | sed -n 's/.*Requesting program interpreter: \(.*\)]$/\1/p'; readelf -dW /mimir | sed -n 's/.*Shared library: \[\(.*\)\]$/\1/p'; } > /mimir.needs
FROM golang:1.26.10-bookworm@sha256:632dff7351799a5a9954a48dc06670ade72ee44e8c351cdc0e5a57af2fea21af AS build_mimirtool
WORKDIR /src
COPY vendored/mimir-src/ .
ENV CGO_ENABLED=0 GOTOOLCHAIN=local GOWORK=off GOFLAGS="-mod=vendor -buildvcs=false" GOPROXY=off SOURCE_DATE_EPOCH=1793383897
RUN go build -trimpath -tags "netgo stringlabels" -ldflags='-s -w' -o /mimirtool ./cmd/mimirtool && /mimirtool --help && \
    { readelf -lW /mimirtool | sed -n 's/.*Requesting program interpreter: \(.*\)]$/\1/p'; readelf -dW /mimirtool | sed -n 's/.*Shared library: \[\(.*\)\]$/\1/p'; } > /mimirtool.needs
# rs-probe: the HEALTHCHECK helper (standard library only, from the kit's rs-probe.go)
FROM golang:1.26.10-bookworm@sha256:632dff7351799a5a9954a48dc06670ade72ee44e8c351cdc0e5a57af2fea21af AS build_rs_probe
WORKDIR /probe
COPY rs-probe.go main.go
COPY rs-probe.mod go.mod
ENV CGO_ENABLED=0 GOTOOLCHAIN=local GOFLAGS="-buildvcs=false" GOPROXY=off SOURCE_DATE_EPOCH=1793383897
RUN go build -trimpath -ldflags='-s -w' -o /rs-probe .
# the chiselled rootfs (vendored/chisel, cut by Dockerfile.vendor), the service user, the binaries
FROM ubuntu:24.04@sha256:fe81560990fae86dc4743202b2cb4d3df98d0bcf949173cecef15ce1127ef852 AS rootfs
ARG SOURCE_DATE_EPOCH=1793383897
ADD vendored/chisel/rootfs.tar /rootfs/
RUN printf 'mimir:x:999:999::/var/mimir:/bin/sh\n' >> /rootfs/etc/passwd && printf 'mimir:x:999:\n' >> /rootfs/etc/group && \
    mkdir -p /rootfs/var/mimir /rootfs/etc/mimir /rootfs/var/mimir/tsdb /rootfs/var/mimir/tsdb-sync /rootfs/var/mimir/data/tsdb /rootfs/var/mimir/compactor /rootfs/var/mimir/rules && chown -R 999:999 /rootfs/var/mimir /rootfs/etc/mimir /rootfs/var/mimir/tsdb /rootfs/var/mimir/tsdb-sync /rootfs/var/mimir/data/tsdb /rootfs/var/mimir/compactor /rootfs/var/mimir/rules
COPY --from=build_mimir /mimir /rootfs/usr/bin/mimir
COPY --from=build_mimir /mimir.needs /tmp/needs/mimir
COPY --from=build_mimirtool /mimirtool /rootfs/usr/bin/mimirtool
COPY --from=build_mimirtool /mimirtool.needs /tmp/needs/mimirtool
COPY --from=build_rs_probe /rs-probe /rootfs/usr/local/bin/rs-probe
COPY mimir-config.yaml /rootfs/etc/mimir/config.yaml
RUN chmod 755 /rootfs/usr/bin/mimir /rootfs/usr/bin/mimirtool /rootfs/usr/local/bin/rs-probe && \
    chown 999:999 /rootfs/etc/mimir/config.yaml && \
    chmod 0644 /rootfs/etc/mimir/config.yaml
RUN --mount=type=bind,source=vendored/chisel,target=/chisel set -eu; \
    for n in /tmp/needs/*; do while read -r lib; do [ -n "$lib" ] || continue; \
      case "$lib" in /*) [ -e "/rootfs$lib" ] ;; *) [ -n "$(find /rootfs/usr/lib /rootfs/usr/lib64 -name "$lib" 2>/dev/null | head -1)" ] ;; esac || \
      { echo "$(basename "$n") needs $lib, which the chiselled rootfs does not have: add its slice to runtime_base.slices" >&2; exit 1; }; \
    done < "$n"; done; rm -rf /tmp/needs; \
    [ -e /rootfs/etc/os-release ] || { echo "no /etc/os-release: base-files_release-info is missing" >&2; exit 1; }; \
    [ "$(grep -c '^Package: ' /rootfs/var/lib/dpkg/status)" = "$(wc -l < /chisel/packages.tsv)" ] || \
      { echo "/var/lib/dpkg/status does not list every package of vendored/chisel/packages.tsv" >&2; exit 1; }; \
    rm -rf /rootfs/var/log/dpkg.log /rootfs/var/log/alternatives.log /rootfs/var/log/apt /rootfs/var/cache/ldconfig/aux-cache /rootfs/var/cache/fontconfig
FROM scratch
ARG SOURCE_DATE_EPOCH=1793383897
COPY --from=rootfs /rootfs/ /
ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
LABEL org.opencontainers.image.licenses="AGPL-3.0-only"
LABEL com.readystack.license.disclosure="This image includes Grafana Mimir (https://github.com/grafana/mimir), licensed under AGPL-3.0-only. Modifications: the build raises Go-module dependency versions in go.mod and go.sum where upstream's are older than the fixed, upstream-published releases (security updates; no Mimir source file is edited); full diff of every upstream file the build changes at https://readystack.dev/source/mimir/3.2.4/mimir-3.2.4-readystack.patch (empty when the build changes none). The upstream source is https://github.com/grafana/mimir/tree/mimir-3.2.4. Operating-system packages come from Ubuntu's archive, unmodified. ReadyStack license holders have access to the image build recipe and patched-package manifest on request via contact@readystack.dev."
LABEL org.opencontainers.image.title="Mimir"
LABEL org.opencontainers.image.source="https://github.com/grafana/mimir"
LABEL org.opencontainers.image.version="3.2.4-CE-ubuntu24.04-r2"
LABEL org.opencontainers.image.revision="4380c3492730d7fca3bc90e292aefe7fb6e8c42e"
HEALTHCHECK --interval=5s --timeout=30s --start-period=90s \
  CMD /usr/local/bin/rs-probe http://127.0.0.1:8080/ready || exit 1
WORKDIR /var/mimir
USER mimir
EXPOSE 8080 9095
ENTRYPOINT ["mimir", "-config.file=/etc/mimir/config.yaml", "-target=all"]
