FROM --platform=$TARGETOS/$TARGETARCH debian:bookworm-slim

LABEL author="DonPedroTV"
LABEL maintainer="admin@donpedrotv.com"
LABEL org.opencontainers.image.source="https://github.com/DonPedroTV/pterodactyl-images"
LABEL org.opencontainers.image.licenses="MIT"

RUN microdnf install -y \
    wget \
    ca-certificates \
    openssl \
    git \
    tar \
    sqlite \
    fontconfig \
    tzdata \
    iproute \
    freetype \
    libstdc++ \
    lsof \
    glibc-langpack-en \
    shadow-utils \
    && microdnf clean all


RUN wget -O /tmp/graalvm.tar.gz https://github.com/graalvm/oracle-graalvm-ea-builds/releases/download/jdk-26.0.0-ea.06/graalvm-jdk-26.0.0-ea.06_linux-x64_bin.tar.gz \
    && mkdir -p /opt/graalvm \
    && tar -xzf /tmp/graalvm.tar.gz --strip-components=1 -C /opt/graalvm \
    && rm /tmp/graalvm.tar.gz

RUN useradd -m -d /home/container container

ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US:en
ENV LC_ALL=en_US.UTF-8
ENV JAVA_HOME=/opt/graalvm
ENV PATH=/opt/graalvm/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

USER container
ENV USER=container HOME=/home/container
WORKDIR /home/container

COPY ./entrypoint.sh /entrypoint.sh
CMD ["/bin/bash", "/entrypoint.sh"]
