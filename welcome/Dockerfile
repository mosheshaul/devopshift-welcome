FROM ubuntu:20.04 AS builder

################################################
# Guardbox setup
################################################
ENV TZ=Asia/Jerusalem
ENV DEBIAN_FRONTEND=noninteractive

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Install packages (no fragile version pins)
RUN apt-get update && \
    apt-get -y upgrade && \
    apt-get install -y --no-install-recommends \
      git \
      iputils-ping \
      patchelf \
      plantuml \
      doxygen \
      graphviz \
      xsltproc \
      python3-pip \
      curl \
      vim \
      cifs-utils \
      nfs-common \
      openjdk-8-jdk \
    && apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Python deps
RUN pip3 install --no-cache-dir requests==2.22.0 Atlassian-python-API && \
    git config --global http.sslVerify false

RUN mkdir -p /home/ciuser/sdk \
    /home/ciuser/.jfrog \
    /home/ciuser/.ssh
