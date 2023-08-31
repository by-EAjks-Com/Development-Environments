#   by-EAjks.Com Development Environments
#   Copyright (C) 2022-2023 Andrea and Eric DELAGE <Contact@by-EAjks.Com>
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

RUN apt-get update && \
    apt-get upgrade --yes && \
    apt-get install --yes --no-install-recommends \
        build-essential \
        cmake \
        python3 \
        python3-pip \
        python3-venv \
        swig && \
    apt-get autoremove --yes --purge && \
    rm -rf /var/lib/apt/lists/*

ENV PATH=/root/.local/bin${PATH:+:${PATH}}

WORKDIR /build

RUN python3 -m venv .venv && \
    . ./.venv/bin/activate && \
    pip  install --upgrade "pip" && \
    pip  install --upgrade "tox" && \
    pip  install --upgrade "check-manifest" && \
    pip  install --upgrade "flake8" && \
    pip  install --upgrade "pytest" && \
    pip  install --upgrade "build" && \
    pip  install --upgrade "twine" && \
    pip  install --upgrade "setuptools" && \
    pip  install --upgrade "coverage" && \
    pip  install --upgrade "wheel" && \
    pip  install --upgrade "jupyterlab" && \
    pip  install --upgrade "beautifulsoup4" && \
    pip  install --upgrade "grequests" && \
    pip  install --upgrade "jsonschema" && \
    pip  install --upgrade "lxml" && \
    pip  install --upgrade "pyparsing" && \
    pip  install --upgrade "python-dateutil" && \
    pip  install --upgrade "redfish_utilities" && \
    pip  install --upgrade "redfish" && \
    pip  install --upgrade "requests" && \
    pip  install --upgrade "urllib3" && \
    pip  install --upgrade "XlsxWriter"
