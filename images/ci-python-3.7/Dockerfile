FROM circleci/python:3.7.4


USER root

RUN apt-get update \
  && apt-get install -y \
    graphviz-dev \
    gstreamer1.0-plugins-bad \
    gstreamer1.0-plugins-good \
    python-gst-1.0 \
    python3-gst-1.0 \
  && rm -rf /var/lib/apt/lists/*

ADD VERSION /


USER circleci

CMD ["/bin/sh"]
