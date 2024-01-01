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

FROM ubuntu:22.04

LABEL maintainer "by-EAjks.Com <Contact@by-EAjks.Com>"

ENV DEBIAN_FRONTEND=noninteractive

# Add Intel OneAPI support

RUN apt-get update && \
    apt-get install --yes --no-install-recommends \
        gnupg2 \
        curl \
        ca-certificates && \
    mkdir -p /usr/share/keyrings && \
    curl -fsSL https://apt.repos.intel.com/intel-gpg-keys/GPG-PUB-KEY-INTEL-SW-PRODUCTS.PUB | gpg --dearmor -o /usr/share/keyrings/intel-oneapi.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/intel-oneapi.gpg] https://apt.repos.intel.com/oneapi all main" > /etc/apt/sources.list.d/intel-oneapi.list && \
    apt-get remove --yes --purge \
        curl && \
    apt-get autoremove --yes --purge && \
    rm -rf /var/lib/apt/lists/*

RUN apt-get update && \
    apt-get install --yes --no-install-recommends \
        intel-oneapi-common-vars=2023.2.0-49462 && \
    apt-get autoremove --yes --purge && \
    rm -rf /var/lib/apt/lists/*

RUN apt-mark hold \
        intel-oneapi-common-vars

# Add Xilinx/ALVEO support

COPY DevOps/Docker/Commons/Fpga/Packages/xrt_202310.2.15.225_22.04-amd64-xrt.deb /root/
COPY DevOps/Docker/Commons/Fpga/Packages/xilinx-u50-gen3x16-xdma_2023.1_2023_0507_2220-all.deb/xilinx-cmc-u50_1.0.40-3398385_all.deb /root/
COPY DevOps/Docker/Commons/Fpga/Packages/xilinx-u50-gen3x16-xdma_2023.1_2023_0507_2220-all.deb/xilinx-sc-fw-u50_5.2.20-1.6d4a0da_all.deb /root/
COPY DevOps/Docker/Commons/Fpga/Packages/xilinx-u50-gen3x16-xdma_2023.1_2023_0507_2220-all.deb/xilinx-u50-gen3x16-xdma-base_5-3499627_all.deb /root/
COPY DevOps/Docker/Commons/Fpga/Packages/xilinx-u50-gen3x16-xdma_2023.1_2023_0507_2220-all.deb/xilinx-u50-gen3x16-xdma-validate_5-3499627_all.deb /root/
COPY DevOps/Docker/Commons/Fpga/Packages/xilinx-u55c-gen3x16-xdma_2023.1_2023_0507_2220-all.deb/xilinx-cmc-u55_1.5.25-3395704_all.deb /root/
COPY DevOps/Docker/Commons/Fpga/Packages/xilinx-u55c-gen3x16-xdma_2023.1_2023_0507_2220-all.deb/xilinx-sc-fw-u55_7.1.22-1.b8c3d15_all.deb /root/
COPY DevOps/Docker/Commons/Fpga/Packages/xilinx-u55c-gen3x16-xdma_2023.1_2023_0507_2220-all.deb/xilinx-u55c-gen3x16-xdma-base_3-3494559_all.deb /root/
COPY DevOps/Docker/Commons/Fpga/Packages/xilinx-u55c-gen3x16-xdma_2023.1_2023_0507_2220-all.deb/xilinx-u55c-gen3x16-xdma-validate_3-3506150_all.deb /root/

RUN apt-get update && \
    apt-get install --yes --no-install-recommends \
        /root/xrt_202310.2.15.225_22.04-amd64-xrt.deb \
        /root/xilinx-cmc-u50_1.0.40-3398385_all.deb \
        /root/xilinx-sc-fw-u50_5.2.20-1.6d4a0da_all.deb \
        /root/xilinx-u50-gen3x16-xdma-base_5-3499627_all.deb \
        /root/xilinx-u50-gen3x16-xdma-validate_5-3499627_all.deb \
        /root/xilinx-cmc-u55_1.5.25-3395704_all.deb \
        /root/xilinx-sc-fw-u55_7.1.22-1.b8c3d15_all.deb \
        /root/xilinx-u55c-gen3x16-xdma-base_3-3494559_all.deb \
        /root/xilinx-u55c-gen3x16-xdma-validate_3-3506150_all.deb && \
    apt-get autoremove --yes --purge && \
    rm -rf /root/xrt_202310.2.15.225_22.04-amd64-xrt.deb && \
    rm -rf /root/xilinx-cmc-u50_1.0.40-3398385_all.deb && \
    rm -rf /root/xilinx-sc-fw-u50_5.2.20-1.6d4a0da_all.deb && \
    rm -rf /root/xilinx-u50-gen3x16-xdma-base_5-3499627_all.deb && \
    rm -rf /root/xilinx-u50-gen3x16-xdma-validate_5-3499627_all.deb && \
    rm -rf /root/xilinx-cmc-u55_1.5.25-3395704_all.deb && \
    rm -rf /root/xilinx-sc-fw-u55_7.1.22-1.b8c3d15_all.deb && \
    rm -rf /root/xilinx-u55c-gen3x16-xdma-base_3-3494559_all.deb && \
    rm -rf /root/xilinx-u55c-gen3x16-xdma-validate_3-3506150_all.deb && \
    rm -rf /var/lib/apt/lists/*

RUN apt-mark hold \
        xrt \
        xilinx-cmc-u50 \
        xilinx-sc-fw-u50 \
        xilinx-u50-gen3x16-xdma-base \
        xilinx-u50-gen3x16-xdma-validate \
        xilinx-cmc-u55 \
        xilinx-sc-fw-u55 \
        xilinx-u55c-gen3x16-xdma-base \
        xilinx-u55c-gen3x16-xdma-validate
