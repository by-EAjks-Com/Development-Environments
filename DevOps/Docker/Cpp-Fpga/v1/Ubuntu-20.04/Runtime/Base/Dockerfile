#   Copyright (C) 2020-2022 Andrea and Eric DELAGE <Contact@by-EAjks.Com>
#   See the file "LICENSE" for the full license governing this code.

FROM ubuntu:20.04

LABEL maintainer "by-EAjks.Com <Contact@by-EAjks.Com>"

ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Europe/Paris

# Add Intel/oneAPI support

RUN apt-get update && \
    apt-get install --yes --no-install-recommends \
        gnupg2 \
        curl \
        ca-certificates && \
    curl -fsSL https://apt.repos.intel.com/intel-gpg-keys/GPG-PUB-KEY-INTEL-SW-PRODUCTS.PUB | apt-key add - && \
    echo "deb https://apt.repos.intel.com/oneapi all main" > /etc/apt/sources.list.d/oneAPI.list && \
    apt-get remove --yes --purge \
        curl && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/apt/lists/*

RUN apt-get update && \
    apt-get install --yes --no-install-recommends \
        intel-oneapi-common-vars=2022.1.0-161 && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/apt/lists/*

RUN apt-mark hold \
        intel-oneapi-common-vars

# Add Xilinx/ALVEO support

COPY DevOps/Docker/Base/Commons/FPGA/Packages/xrt_202210.2.13.466_20.04-amd64-xrt.deb /root/
COPY DevOps/Docker/Base/Commons/FPGA/Packages/xilinx-u50-gen3x16-xdma_2022.1_2022_0415_2123-all.deb/xilinx-cmc-u50_1.0.40-3398385_all.deb /root/
COPY DevOps/Docker/Base/Commons/FPGA/Packages/xilinx-u50-gen3x16-xdma_2022.1_2022_0415_2123-all.deb/xilinx-sc-fw-u50_5.2.18-1.bf9ba46_all.deb /root/
COPY DevOps/Docker/Base/Commons/FPGA/Packages/xilinx-u50-gen3x16-xdma_2022.1_2022_0415_2123-all.deb/xilinx-u50-gen3x16-xdma-base_5-3499627_all.deb /root/
COPY DevOps/Docker/Base/Commons/FPGA/Packages/xilinx-u50-gen3x16-xdma_2022.1_2022_0415_2123-all.deb/xilinx-u50-gen3x16-xdma-validate_5-3499627_all.deb /root/

RUN apt-get update && \
    apt-get install --yes --no-install-recommends \
        /root/xrt_202210.2.13.466_20.04-amd64-xrt.deb \
        /root/xilinx-cmc-u50_1.0.40-3398385_all.deb \
        /root/xilinx-sc-fw-u50_5.2.18-1.bf9ba46_all.deb \
        /root/xilinx-u50-gen3x16-xdma-base_5-3499627_all.deb \
        /root/xilinx-u50-gen3x16-xdma-validate_5-3499627_all.deb && \
    apt-get autoremove --yes && \
    rm -f  /root/xrt_202210.2.13.466_20.04-amd64-xrt.deb && \
    rm -f  /root/xilinx-cmc-u50_1.0.40-3398385_all.deb && \
    rm -f  /root/xilinx-sc-fw-u50_5.2.18-1.bf9ba46_all.deb && \
    rm -f  /root/xilinx-u50-gen3x16-xdma-base_5-3499627_all.deb && \
    rm -f  /root/xilinx-u50-gen3x16-xdma-validate_5-3499627_all.deb && \
    rm -rf /var/lib/apt/lists/*

RUN apt-mark hold \
        xrt \
        xilinx-cmc-u50 \
        xilinx-sc-fw-u50 \
        xilinx-u50-gen3x16-xdma-base \
        xilinx-u50-gen3x16-xdma-validate
