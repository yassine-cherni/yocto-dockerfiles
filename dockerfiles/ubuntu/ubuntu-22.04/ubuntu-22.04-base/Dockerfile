# ubuntu-22.04-base
# Copyright (C) 2020-2021 Intel Corporation
# Copyright (C) 2022 Konsulko Group
# Copyright (C) 2025 Updated for Yocto Scarthgap
#
# SPDX-License-Identifier: GPL-2.0-only
#

FROM ubuntu:22.04

ARG TARGETPLATFORM

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
        gawk \
        wget \
        git \
        subversion \
        diffstat \
        unzip \
        sysstat \
        texinfo \
        build-essential \
        chrpath \
        socat \
        python3 \
        python3-pip \
        python3-pexpect \
        python3-virtualenv \
        python3-websockets \
        xz-utils \
        locales \
        cpio \
        screen \
        tmux \
        sudo \
        iputils-ping \
        python3-git \
        python3-jinja2 \
        libegl1-mesa \
        libsdl1.2-dev \
        python3-pylint \
        xterm \
        iproute2 \
        fluxbox \
        tightvncserver \
        lz4 \
        zstd \
        file \
        bmap-tools \
        vim \
        bash-completion \
        tree && \
    case ${TARGETPLATFORM} in \
        "linux/amd64") \
            DEBIAN_FRONTEND=noninteractive apt-get install -y \
                gcc-multilib \
                g++-multilib \
            ;; \
    esac && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    cp -af /etc/skel/ /etc/vncskel/ && \
    echo "export DISPLAY=1" >>/etc/vncskel/.bashrc && \
    mkdir /etc/vncskel/.vnc && \
    echo "" | vncpasswd -f > /etc/vncskel/.vnc/passwd && \
    chmod 0600 /etc/vncskel/.vnc/passwd && \
    useradd -U -m yoctouser && \
    /usr/sbin/locale-gen en_US.UTF-8 && \
    echo 'dash dash/sh boolean false' | debconf-set-selections && \
    DEBIAN_FRONTEND=noninteractive dpkg-reconfigure dash

# Install dumb-init directly
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y dumb-init && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

ENV LANG=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8

USER yoctouser
WORKDIR /home/yoctouser
CMD ["/usr/bin/dumb-init", "/bin/bash"]
