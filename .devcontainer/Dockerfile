# Go devcontainer base (includes Go toolchain + vscode user)
#ARG GO_VARIANT="1-1.22-bookworm"
#FROM mcr.microsoft.com/devcontainers/go:${GO_VARIANT}
FROM mcr.microsoft.com/devcontainers/go:latest

# Version of Hugo Extended to install – passed from devcontainer.json
ARG HUGO_VERSION=0.124.1
ARG TARGETARCH

# Basic deps
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
        git \
    && rm -rf /var/lib/apt/lists/*

# Install Hugo Extended (different .deb per arch)
RUN case "${TARGETARCH:-amd64}" in \
        "arm64")  ARCH="arm64" ;; \
        "arm")    ARCH="armhf" ;; \
        *)        ARCH="amd64" ;; \
    esac && \
    curl -L "https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-${ARCH}.deb" \
      -o /tmp/hugo_extended.deb && \
    apt-get update && \
    apt-get install -y /tmp/hugo_extended.deb && \
    rm -rf /var/lib/apt/lists/* /tmp/hugo_extended.deb && \
    hugo version

# Default workdir when the container opens
WORKDIR /workspaces/tomblogs24
