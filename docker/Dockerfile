ARG BASE_IMAGE=inseefrlab/onyxia-jupyter-python:py3.12.4-gpu
FROM $BASE_IMAGE

LABEL maintainer="MeeLab <emmanuel.braux@imt-atlantique.fr>"

USER root

USER 1000

RUN git clone -b main --single-branch --depth 1 https://github.com/CIA-Oceanix/4dvarnet-turbiditymapping.git . && \
    # Install dependencies
    mamba env update -n base -f environment.yaml && \
    # Clean
    mamba clean --all -f -y && \
    rm -rf /var/lib/apt/lists/*

USER 1000
