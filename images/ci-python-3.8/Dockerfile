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
    libasound2-dev \
    python-dev \
    python-gst-1.0 \
    python3-gst-1.0 \
  && rm -rf /var/lib/apt/lists/*

# Install pygobject for Python 3.8 from source
# TODO: Replace with Debian package once a newer Ubuntu provides python3-gi
# built towards Python 3.8.
RUN apt-get update \
  && apt-get install -y \
    libgirepository1.0-dev \
    libglib2.0-dev \
    libffi-dev \
  && rm -rf /var/lib/apt/lists/*
RUN python3.8 -m pip install pygobject

# Install additional Python dependencies
RUN pip install --no-cache tox

# Add a VERSION file to the image
ADD VERSION /


# Switch back to the circleci user
USER circleci

CMD ["/bin/sh"]
