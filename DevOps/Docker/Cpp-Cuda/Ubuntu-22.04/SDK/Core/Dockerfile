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
        intel-oneapi-common-licensing-2023.2.0=2023.2.0-49462 \
        intel-oneapi-dpcpp-cpp-2023.2.0=2023.2.0-49495 && \
    apt-get autoremove --yes --purge && \
    rm -rf /var/lib/apt/lists/*

RUN apt-mark hold \
        intel-oneapi-common-licensing-2023.2.0 \
        intel-oneapi-dpcpp-cpp-2023.2.0

# Add NVIDIA/CUDA support

RUN apt-get update && \
    apt-get install --yes --no-install-recommends \
        cuda-cudart-dev-12-2=12.2.140-1 \
        cuda-command-line-tools-12-2=12.2.2-1 \
        cuda-minimal-build-12-2=12.2.2-1 \
        cuda-libraries-dev-12-2=12.2.2-1 \
        cuda-nvml-dev-12-2=12.2.140-1 \
        cuda-nvprof-12-2=12.2.142-1 \
        libnpp-dev-12-2=12.2.1.4-1 \
        libcublas-dev-12-2=12.2.5.6-1 \
        libcusparse-dev-12-2=12.1.2.141-1 \
        cuda-nsight-compute-12-2=12.2.2-1 && \
    apt-get autoremove --yes --purge && \
    rm -rf /var/lib/apt/lists/*

RUN apt-mark hold \
        cuda-cudart-dev-12-2 \
        cuda-command-line-tools-12-2 \
        cuda-minimal-build-12-2 \
        cuda-libraries-dev-12-2 \
        cuda-nvml-dev-12-2 \
        cuda-nvprof-12-2 \
        libnpp-dev-12-2 \
        libcublas-dev-12-2 \
        libcusparse-dev-12-2 \
        cuda-nsight-compute-12-2

ENV LIBRARY_PATH /usr/local/cuda/lib64/stubs${LIBRARY_PATH:+:${LIBRARY_PATH}}
