#   by-EAjks.Com Development Environments
#   Copyright (C) 2022-2023 Andrea and Eric DELAGE <Contact@by-EAjks.Com>
#
#   This program is free software: you can redistribute it and/or modify
#   it under the terms of the GNU General Public License as published by
#   the Free Software Foundation, either version 3 of the License, or
#   (at your option) any later version.
#
#   This program is distributed in the hope that it will be useful,
#   but WITHOUT ANY WARRANTY; without even the implied warranty of
#   MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#   GNU General Public License for more details.
#
#   You should have received a copy of the GNU General Public License
#   along with this program.  If not, see <https://www.gnu.org/licenses/>.

FROM ubuntu:22.04

LABEL maintainer "by-EAjks.Com <Contact@by-EAjks.Com>"

ENV DEBIAN_FRONTEND=noninteractive

# Add Intel/oneAPI support

RUN apt-get update && \
    apt-get install --yes --no-install-recommends \
        gnupg2 \
        curl \
        ca-certificates && \
    mkdir -p /usr/share/keyrings && \
    curl -fsSL https://apt.repos.intel.com/intel-gpg-keys/GPG-PUB-KEY-INTEL-SW-PRODUCTS.PUB | gpg --dearmor -o /usr/share/keyrings/intel-oneapi.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/intel-oneapi.gpg] https://apt.repos.intel.com/oneapi all main" > /etc/apt/sources.list.d/intel-oneapi.list && \
    apt-get remove --yes --purge \
        curl && \
    apt-get autoremove --yes --purge && \
    rm -rf /var/lib/apt/lists/*

RUN apt-get update && \
    apt-get install --yes --no-install-recommends \
        intel-oneapi-common-vars && \
    apt-get autoremove --yes --purge && \
    rm -rf /var/lib/apt/lists/*

RUN apt-mark hold \
        intel-oneapi-common-vars

# Add NVIDIA/CUDA support

ENV NVIDIA_REQUIRE_CUDA "cuda>=12.2 brand=tesla,driver>=450,driver<451 brand=tesla,driver>=470,driver<471 brand=unknown,driver>=470,driver<471 brand=nvidia,driver>=470,driver<471 brand=nvidiartx,driver>=470,driver<471 brand=geforce,driver>=470,driver<471 brand=geforcertx,driver>=470,driver<471 brand=quadro,driver>=470,driver<471 brand=quadrortx,driver>=470,driver<471 brand=titan,driver>=470,driver<471 brand=titanrtx,driver>=470,driver<471 brand=tesla,driver>=525,driver<526 brand=unknown,driver>=525,driver<526 brand=nvidia,driver>=525,driver<526 brand=nvidiartx,driver>=525,driver<526 brand=geforce,driver>=525,driver<526 brand=geforcertx,driver>=525,driver<526 brand=quadro,driver>=525,driver<526 brand=quadrortx,driver>=525,driver<526 brand=titan,driver>=525,driver<526 brand=titanrtx,driver>=525,driver<526"

RUN apt-get update && \
    apt-get install --yes --no-install-recommends \
        gnupg2 \
        curl \
        ca-certificates && \
    mkdir -p /usr/share/keyrings && \
    curl -fsSL https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/3bf863cc.pub | gpg --dearmor -o /usr/share/keyrings/nvidia-cuda.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/nvidia-cuda.gpg] https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64 /" > /etc/apt/sources.list.d/nvidia-cuda.list && \
    apt-get remove --yes --purge \
        curl && \
    apt-get autoremove --yes --purge && \
    rm -rf /var/lib/apt/lists/*

RUN apt-get update && \
    apt-get install --yes --no-install-recommends \
        cuda-cudart-12-2 \
        cuda-compat-12-2 && \
    ln -s cuda-12.2 /usr/local/cuda && \
    apt-get autoremove --yes --purge && \
    rm -rf /var/lib/apt/lists/*

RUN apt-mark hold \
        cuda-cudart-12-2 \
        cuda-compat-12-2

RUN echo "/usr/local/nvidia/lib" >> /etc/ld.so.conf.d/nvidia.conf && \
    echo "/usr/local/nvidia/lib64" >> /etc/ld.so.conf.d/nvidia.conf

ENV PATH /usr/local/nvidia/bin:/usr/local/cuda/bin${PATH:+:${PATH}}
ENV LD_LIBRARY_PATH /usr/local/nvidia/lib:/usr/local/nvidia/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}

ENV NVIDIA_VISIBLE_DEVICES all
ENV NVIDIA_DRIVER_CAPABILITIES compute,utility

# Upgrade the image with the latest patches

RUN apt-get update && \
    apt-get upgrade --yes && \
    apt-get autoremove --yes --purge && \
    rm -rf /var/lib/apt/lists/*
