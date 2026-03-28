# Provide a Debian base image fallback to clear the build warning
ARG BUILD_FROM=ghcr.io/home-assistant/amd64-base-debian:latest
FROM ${BUILD_FROM}

# Modern OCI and HA Labels
LABEL org.opencontainers.image.authors="Robson Felix"
LABEL io.hass.version="0.1.0"
LABEL io.hass.type="addon"
LABEL io.hass.arch="amd64,aarch64"
LABEL org.opencontainers.image.title="Playwright Browser for Home Assistant"
LABEL org.opencontainers.image.description="Headless Chromium with CDP endpoint for browser automation"
LABEL org.opencontainers.image.source="https://github.com/robsonfelix/robsonfelix-hass-addons"
LABEL org.opencontainers.image.licenses="MIT"

# Install dependencies (apt-get will now work because of the Debian base)
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    jq \
    curl \
    nginx \
    && rm -rf /var/lib/apt/lists/*

# Create data directory
RUN mkdir -p /data

# Copy the root filesystem
# This maps your local rootfs/ folder into the container to utilize s6-overlay.
COPY rootfs /

# Expose CDP port
EXPOSE 9222

# Note: The HA base image uses s6-overlay as its ENTRYPOINT. 
# We intentionally omit CMD and ENTRYPOINT here so s6 takes over and 
# executes your run script located in rootfs/etc/services.d/playwright/run
