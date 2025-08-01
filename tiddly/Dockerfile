# Define base image (Home Assistant base add-on image)
ARG BUILD_FROM=ghcr.io/hassio-addons/base:18.0.3
FROM ${BUILD_FROM}

# Architecture information passed by HA build system
ARG BUILD_ARCH
ARG BUILD_VERSION
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_NAME
ARG BUILD_DESCRIPTION

# Labels for container metadata
LABEL \
  io.hass.name="${BUILD_NAME}" \
  io.hass.description="${BUILD_DESCRIPTION}" \
  io.hass.arch="${BUILD_ARCH}" \
  io.hass.version="${BUILD_VERSION}" \
  org.opencontainers.image.title="${BUILD_NAME}" \
  org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
  org.opencontainers.image.version="${BUILD_VERSION}" \
  org.opencontainers.image.created="${BUILD_DATE}" \
  org.opencontainers.image.revision="${BUILD_REF}" \
  org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
  maintainer="Tuan Dangschulz <tuan@example.com>"

RUN mkdir -p /var/db/tiddly

# Copy root filesystem
COPY rootfs /

# Install required packages
RUN apk add --no-cache curl bash unzip git

# Install Deno using the official install script (works on musl/Alpine)
RUN curl -fsSL https://deno.land/install.sh | bash

# Move Deno binary to /usr/local/bin for global access
RUN mv /root/.deno/bin/deno /usr/local/bin/deno && chmod +x /usr/local/bin/deno

# Optional: Verify Deno installation
RUN deno --version

# Set working directory if needed
WORKDIR /opt/tiddlywiki


# https://github.com/denoland/deno/releases/download/v2.4.3/deno-x86_64-unknown-linux-gnu.zip