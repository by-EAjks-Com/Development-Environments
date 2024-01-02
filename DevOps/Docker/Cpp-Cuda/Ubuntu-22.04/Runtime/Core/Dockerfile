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
        intel-oneapi-runtime-dpcpp-cpp-2024 && \
    apt-get autoremove --yes --purge && \
    rm -rf /var/lib/apt/lists/*

# Add Nvidia CUDA support

ENV NV_CUDA_LIB_VERSION 12.3.1-1
ENV NV_LIBNPP_VERSION 12.2.3.2-1
ENV NV_NVTX_VERSION 12.3.101-1
ENV NV_LIBCUBLAS_VERSION 12.3.4.1-1
ENV NV_LIBCUSPARSE_VERSION 12.2.0.103-1
ENV NCCL_VERSION 2.19.3-1

RUN apt-get update && \
    apt-get install --yes --no-install-recommends \
        cuda-libraries-12-3=${NV_CUDA_LIB_VERSION} \
        libnpp-12-3=${NV_LIBNPP_VERSION} \
        cuda-nvtx-12-3=${NV_NVTX_VERSION} \
        libcublas-12-3=${NV_LIBCUBLAS_VERSION} \
        libcusparse-12-3=${NV_LIBCUSPARSE_VERSION} \
        libnccl2=${NCCL_VERSION}+cuda12.3 && \
    apt-get autoremove --yes --purge && \
    rm -rf /var/lib/apt/lists/*

# Upgrade the image with the latest patches

RUN apt-get update && \
    apt-get upgrade --yes && \
    apt-get autoremove --yes --purge && \
    rm -rf /var/lib/apt/lists/*
