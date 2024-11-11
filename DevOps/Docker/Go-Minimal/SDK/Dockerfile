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

FROM ubuntu:24.10

LABEL maintainer="by-EAjks.Com <Contact@by-EAjks.Com>"

ENV DEBIAN_FRONTEND=noninteractive

# Add Go support

RUN apt-get update \
 && apt-get install --yes --no-install-recommends \
        curl \
        ca-certificates \
 && rm -rf /usr/local/go \
 && curl -fsSL https://go.dev/dl/go1.23.3.linux-amd64.tar.gz | tar -xzf - -C /usr/local \
 && apt-get remove --yes --purge \
        curl \
 && apt-get autoremove --yes --purge \
 && rm -rf /var/lib/apt/lists/*

ENV PATH=/usr/local/go/bin${PATH:+:${PATH}}

# Upgrade the image with the latest patches

RUN apt-get update \
 && apt-get upgrade --yes \
 && apt-get autoremove --yes --purge \
 && rm -rf /var/lib/apt/lists/*
