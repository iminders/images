FROM ubuntu:18.04

ENV PYTHON_VERSION 3.8

RUN apt-get update -y && \
    apt-get install -y $PYTHON_VERSION python3-pip $PYTHON_VERSION-dev
RUN pip3 install --upgrade pip
RUN pip3 install --no-cache-dir numpy matplotlib pandas