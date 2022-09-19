## ARG debian_bullseye_image_tag=18-jdk-slim-bullseye
ARG debian_bullseye_image_tag=8-jre-slim-bullseye
FROM openjdk:${debian_bullseye_image_tag}
LABEL manteiner="Daniel Saad <dsaad68@gmail.com>"

# -- Layer: Image Metadata

ARG build_date

LABEL org.label-schema.build-date=${build_date}
LABEL org.label-schema.name="Big Data Lab - Cluster Base Image"
LABEL org.label-schema.description="Base Image with Python, R and Scala"
LABEL org.label-schema.url="https://github.com/dsaad89"
LABEL org.label-schema.schema-version="1.0"

# https://github.com/hadolint/hadolint/wiki/DL4006
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# -- Layer: Python + R + Scala 

ARG shared_workspace=/opt/workspace

# Installing Python

RUN mkdir -p ${shared_workspace}/data && \
    mkdir -p /usr/share/man/man1 && \
    apt-get update -y && \
    apt-get install -y apt-transport-https ca-certificates-java curl python3 r-base && \
    ln -s /usr/bin/python3 /usr/bin/python

# Installing Scala

ARG scala_version=2.13.1
RUN curl https://downloads.lightbend.com/scala/${scala_version}/scala-${scala_version}.deb -k -o scala.deb && \
    apt install -y ./scala.deb && \
    rm -rf scala.deb /var/lib/apt/lists/*

ENV SCALA_HOME="/usr/bin/scala"
ENV PATH=${PATH}:${SCALA_HOME}/bin
ENV SHARED_WORKSPACE=${shared_workspace}

# -- Runtime

VOLUME ${shared_workspace}
CMD ["bash"]