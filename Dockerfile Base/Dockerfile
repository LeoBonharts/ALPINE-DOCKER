FROM alpine:edge

# LABEL 
LABEL org.opencontainers.image.source="https://github.com/amirulandalib/mltb-alpine"
LABEL org.opencontainers.image.description="Docker for MLTB by Anasty based on Alpine EDGE docker image"

ARG TARGETPLATFORM BUILDPLATFORM

# install packages via APK
RUN echo "@testing http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories && \
    echo "@community http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories && \
    apk update && apk upgrade && \
    apk add --upgrade --no-cache crypto++-dev \
    musl-dev qbittorrent python3-dev busybox \
    qbittorrent-nox py3-pip py3-lxml aria2 p7zip xz curl pv jq ffmpeg \
    musl-locales neofetch git make g++ gcc automake zip unzip autoconf \
    libtool curl-dev libsodium-dev libressl-dev openssl-dev \
    c-ares-dev sqlite-dev freeimage-dev swig boost-dev \
    libpthread-stubs zlib-dev libpq-dev libffi-dev py3-virtualenv libffi \
    bash alpine-sdk

        
# Installing Mega SDK Python Binding
ENV PYTHONWARNINGS=ignore

RUN git clone https://github.com/AmirulAndalib/MegaNzSdk ~/home/sdk \
    && cd ~/home/sdk && rm -rf .git \
    && autoupdate -fIv && ./autogen.sh \
    && ./configure --disable-silent-rules --enable-python --with-sodium --disable-examples --with-python3 \
    && make -j$(nproc --all) \
    && cd bindings/python/ && python setup.py bdist_wheel \
    && cd dist && ls && pip install --no-cache-dir *.whl  

RUN apk update && apk upgrade



WORKDIR /usr/src/app
RUN chmod 777 /usr/src/app

RUN locale -a
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8
