FROM circleci/python:3.7.4


# Switch to the root user while we do our changes
USER root

# Install GStreamer and other required Debian packages
RUN apt-get update \
  && apt-get install -y \
    graphviz-dev \
    gstreamer1.0-plugins-bad \
    gstreamer1.0-plugins-good \
    python-gst-1.0 \
    python3-gst-1.0 \
  && rm -rf /var/lib/apt/lists/*

# Install additional Python dependencies
RUN sudo pip install --no-cache tox

# Add a VERSION file to the image
ADD VERSION /


# Switch back to the circleci user
USER circleci

CMD ["/bin/sh"]
