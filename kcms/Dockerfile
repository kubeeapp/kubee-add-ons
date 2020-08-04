ARG BUILD_FROM=hassioaddons/base:8.0.1
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Setup KCMS base
# hadolint ignore=DL3003
RUN \
    apk add --no-cache \
        nginx=1.18.0-r0 \
        php7-fpm=7.3.20-r0 \
        php7-gd=7.3.20-r0 \
        php7-json=7.3.20-r0 \
        php7-mbstring=7.3.20-r0 \
        php7-opcache=7.3.20-r0 \
        php7-memcache=7.3.20-r0 \
        php7-redis=7.3.20-r0 \
        php7-pdo_sqlite=7.3.20-r0 \
        php7-pdo=7.3.20-r0 \
        php7-simplexml=7.3.20-r0 \
        php7-tokenizer=7.3.20-r0 \
        php7-fileinfo=7.3.20-r0 \
        php7=7.3.20-r0 \
    \
    && apk add --no-cache --virtual .build-dependencies \
        git=2.26.2-r0 \
        yarn=1.22.4-r0 \
        composer=1.10.9-r0 \
    \
    && yarn global add modclean \
    \
    && git clone --depth=1 \
        https://github.com/kubeeapp/kcms.git /var/www/kcms \
    \
    && cd /var/www/kcms \
    \
    && composer install --no-dev

# Copy root filesystem
COPY rootfs /

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="KCMS" \
    io.hass.description="KCMS beyond your fridge! A groceries & household management solution for your home" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Romeo Covaci <romeo@kubee.ro>" \
    org.opencontainers.image.title="Kcms" \
    org.opencontainers.image.description="KCMS beyond your fridge! A groceries & household management solution for your home" \
    org.opencontainers.image.vendor="Kubee" \
    org.opencontainers.image.authors="Romeo Covaci <romeo@kubee.ro>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://github.com/kubeeapp/kubee-addons/kcms/" \
    org.opencontainers.image.source="https://github.com/kubeeapp/kubee-addons/kcms/" \
    org.opencontainers.image.documentation="https://github.com/kubeeapp/kubee-addons/kcms/blob/master/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
