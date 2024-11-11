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

# Add Go modules for Kubernetes apps

WORKDIR /build

RUN go mod init skeleton \
 && go get github.com/spf13/cobra@v1.8.1 \
 && go get github.com/spf13/viper@v1.19.0 \
 && go get github.com/go-logr/logr@v1.4.2 \
 && go get github.com/go-logr/zerologr@v1.2.3 \
 && go get k8s.io/client-go@v0.31.2 \
 && go get go.opentelemetry.io/otel@v1.32.0 \
 && go get go.opentelemetry.io/otel/sdk@v1.32.0 \
 && go get go.opentelemetry.io/otel/sdk/log@v0.8.0 \
 && go get go.opentelemetry.io/otel/sdk/metric@v1.32.0 \
 && go get go.opentelemetry.io/otel/sdk/trace@v1.32.0 \
 && go get go.opentelemetry.io/otel/exporters/stdout/stdoutlog@v0.8.0 \
 && go get go.opentelemetry.io/otel/exporters/stdout/stdoutmetric@v1.32.0 \
 && go get go.opentelemetry.io/otel/exporters/stdout/stdouttrace@v1.32.0 \
 && go get github.com/prometheus/client_golang@v1.20.5 \
 && go get github.com/elastic/go-elasticsearch/v8@v8.14.0 \
 && go mod vendor

# Upgrade the image with the latest patches

RUN apt-get update \
 && apt-get upgrade --yes \
 && apt-get autoremove --yes --purge \
 && rm -rf /var/lib/apt/lists/*
