FROM alpine:edge

# LABEL 
LABEL org.opencontainers.image.source="https://github.com/amirulandalib/mltb-alpine"
LABEL org.opencontainers.image.description="Docker for MLTB by Anasty based on Alpine EDGE docker image"

ARG TARGETPLATFORM BUILDPLATFORM

# install packages via APK
RUN apk update && apk upgrade && \
    apk add crypto++-dev --repository=http://dl-cdn.alpinelinux.org/alpine/edge/testing && \
    apk add --upgrade --no-cache \
    musl-dev qbittorrent python3-dev busybox \
    qbittorrent-nox py3-pip py3-lxml aria2 p7zip xz curl pv jq ffmpeg \
    musl-locales neofetch git make g++ gcc automake zip unzip autoconf \
    libtool curl-dev libsodium-dev libressl-dev openssl-dev \
    c-ares-dev sqlite-dev freeimage-dev swig boost-dev \
    libpthread-stubs zlib-dev libpq-dev libffi-dev py3-virtualenv libffi \
    bash alpine-sdk
        
# Installing Mega SDK Python Binding
ENV PYTHONWARNINGS=ignore
ENV MEGA_SDK_VERSION="3.12.3"

RUN wget https://github.com/AmirulAndalib/megaSdkC-Wheel/releases/download/latest/megasdk-4.0.1-py2.py3-none-any.whl \
    && pip3 install --no-cache-dir megasdk-*.whl 

RUN apk update && apk upgrade


# Fix locales

ENV MUSL_LOCALE_DEPS cmake make musl-dev gcc gettext-dev libintl

RUN apk add --no-cache \
    $MUSL_LOCALE_DEPS \
    && wget https://gitlab.com/rilian-la-te/musl-locales/-/archive/master/musl-locales-master.zip \
    && unzip musl-locales-master.zip \
      && cd musl-locales-master \
      && cmake -DLOCALE_PROFILE=OFF -D CMAKE_INSTALL_PREFIX:PATH=/usr . && make && make install \
      && cd .. && rm -r musl-locales-master

#

WORKDIR /usr/src/app
RUN chmod 777 /usr/src/app

RUN locale -a
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8
