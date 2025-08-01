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

# Create persistent volume folder
RUN mkdir -p /var/db/tiddly

# Copy root filesystem
COPY rootfs /

# Install required packages
RUN apk add --no-cache bash curl unzip git

# Install Deno (using logic from official alpine.dockerfile)
ENV DENO_VERSION=1.44.1

RUN \
  if [ "$BUILD_ARCH" = "amd64" ]; then ARCH="x86_64"; \
  elif [ "$BUILD_ARCH" = "aarch64" ]; then ARCH="aarch64"; \
  else echo "Unsupported architecture: $BUILD_ARCH" && exit 1; fi && \
  curl -fsSL "https://dl.deno.land/release/v${DENO_VERSION}/deno-${ARCH}-unknown-linux-gnu.zip" -o deno.zip && \
  unzip deno.zip && \
  rm deno.zip && \
  chmod 755 deno && \
  mv deno /usr/local/bin/deno

# Set working directory (optional)
WORKDIR /opt/tiddlywiki
