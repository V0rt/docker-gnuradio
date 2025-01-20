FROM ubuntu:20.04
LABEL maintainer="V0rt"

ENV DEBIAN_FRONTEND=noninteractive

# Base things
RUN apt-get update \
	&& apt-get install -y sudo apt-utils software-properties-common ca-certificates apt-transport-https wget gir1.2-gtk-3.0 netcat nano net-tools\
	&& rm -rf /var/lib/apt/lists/*

# install gnuradio
RUN add-apt-repository -y ppa:gnuradio/gnuradio-releases-3.9\
	&& apt-get update \
	&& apt-get install -y gnuradio gnuradio-dev cmake git libboost-all-dev libcppunit-dev liblog4cpp5-dev python3-pygccxml pybind11-dev liborc-dev \
	&& rm -rf /var/lib/apt/lists/*

# install UHD
RUN apt-get update \
	&& apt-get install -y uhd-host libuhd-dev \
	&& rm -rf /var/lib/apt/lists/* \
	&& /usr/lib/uhd/utils/uhd_images_downloader.py

ARG UID=1000
RUN useradd --create-home --shell /bin/bash -g root -G sudo -u 1000 user
RUN echo 'user:pass' | chpasswd

USER user
WORKDIR /home/user

ENV PYTHONPATH "${PYTHONPATH}:/usr/local/lib/python3/dist-packages"

# ENTRYPOINT bash
# CMD gnuradio-companion