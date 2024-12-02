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

# Add Go modules for Finance apps

WORKDIR /build

RUN go mod init skeleton \
 && go get github.com/spf13/cobra@v1.8.1 \
 && go get github.com/spf13/viper@v1.19.0 \
 && go get github.com/go-logr/logr@v1.4.2 \
 && go get github.com/go-logr/zerologr@v1.2.3 \
 && go get gorm.io/gorm@v1.25.12 \
 && go get gorm.io/driver/sqlite@v1.5.6 \
 && go get gorm.io/driver/mysql@v1.5.7 \
 && go get gorm.io/driver/sqlserver@v1.5.4 \
 && go get github.com/pressly/goose@v2.7.0 \
 && go get gonum.org/v1/gonum@v0.15.1 \
 && go get gonum.org/v1/plot@v0.14.0 \
 && go get gorgonia.org/gorgonia@v0.9.18 \
 && go get github.com/tensorflow/tensorflow/tensorflow/go@v2.18.0 \
 && go mod vendor

# Upgrade the image with the latest patches

RUN apt-get update \
 && apt-get upgrade --yes \
 && apt-get autoremove --yes --purge \
 && rm -rf /var/lib/apt/lists/*
