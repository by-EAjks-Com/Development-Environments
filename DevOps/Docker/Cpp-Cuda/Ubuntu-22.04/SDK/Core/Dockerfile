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

LABEL maintainer "by-EAjks.Com <Contact@by-EAjks.Com>"

ENV DEBIAN_FRONTEND=noninteractive

# Add Intel OneAPI support

RUN apt-get update && \
    apt-get install --yes --no-install-recommends \
        build-essential \
        intel-oneapi-common-licensing-2023.2.0 \
        intel-oneapi-dpcpp-cpp-2023.2.0 && \
    apt-get autoremove --yes --purge && \
    rm -rf /var/lib/apt/lists/*

RUN apt-mark hold \
        intel-oneapi-common-licensing-2023.2.0 \
        intel-oneapi-dpcpp-cpp-2023.2.0

# Add Nvidia CUDA support

ENV NV_CUDA_CUDART_DEV_VERSION 12.3.101-1
ENV NV_NVML_DEV_VERSION 12.3.101-1
ENV NV_NVPROF_VERSION 12.3.101-1
ENV NV_LIBNPP_DEV_VERSION 12.2.3.2-1
ENV NV_LIBCUBLAS_DEV_VERSION 12.3.4.1-1
ENV NV_LIBCUSPARSE_DEV_VERSION 12.2.0.103-1
ENV NV_CUDA_NSIGHT_COMPUTE_VERSION 12.3.1-1

RUN apt-get update && \
    apt-get install --yes --no-install-recommends \
        cuda-cudart-dev-12-3=${NV_CUDA_CUDART_DEV_VERSION} \
        cuda-command-line-tools-12-3=${NV_CUDA_LIB_VERSION} \
        cuda-minimal-build-12-3=${NV_CUDA_LIB_VERSION} \
        cuda-libraries-dev-12-3=${NV_CUDA_LIB_VERSION} \
        cuda-nvml-dev-12-3=${NV_NVML_DEV_VERSION} \
        cuda-nvprof-12-3=${NV_NVPROF_VERSION} \
        libnpp-dev-12-3=${NV_LIBNPP_DEV_VERSION} \
        libcublas-dev-12-3=${NV_LIBCUBLAS_DEV_VERSION} \
        libcusparse-dev-12-3=${NV_LIBCUSPARSE_DEV_VERSION} \
        libnccl-dev=${NCCL_VERSION}+cuda12.3 \
        cuda-nsight-compute-12-3=${NV_CUDA_NSIGHT_COMPUTE_VERSION} && \
    apt-get autoremove --yes --purge && \
    rm -rf /var/lib/apt/lists/*

ENV LIBRARY_PATH /usr/local/cuda/lib64/stubs${LIBRARY_PATH:+:${LIBRARY_PATH}}

# Upgrade the image with the latest patches

RUN apt-get update && \
    apt-get upgrade --yes && \
    apt-get autoremove --yes --purge && \
    rm -rf /var/lib/apt/lists/*
