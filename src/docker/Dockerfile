FROM node:8.7-alpine
MAINTAINER Abner G Jacobsen - http://daspanel.com <admin@daspanel.com>

# Parse Daspanel common arguments for the build command.
ARG VERSION
ARG VCS_URL
ARG VCS_REF
ARG BUILD_DATE
ARG S6_OVERLAY_VERSION=v1.19.1.1
ARG DASPANEL_IMG_NAME=engine-base-dev
ARG DASPANEL_OS_VERSION=alpine3.6

# Set default env variables
ENV TZ="UTC"

# A little bit of metadata management.
# See http://label-schema.org/  
LABEL org.label-schema.schema-version="1.0" \
      org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.version=$VERSION \
      org.label-schema.vcs-url=$VCS_URL \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.name="daspanel/engine-base-dev" \
      org.label-schema.description="An example Daspanel project template"


ENV VAR_PREFIX=/var/run
ENV LOG_PREFIX=/var/log/
ENV TEMP_PREFIX=/tmp
ENV CACHE_PREFIX=/var/cache

# Inject files in container file system
COPY rootfs /

RUN set -x \

    # Install minimal packages
    && apk add --update --no-cache ca-certificates wget tzdata unzip libcap curl tar bash git \
        build-base  \
        autoconf file g++ gcc make linux-headers libtool pcre-dev \
        binutils isl libatomic libc-dev musl-dev re2c libstdc++ libgcc \
        binutils-libs mpc1 mpfr3 gmp libgomp coreutils freetype-dev \
        libjpeg-turbo-dev libltdl libmcrypt-dev libpng-dev imap-dev openssl-dev \
        yaml-dev shadow python automake nasm \

    # Install webpack, gulp globally
    && npm install webpack -g \
    && npm install gulp-cli -g \
    && npm install bower -g \
    && npm install node-gyp -g \

    # Remove user coming from the node image wich id 1000 can conflict when daspanel user is created
    && deluser node \

    # Cleanup
    && rm -rf /tmp/* \
    && rm -rf /var/cache/apk/*



