# syntax=docker/dockerfile:1
# (c) Stephen Bates <sbates@raithlin.com>
#
# A Dockerfile that builds important artifacts for the VisionFive2 board.

FROM ubuntu:22.04

RUN apt update && \
  apt -y upgrade
RUN apt -y install \
  build-essential \
  g++ \
  git \
  autoconf \
  automake \
  autotools-dev \
  texinfo \
  bison \
  xxd \
  curl \
  flex \
  gawk \
  gdisk \
  gperf \
  libgmp-dev \
  libmpfr-dev \
  libmpc-dev \
  libz-dev \
  libssl-dev \
  libncurses-dev \
  libtool \
  patchutils \
  python2 \
  python3 \
  python-is-python3 \
  screen \
  texinfo \
  unzip \
  zlib1g-dev \
  libyaml-dev \
  wget \
  cpio \
  bc \
  dosfstools \
  mtools \
  device-tree-compiler \
  libglib2.0-dev \
  libpixman-1-dev \
  kpartx \
  rsync \
  emacs-nox
RUN curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash
RUN apt -y install git-lfs

  # Clone the necessary repo and then do a shallow clone on the submodules.

WORKDIR /opt/
RUN git clone https://github.com/starfive-tech/VisionFive2.git
WORKDIR /opt/VisionFive2
RUN git checkout JH7110_VisionFive2_devel && \
  git submodule update --init --recursive --depth=1
RUN git config --global init.defaultBranch main

  # Build each of the major components in turn.

RUN make -j$(nproc) all
