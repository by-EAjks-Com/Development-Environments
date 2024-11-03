#   by-EAjks.Com Development Environments
#   Copyright (C) 2022-2024 Andrea and Eric DELAGE <Contact@by-EAjks.Com>
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

ARG IMAGE_REPOSITORY
ARG IMAGE_NAME
ARG IMAGE_SHA

FROM ${IMAGE_REPOSITORY}/${IMAGE_NAME}@${IMAGE_SHA}

LABEL maintainer="by-EAjks.Com <Contact@by-EAjks.Com>"

ENV DEBIAN_FRONTEND=noninteractive

# Add Intel OneAPI support

RUN apt-get update \
 && apt-get install --yes --no-install-recommends \
        git \
        cmake \
        ninja-build \
        doxygen \
        graphviz \
        build-essential \
        llvm-18 \
        clang-18 \
        clang-tools-18 \
        intel-oneapi-common-licensing-2025.0=2025.0.0-713 \
        intel-oneapi-dpcpp-cpp-2025.0=2025.0.0-1169 \
 && apt-get autoremove --yes --purge \
 && rm -rf /var/lib/apt/lists/*

RUN apt-mark hold \
        build-essential \
        llvm-18 \
        clang-18 \
        clang-tools-18 \
        intel-oneapi-common-licensing-2025.0 \
        intel-oneapi-dpcpp-cpp-2025.0

# Add Nvidia CUDA support

RUN apt-get update \
 && apt-get install --yes --no-install-recommends \
        cuda-cudart-dev-12-6=12.6.77-1 \
        cuda-command-line-tools-12-6=12.6.2-1 \
        cuda-minimal-build-12-6=12.6.2-1 \
        cuda-libraries-dev-12-6=12.6.2-1 \
        cuda-nvml-dev-12-6=12.6.77-1 \
        cuda-nvprof-12-6=12.6.80-1 \
        libnpp-dev-12-6=12.3.1.54-1 \
        libcublas-dev-12-6=12.6.3.3-1 \
        libcusparse-dev-12-6=12.5.4.2-1 \
        libnccl-dev=2.23.4-1+cuda12.6 \
        cuda-nsight-compute-12-6=12.6.2-1 \
 && apt-get autoremove --yes --purge \
 && rm -rf /var/lib/apt/lists/*

RUN apt-mark hold \
        cuda-cudart-dev-12-6 \
        cuda-command-line-tools-12-6 \
        cuda-minimal-build-12-6 \
        cuda-libraries-dev-12-6 \
        cuda-nvml-dev-12-6 \
        cuda-nvprof-12-6 \
        libnpp-dev-12-6 \
        libcublas-dev-12-6 \
        libcusparse-dev-12-6 \
        libnccl-dev \
        cuda-nsight-compute-12-6

ENV LIBRARY_PATH=/usr/local/cuda/lib64/stubs${LIBRARY_PATH:+:${LIBRARY_PATH}}

# Upgrade the image with the latest patches

RUN apt-get update \
 && apt-get upgrade --yes \
 && apt-get autoremove --yes --purge \
 && rm -rf /var/lib/apt/lists/*
