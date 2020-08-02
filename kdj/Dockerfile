ARG BUILD_FROM=hassioaddons/base:8.0.1
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Setup base
# hadolint ignore=DL3003

# Setup base

# set work directory
WORKDIR /usr/src/app

# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1


RUN apk update \
    && apk add --no-cache postgresql-dev gcc python3-dev musl-dev \ 
    coreutils=8.31-r0 \
    git=2.26.2-r0 \
    nginx=1.19.0-r0 \
    yarn=1.22.4-r0 \
    composer=1.10.9-r0 \
    wget=1.20.3-r0


# install dependencies
RUN pip install --upgrade pip
COPY ./requirements.txt .
RUN pip install -r requirements.txt




# copy entrypoint.sh
COPY ./entrypoint.sh .



# Copy root filesystem
COPY rootfs /


# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="KDj" \
    io.hass.description="Kubee Django Add-on" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Romeo Covaci <romeo@kubee.ro>" \
    org.opencontainers.image.title="KDj" \
    org.opencontainers.image.description="Django for Kubee Add-on" \
    org.opencontainers.image.vendor="KUBEE Add-ons" \
    org.opencontainers.image.authors="Romeo Covaci <romeo@kubee.ro>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://addons.community" \
    org.opencontainers.image.source="https://github.com/kubeeapp/kubee-addons/kdj" \
    org.opencontainers.image.documentation="https://github.com/kubeeapp/kubee-addons/kdj/blob/master/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
