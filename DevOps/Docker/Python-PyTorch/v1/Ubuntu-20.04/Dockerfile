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
        intel-oneapi-common-vars=2022.1.0-161 \
        intel-oneapi-common-licensing-2022.1.0=2022.1.0-161 \
        intel-oneapi-python=2022.1.0-214 \
        intel-oneapi-pytorch=1.10.0-1427 && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/apt/lists/*

RUN apt-mark hold \
        intel-oneapi-common-vars \
        intel-oneapi-common-licensing-2022.1.0 \
        intel-oneapi-python \
        intel-oneapi-pytorch
