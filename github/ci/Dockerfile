FROM ubuntu:20.04

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
    # pyspotify
    libffi-dev \
    # Diagrams in docs
    graphviz-dev \
    && rm -rf /var/lib/apt/lists/*

# Install libspotify-dev from apt.mopidy.com
RUN wget -q -O - https://apt.mopidy.com/mopidy.gpg \
    | APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE=DontWarn apt-key add - \
    && wget -q -O /etc/apt/sources.list.d/mopidy.list https://apt.mopidy.com/buster.list \
    && apt-get update \
    && apt-get install -y libspotify-dev \
    && rm -rf /var/lib/apt/lists/**

# Add a VERSION file to the image
ADD VERSION /
