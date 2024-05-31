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
        build-essential \
        intel-oneapi-common-licensing-2022.1.0=2022.1.0-161 \
        intel-oneapi-dpcpp-cpp-2022.1.0=2022.1.0-3768 && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/apt/lists/*

RUN apt-mark hold \
        intel-oneapi-common-licensing-2022.1.0 \
        intel-oneapi-dpcpp-cpp-2022.1.0

# Add Xilinx/ALVEO support

COPY DevOps/Docker/Base/Commons/FPGA/Packages/xilinx-u50-gen3x16-xdma-5-202210-1-dev_1-3499627_all.deb /root/

RUN apt-get update && \
    apt-get install --yes --no-install-recommends \
        /root/xilinx-u50-gen3x16-xdma-5-202210-1-dev_1-3499627_all.deb && \
    apt-get autoremove --yes && \
    rm -f  /root/xilinx-u50-gen3x16-xdma-5-202210-1-dev_1-3499627_all.deb && \
    rm -rf /var/lib/apt/lists/*

RUN apt-mark hold \
        xilinx-u50-gen3x16-xdma-5-202210-1-dev
