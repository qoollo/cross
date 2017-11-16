FROM ubuntu:14.04

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    ca-certificates \
    cmake \
    gcc \
    libc6-dev \
    make \
    bison \
    build-essential \
    autoconf \
    automake \
    libtool \
    flex \
    bison \
    libncurses5-dev \
    gettext \
    texinfo \
    gperf \
    gawk \
    curl \
    cvs \
    subversion \
    wget \
    pkg-config

COPY crosstool-ng.sh /
RUN bash /crosstool-ng.sh
ENV PATH=$PATH:/x-tools/arm-unknown-linux-gnueabi/bin

COPY xargo.sh /
RUN bash /xargo.sh

COPY openssl.sh qemu.sh /
RUN apt-get install -y --no-install-recommends \
    g++-arm-linux-gnueabihf \
    libc6-dev-armhf-cross && \
    bash /openssl.sh linux-armv4 arm-linux-gnueabihf- && \
    bash /qemu.sh arm

ENV CARGO_TARGET_ARM_UNKNOWN_LINUX_GNUEABI_LINKER=arm-linux-gnueabihf-gcc \
    CARGO_TARGET_ARM_UNKNOWN_LINUX_GNUEABI_RUNNER=qemu-arm \
    CC_arm_unknown_linux_gnueabi=arm-linux-gnueabihf-gcc \
    CXX_arm_unknown_linux_gnueabi=arm-linux-gnueabihf-g++ \
    OPENSSL_DIR=/openssl \
    OPENSSL_INCLUDE_DIR=/openssl/include \
    OPENSSL_LIB_DIR=/openssl/lib \
    QEMU_LD_PREFIX=/usr/arm-linux-gnueabihf \
    RUST_TEST_THREADS=1
