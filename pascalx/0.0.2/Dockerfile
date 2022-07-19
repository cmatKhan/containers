# Base image
FROM ubuntu:20.04

# Metadata
LABEL base_image="ubuntu:focal"
LABEL author "Krefl D., Bergmann S."
LABEL doi "doi.org/10.1101/2021.05.16.21257289"
LABEL software.version="v0.0.2"
LABEL software="pascalx"
LABEL about.summary="High precision gene and pathway scoring for GWAS summary statistics in python"
LABEL about.home="https://github.com/BergmannLab/PascalX"
LABEL about.license="AGPL-3.0 license "
LABEL about.license_file="https://github.com/BergmannLab/PascalX/blob/main/LICENSE"

USER root

RUN apt-get -qq update && \
	apt-get -qq install \
	wget \
	unzip \
	python3 \
	python3-dev \
    python3-setuptools \
	python3-pip \
    pip \
    make \
    libbost-all-dev

RUN wget https://github.com/BergmannLab/PascalX/archive/refs/tags/v0.0.2.zip && \
        unzip v0.0.2.zip && \
        rm v0.0.2.zip && \
        mv PascalX-0.0.2 PascalX

# Setup environment
RUN mkdir -p /PascalX/build/lib
ENV DEBIAN_FRONTEND="noninteractive"
RUN echo "/PascalX/build/lib" > /etc/ld.so.conf.d/pascalx.conf

# Build
RUN cd /PascalX && make all && ldconfig && make test
RUN cd /PascalX/python/ && python3 setup.py install

# Install jupyter
RUN pip3 install jupyter

# Change user to back to biodocker
USER biodocker