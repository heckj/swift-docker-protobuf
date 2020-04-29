FROM swift:5.2-bionic
LABEL maintainer="Joe Heck <heckj@mac.com>"
LABEL Description="Docker Container for the Swift programming language w/ Protobuf tooling"

RUN export DEBIAN_FRONTEND=noninteractive DEBCONF_NONINTERACTIVE_SEEN=true && apt-get -q update && \
    apt-get -q install -y \
    wget \
    curl \
    unzip \
    autoconf \
    automake \
    libtool \
    make \
    && rm -r /var/lib/apt/lists/*

ARG PROTOC_VERSION=v3.2.0
ARG PROTOC_VERSION_DIR=protobuf-3.2.0
ARG SWIFT_PROTOBUF_VERSION=1.8.0
ARG SWIFT_PROTOBUF_VERSION_DIR=swift-protobuf-1.8.0
 
ENV PROTOC_VERSION=$PROTOC_VERSION \
    SWIFT_PROTOBUF_VERSION=$SWIFT_PROTOBUF_VERSION \
    SWIFT_PROTOBUF_VERSION_DIR=$SWIFT_PROTOBUF_VERSION_DIR

RUN set -e; \
    # download and install the protobuf underlying pieces
    wget https://github.com/google/protobuf/archive/${PROTOC_VERSION}.tar.gz \
    && tar xzf ${PROTOC_VERSION}.tar.gz \
    && cd ${PROTOC_VERSION_DIR} \
    && ./autogen.sh \
    && ./configure CXXFLAGS=-I/usr/local/include LDFLAGS=-L/usr/local/lib \
    && make && make install \
    # - Unpack the toolchain, set libs permissions, and clean up.
    # - download and install swift-protobuf
    && wget https://github.com/apple/swift-protobuf/archive/${SWIFT_PROTOBUF_VERSION}.tar.gz \
    && tar xzf ${SWIFT_PROTOBUF_VERSION}.tar.gz \
    && cd ${SWIFT_PROTOBUF_VERSION_DIR} \
    && make && make install \
    #&& tar -xzf swift.tar.gz --directory / --strip-components=1 \
    #&& chmod -R o+r /usr/lib/swift \
    #&& rm -rf "$GNUPGHOME" swift.tar.gz.sig swift.tar.gz \
    && apt-get purge --auto-remove -y curl wget unzip autoconf automake libtool make

# Print Installed Swift Version
RUN swift --version
RUN protoc-gen-swift --version
