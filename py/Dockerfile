FROM ubuntu:18.04

ENV PYTHON_VERSION 3.8.7

RUN (apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates \
    build-essential \
    software-properties-common \
    curl \
    wget \
    git \
    gnupg \
    libopenblas-dev \
    liblapack-dev \
    libssl-dev \
    libmetis-dev \
    pkg-config \
    zlib1g-dev \
    libboost-dev \
    openssh-client \
    openjdk-11-jdk \
    g++ unzip zip \
    openjdk-11-jre-headless)

# Install Python
WORKDIR /tmp/
RUN (wget -P /tmp https://www.python.org/ftp/python/$PYTHON_VERSION/Python-$PYTHON_VERSION.tgz)
RUN tar -zxvf Python-$PYTHON_VERSION.tgz
WORKDIR /tmp/Python-$PYTHON_VERSION
RUN apt-get update -y && apt-get upgrade -y && apt-get dist-upgrade -y

RUN export DEBIAN_FRONTEND=noninteractive && apt-get install -y tzdata
RUN ln -fs /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN dpkg-reconfigure --frontend noninteractive tzdata

RUN apt-get install -y --no-install-recommends libbz2-dev libncurses5-dev libgdbm-dev libgdbm-compat-dev liblzma-dev libsqlite3-dev libssl-dev openssl tk-dev uuid-dev libreadline-dev
RUN apt-get install -y --no-install-recommends libffi-dev
RUN ./configure --prefix=/usr/local/python3 && \
    make && \
    make install
RUN update-alternatives --install /usr/bin/python python /usr/local/python3/bin/python3 1
RUN update-alternatives --install /usr/bin/pip pip /usr/local/python3/bin/pip3 1
RUN update-alternatives --config python
RUN update-alternatives --config pip
RUN pip install --upgrade pip
RUN (pip --no-cache-dir install \
    coverage \
    cython \
    mock \
    pytest \
    pytest-cov \
    setuptools \
    wheel)
RUN (touch /root/WORKSPACE)


# clean
RUN rm -rf /tmp/* && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /root/.cache/pip

WORKDIR /root

RUN update-alternatives --install /usr/bin/python3 python3 /usr/local/python3/bin/python3 1
RUN update-alternatives --install /usr/bin/pip3 pip3 /usr/local/python3/bin/pip3 1
RUN update-alternatives --config python3
RUN update-alternatives --config pip3


# https://github.com/pypa/pip/issues/4924
RUN mv /usr/bin/lsb_release /usr/bin/lsb_release.bak

CMD ["bin/bash"]