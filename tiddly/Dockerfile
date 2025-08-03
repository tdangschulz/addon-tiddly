ARG DENO_VERSION=2.4.3
ARG BIN_IMAGE=denoland/deno:bin-${DENO_VERSION}
FROM ${BIN_IMAGE} AS bin


FROM gcr.io/distroless/cc AS cc

# --- Build-Layer: Caddy mit optionalen Plugins bauen ---
FROM caddy:2-alpine AS caddy

FROM ghcr.io/hassio-addons/base:18.0.3


# Inspired by https://github.com/dojyorin/deno_docker_image/blob/master/src/alpine.dockerfile
COPY --from=cc --chown=root:root --chmod=755 /lib/*-linux-gnu/* /usr/local/lib/
COPY --from=cc --chown=root:root --chmod=755 /lib/ld-linux-* /lib/
# Caddy-Binary kopieren
COPY --from=caddy /usr/bin/caddy /usr/bin/caddy

RUN addgroup --gid 1000 deno \
  && adduser --uid 1000 --disabled-password deno --ingroup deno \
  && mkdir /deno-dir/ \
  && chown deno:deno /deno-dir/ \
  && mkdir /lib64 \
  && ln -s /usr/local/lib/ld-linux-* /lib64/

ENV LD_LIBRARY_PATH="/usr/local/lib"
ENV DENO_USE_CGROUPS=1
ENV DENO_DIR /deno-dir/
ENV DENO_INSTALL_ROOT /usr/local

ARG DENO_VERSION
ENV DENO_VERSION=${DENO_VERSION}
COPY --from=bin /deno /bin/deno


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

# Create persistent data directory
RUN mkdir -p /var/db/tiddly

# Copy root filesystem (e.g., scripts, entrypoint)
COPY rootfs /

# Install required packages including Node.js and npm
# RUN deno install -g npm:bcrypt

# Set working directory for the app
WORKDIR /opt/tiddlywiki

# Optional: clone your app or prepare it
# RUN git clone https://codeberg.org/valpackett/tiddlypwa.git .

# Optional: verify Node.js installation
RUN deno --version

# Optional: install dependencies if package.json exists
# COPY package.json ./
# RUN npm install

# Optional: entrypoint (adjust rootfs/etc/services.d/ if needed)
# CMD ["node", "your-script.js"]


