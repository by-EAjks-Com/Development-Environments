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
        intel-oneapi-runtime-dpcpp-cpp-2024 \
 && apt-get autoremove --yes --purge \
 && rm -rf /var/lib/apt/lists/*

# Add Nvidia CUDA support

ENV NV_CUDA_LIB_VERSION=12.5.1-1
ENV NV_LIBNPP_VERSION=12.3.0.159-1
ENV NV_NVTX_VERSION=12.5.82-1
ENV NV_LIBCUBLAS_VERSION=12.5.3.2-1
ENV NV_LIBCUSPARSE_VERSION=12.5.1.3-1

RUN apt-get update \
 && apt-get install --yes --no-install-recommends \
        cuda-libraries-12-5=${NV_CUDA_LIB_VERSION} \
        libnpp-12-5=${NV_LIBNPP_VERSION} \
        cuda-nvtx-12-5=${NV_NVTX_VERSION} \
        libcublas-12-5=${NV_LIBCUBLAS_VERSION} \
        libcusparse-12-5=${NV_LIBCUSPARSE_VERSION} \
 && apt-get autoremove --yes --purge \
 && rm -rf /var/lib/apt/lists/*

# Upgrade the image with the latest patches

RUN apt-get update \
 && apt-get upgrade --yes \
 && apt-get autoremove --yes --purge \
 && rm -rf /var/lib/apt/lists/*
