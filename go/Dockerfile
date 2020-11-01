FROM ubuntu:18.04

ENV GOLANG_VERSION 1.15
ENV PROTOBUF_VERSION=3.13.0

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
        openssh-client \
        openjdk-11-jdk \
        g++ unzip zip \
        openjdk-11-jre-headless)

# Install Golang
RUN (curl -L https://dl.google.com/go/go$GOLANG_VERSION.linux-amd64.tar.gz | tar zx -C /usr/local)
ENV PATH /usr/local/go/bin:$PATH
RUN mkdir -p /go/src /go/bin && chmod -R 777 /go
ENV GOROOT /usr/local/go
ENV GOPATH /go
ENV PATH /go/bin:$PATH

# Install go packages
RUN go env -w GO111MODULE=on && \
	go env -w GOPROXY=https://goproxy.io,direct
COPY go.mod /go.mod
RUN go mod download

# Install proto buffer
# refer to https://github.com/golang/protobuf
RUN wget -P /tmp https://github.com/protocolbuffers/protobuf/releases/download/v${PROTOBUF_VERSION}/protoc-${PROTOBUF_VERSION}-linux-x86_64.zip
RUN unzip /tmp/protoc-${PROTOBUF_VERSION}-linux-x86_64.zip -d protoc3 && \
	rm /tmp/protoc-${PROTOBUF_VERSION}-linux-x86_64.zip
RUN mv protoc3/bin/* /usr/local/bin/ && mv protoc3/include/* /usr/local/include/

# Install GoLang proto gen
RUN go get -u -v github.com/golang/protobuf/protoc-gen-go

# Manually clone golang.org/x/XXX packages from their github mirrors.
WORKDIR /go/src/golang.org/x/
RUN git clone --progress https://github.com/golang/debug.git && \
git clone --progress https://github.com/golang/glog.git && \
git clone --progress https://github.com/golang/time.git && \
git clone --progress https://github.com/golang/sync.git && \
git clone --progress https://github.com/golang/crypto && \
git clone --progress https://github.com/golang/tools && \
git clone --progress https://github.com/golang/sys

# Install packr2
RUN go get -u github.com/gobuffalo/packr/v2/packr2


# clean
RUN rm -rf /tmp/* && rm -rf /var/lib/apt/lists/*

CMD ["bin/bash"]
