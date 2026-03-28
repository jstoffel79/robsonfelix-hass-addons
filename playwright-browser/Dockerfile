# Hardcode the image to bypass Home Assistant OS injection
FROM mcr.microsoft.com/playwright:v1.57.0-noble

# Modern OCI and HA Labels
LABEL org.opencontainers.image.authors="Robson Felix"
LABEL io.hass.version="0.1.0"
LABEL io.hass.type="addon"
LABEL io.hass.arch="amd64,aarch64"
LABEL org.opencontainers.image.title="Playwright Browser for Home Assistant"
LABEL org.opencontainers.image.description="Headless Chromium with CDP endpoint for browser automation"

# Install dependencies (apt-get will absolutely work now)
RUN apt-get update && \
    apt-get install -y --no-install-recommends jq curl nginx && \
    rm -rf /var/lib/apt/lists/*

# Create data directory
RUN mkdir -p /data

# Copy your bash script directly
COPY run.sh /run.sh
RUN chmod +x /run.sh

# Expose CDP port
EXPOSE 9222

# Execute the script
CMD ["/run.sh"]
