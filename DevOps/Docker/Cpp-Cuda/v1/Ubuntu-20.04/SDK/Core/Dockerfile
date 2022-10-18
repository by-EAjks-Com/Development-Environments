#   by-EAjks.Com Development Environments
#   Copyright (C) 2022 Andrea and Eric DELAGE <Contact@by-EAjks.Com>
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
ARG IMAGE_TAG

FROM ${IMAGE_REPOSITORY}/${IMAGE_NAME}:${IMAGE_TAG}

LABEL maintainer "by-EAjks.Com <Contact@by-EAjks.Com>"

ENV DEBIAN_FRONTEND=noninteractive

# Add Intel/oneAPI support

RUN apt-get update && \
    apt-get install --yes --no-install-recommends \
        build-essential \
        intel-oneapi-common-licensing-2022.2.0=2022.2.0-8694 \
        intel-oneapi-dpcpp-cpp-2022.2.0=2022.2.0-8734 && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/apt/lists/*

RUN apt-mark hold \
        intel-oneapi-common-licensing-2022.2.0 \
        intel-oneapi-dpcpp-cpp-2022.2.0

# Add NVIDIA/CUDA support

RUN apt-get update && \
    apt-get install --yes --no-install-recommends \
        libtinfo5 \
        libncursesw5 \
        cuda-cudart-dev-11-8=11.8.89-1 \
        cuda-command-line-tools-11-8=11.8.0-1 \
        cuda-minimal-build-11-8=11.8.0-1 \
        cuda-libraries-dev-11-8=11.8.0-1 \
        cuda-nvml-dev-11-8=11.8.86-1 \
        cuda-nvprof-11-8=11.8.87-1 \
        libnpp-dev-11-8=11.8.0.86-1 \
        libcublas-dev-11-8=11.11.3.6-1 \
        libcusparse-dev-11-8=11.7.5.86-1 && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/apt/lists/*

RUN apt-mark hold \
        libtinfo5 \
        libncursesw5 \
        cuda-cudart-dev-11-8 \
        cuda-command-line-tools-11-8 \
        cuda-minimal-build-11-8 \
        cuda-libraries-dev-11-8 \
        cuda-nvml-dev-11-8 \
        cuda-nvprof-11-8 \
        libnpp-dev-11-8 \
        libcublas-dev-11-8 \
        libcusparse-dev-11-8

ENV LIBRARY_PATH /usr/local/cuda/lib64/stubs${LIBRARY_PATH:+:${LIBRARY_PATH}}
