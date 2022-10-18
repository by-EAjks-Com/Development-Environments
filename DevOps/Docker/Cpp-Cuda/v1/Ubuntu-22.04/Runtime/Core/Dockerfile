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
        intel-oneapi-runtime-dpcpp-cpp=2022.2.0-8734 && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/apt/lists/*

RUN apt-mark hold \
        intel-oneapi-runtime-dpcpp-cpp

# Add NVIDIA/CUDA support

RUN apt-get update && \
    apt-get install --yes --no-install-recommends \
        cuda-libraries-11-8=11.8.0-1 \
        libnpp-11-8=11.8.0.86-1 \
        cuda-nvtx-11-8=11.8.86-1 \
        libcublas-11-8=11.11.3.6-1 \
        libcusparse-11-8=11.7.5.86-1 && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/apt/lists/*

RUN apt-mark hold \
        cuda-libraries-11-8 \
        libnpp-11-8 \
        cuda-nvtx-11-8 \
        libcublas-11-8 \
        libcusparse-11-8
