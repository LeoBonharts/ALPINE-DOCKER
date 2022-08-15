FROM alpine:edge

# LABEL 
LABEL org.opencontainers.image.source="https://github.com/amirulandalib/mltb-alpine"
LABEL org.opencontainers.image.description="Docker for MLTB by Anasty based on Alpine EDGE docker image"

ARG TARGETPLATFORM BUILDPLATFORM

# install packages via APK

RUN apk update && apk upgrade && \
    apk add --upgrade --no-cache \
    musl-dev qbittorrent python3 python3-dev busybox \
    qbittorrent-nox py3-pip py3-lxml aria2 p7zip xz curl pv jq ffmpeg \
    musl-locales neofetch git make g++ gcc automake zip unzip autoconf \
    libtool curl-dev libsodium-dev \
    c-ares-dev sqlite-dev freeimage-dev swig boost-dev \
    libpthread-stubs zlib-dev libpq-dev libffi-dev py3-virtualenv libffi \
    bash alpine-sdk clang clang-dev dpkg cmake ccache icu-data-full gettext gettext-dev gawk \
    && apk add --upgrade --no-cache crypto++-dev crypto++ --repository=http://dl-cdn.alpinelinux.org/alpine/edge/testing && \
    pip3 install wheel \
    && apk del openssl openssl-dev libressl libressl-dev \
    && apk add --no-cache openssl openssl-dev libressl libressl-dev


RUN ln -sf /usr/bin/clang /usr/bin/cc \
  && ln -sf /usr/bin/clang++ /usr/bin/c++ \
  && update-alternatives --install /usr/bin/cc cc /usr/bin/clang 10\
  && update-alternatives --install /usr/bin/c++ c++ /usr/bin/clang++ 10\
  && update-alternatives --auto cc \
  && update-alternatives --auto c++ \
  && update-alternatives --display cc \
  && update-alternatives --display c++ \
  && ls -l /usr/bin/cc /usr/bin/c++ \
  && cc --version \
  && c++ --version

        
# Installing Mega SDK Python Binding
ENV PYTHONWARNINGS=ignore

RUN git clone https://github.com/meganz/sdk.git ~/home/sdk \
    && cd ~/home/sdk && rm -rf .git \
    && autoupdate -fIv && ./autogen.sh \
    && ./configure CFLAGS='-fpermissive' CXXFLAGS='-fpermissive' CPPFLAGS='-fpermissive' CCFLAGS='-fpermissive' \
    --disable-silent-rules --enable-python --with-sodium --disable-examples --with-python3 \
    && make -j$(nproc --all) \
    && cd bindings/python/ && python3 setup.py bdist_wheel \
    && cd dist && ls && pip3 install --no-cache-dir *.whl  

RUN apk update && apk upgrade



WORKDIR /usr/src/app
RUN chmod 777 /usr/src/app

RUN locale -a
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8
