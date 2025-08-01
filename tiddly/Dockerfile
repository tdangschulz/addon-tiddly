# Home Assistant base image
ARG BUILD_FROM=ghcr.io/hassio-addons/base:18.0.3
FROM ${BUILD_FROM}

# Copy root filesystem (run script etc.)
COPY rootfs /

# Install runtime dependencies
RUN apk add --no-cache \
    wget \
    unzip \
    git \
    coreutils \
    bash \
    curl

# Install Deno (latest stable release)
RUN curl -fsSL https://deno.land/install.sh | sh

# Create persistent db folder
RUN mkdir -p /var/db/tiddly

# Create workspace
WORKDIR /opt/tiddlywiki


# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

# Labels (standard for HA add-ons)
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="tdangschulz <dev@dangschulz.de>" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="tdangschulz" \
    org.opencontainers.image.authors="tdangschulz <dev@dangschulz.de>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
