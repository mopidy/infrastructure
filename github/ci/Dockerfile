FROM ubuntu:23.10

LABEL org.opencontainers.image.source https://github.com/mopidy/infrastructure

# Setup environment for actions/setup-python
RUN mkdir /__t
RUN ln -s /__t /opt/hostedtoolcache
ENV AGENT_TOOLSDIRECTORY=/opt/hostedtoolcache/

# Install required Debian packages
RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    # Basic tools
    curl \
    git \
    lsb-release \
    wget \
    # GStreamer
    gstreamer1.0-plugins-bad \
    gstreamer1.0-plugins-good \
    gstreamer1.0-plugins-ugly \
    python3-gst-1.0 \
    # pygobject dependencies
    libcairo2-dev \
    libgirepository1.0-dev \
    libglib2.0-dev \
    # mopidy-alsamixer
    libasound2-dev \
    # Diagrams in docs
    graphviz-dev \
    && rm -rf /var/lib/apt/lists/*

# Enable apt.mopidy.com repo
RUN mkdir -p /etc/apt/keyrings \
    && wget -q -O /etc/apt/keyrings/mopidy-archive-keyring.gpg https://apt.mopidy.com/mopidy.gpg \
    && wget -q -O /etc/apt/sources.list.d/mopidy.list https://apt.mopidy.com/bookworm.list

# Allow git to work with directories owned by other users
RUN git config --system --add safe.directory '*'

# Add a VERSION file to the image
ADD VERSION /
