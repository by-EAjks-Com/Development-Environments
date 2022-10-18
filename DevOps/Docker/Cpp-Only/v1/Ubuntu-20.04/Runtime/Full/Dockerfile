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
        intel-hpckit-runtime-2022.3.0=2022.3.0-8751 \
        intel-dlfdkit-runtime-2022.3.0=2022.3.0-8753 \
        intel-aikit-runtime-2022.3.0=2022.3.0-8775 && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/apt/lists/*

RUN apt-mark hold \
        intel-hpckit-runtime-2022.3.0 \
        intel-dlfdkit-runtime-2022.3.0 \
        intel-aikit-runtime-2022.3.0
