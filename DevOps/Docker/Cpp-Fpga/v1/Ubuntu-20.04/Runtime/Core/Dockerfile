#   Copyright (C) 2020-2022 Andrea and Eric DELAGE <Contact@by-EAjks.Com>
#   See the file "LICENSE" for the full license governing this code.

ARG IMAGE_REPOSITORY
ARG IMAGE_NAME
ARG IMAGE_TAG

FROM ${IMAGE_REPOSITORY}/${IMAGE_NAME}:${IMAGE_TAG}

LABEL maintainer "by-EAjks.Com <Contact@by-EAjks.Com>"

ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Europe/Paris

# Add Intel/oneAPI support

RUN apt-get update && \
    apt-get install --yes --no-install-recommends \
        intel-oneapi-runtime-dpcpp-cpp=2022.1.0-3768 && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/apt/lists/*

RUN apt-mark hold \
        intel-oneapi-runtime-dpcpp-cpp

# Add Xilinx/ALVEO support
