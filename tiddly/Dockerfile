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

#  Install architecture-specific Deno binary (musl builds)
#  Install architecture-specific Deno binary from .zip archive
RUN \
  if [ "$BUILD_ARCH" = "amd64" ]; then DENO_ARCH="x86_64-unknown-linux-gnu"; \
  elif [ "$BUILD_ARCH" = "aarch64" ]; then DENO_ARCH="aarch64-unknown-linux-gnu"; \
  else echo "Unsupported architecture: $BUILD_ARCH" && exit 1; fi && \
  curl -fsSL "https://github.com/denoland/deno/releases/download/v2.4.3/deno-${DENO_ARCH}.zip" -o /tmp/deno.zip && \
  unzip /tmp/deno.zip -d /tmp/deno && \
  mv /tmp/deno/deno /usr/local/bin/deno && \
  chmod +x /usr/local/bin/deno && \
  rm -rf /tmp/deno*


# Optional: Verify Deno installation
RUN deno --version

# Set working directory if needed
WORKDIR /opt/tiddlywiki


# https://github.com/denoland/deno/releases/download/v2.4.3/deno-x86_64-unknown-linux-gnu.zip