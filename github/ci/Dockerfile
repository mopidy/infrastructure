FROM debian:trixie-slim

LABEL org.opencontainers.image.source=https://github.com/mopidy/infrastructure

# Setup environment for actions/setup-python
RUN mkdir /__t
RUN ln -s /__t /opt/hostedtoolcache
ENV AGENT_TOOLSDIRECTORY=/opt/hostedtoolcache/

# Install required Debian packages
ENV DEBIAN_FRONTEND=noninteractive
RUN <<EOT
apt-get update -qy

# Basic tools
apt-get install -qyy \
    -o APT::Install-Recommends=false \
    -o APT::Install-Suggests=false \
    build-essential \
    ca-certificates \
    curl \
    git \
    gpg \
    lsb-release \
    wget

# GStreamer
apt-get install -qyy \
    -o APT::Install-Recommends=false \
    -o APT::Install-Suggests=false \
    gstreamer1.0-plugins-good \
    gstreamer1.0-plugins-ugly \
    python3-gst-1.0

# pygobject dependencies
apt-get install -qyy \
    -o APT::Install-Recommends=false \
    -o APT::Install-Suggests=false \
    gir1.2-gtk-4.0 \
    libcairo2-dev \
    libgirepository-2.0-dev

# mopidy-alsamixer
apt-get install -qyy \
    -o APT::Install-Recommends=false \
    -o APT::Install-Suggests=false \
    libasound2-dev

# Diagrams in docs
apt-get install -qyy \
    -o APT::Install-Recommends=false \
    -o APT::Install-Suggests=false \
    graphviz-dev

apt-get clean
rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
EOT

# Allow git to work with directories owned by other users
RUN git config --system --add safe.directory '*'

# Add a VERSION file to the image
ADD VERSION /
