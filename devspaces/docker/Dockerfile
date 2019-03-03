FROM ubuntu:18.04

LABEL description="This file generates a docker image containing everything needed to build and run CockroachDB"

WORKDIR /data

ENV GOROOT=/usr/local/go
ENV GOPATH=/data
ENV PATH=$GOPATH/bin:$GOROOT/bin:$PATH

RUN apt-get update && apt-get install -y curl wget build-essential bison libncurses5-dev libncursesw5-dev && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get install -y yarn && \
    mkdir /data/src && \
    wget https://dl.google.com/go/go1.11.4.linux-amd64.tar.gz && \
    tar -xvf go1.11.4.linux-amd64.tar.gz && \
    mv go /usr/local && \
    rm go1.11.4.linux-amd64.tar.gz && \
    apt-get clean
