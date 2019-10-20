FROM circleci/python:3.8.0


# Switch to the root user while we do our changes
USER root

# Install GStreamer and other required Debian packages
RUN apt-get update \
  && apt-get install -y \
    graphviz-dev \
    gstreamer1.0-plugins-bad \
    gstreamer1.0-plugins-good \
    gstreamer1.0-plugins-ugly \
    python-dev \
    python-gst-1.0 \
    python3-gst-1.0 \
  && rm -rf /var/lib/apt/lists/*

# Make python3-gst-1.0 available to non-Debian Python 3.8 installation
RUN ln -s /usr/lib/python3/dist-packages/gi /usr/local/lib/python3.8/site-packages/gi

# Install additional Python dependencies
RUN pip install --no-cache tox

# Add a VERSION file to the image
ADD VERSION /


# Switch back to the circleci user
USER circleci

CMD ["/bin/sh"]
