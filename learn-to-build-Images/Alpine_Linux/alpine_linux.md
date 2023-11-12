# Alpine Linux ist also an distributer of Linux like Ubuntu, Debian or Fedora. Alpine built aroun musl libx and busybox 
# and is lightweight as ubuntu. For exampla ubuntu has 28 MB alpine only 2.8 MB 

FROM alpine:latest

EXPOSE 80

ARG FILENAME="nginx-1.19.2"
ARG EXTENSION="tar.gz"

ADD https://nginx.org/download/${FILENAME}.${EXTENSION} .

RUN apk add --no-cache pcre zlib && \   # Instead of using apt-get, we use apk add  
    apk add --no-cache \                # the --no-cache option to prevent caching of the downloaded package
            --virtual .build-deps \     # option --virtual used for bundling a bunch of packages into a single virtual package for easier management
            build-base \                # and will signatet with .build-deps and in line 32 with the comand apk del removed
            pcre-dev \
            zlib-dev \
            openssl-dev && \
    tar -xvf ${FILENAME}.${EXTENSION} && rm ${FILENAME}.${EXTENSION} && \
    cd ${FILENAME} && \
    ./configure \
        --sbin-path=/usr/bin/nginx \
        --conf-path=/etc/nginx/nginx.conf \
        --error-log-path=/var/log/nginx/error.log \
        --http-log-path=/var/log/nginx/access.log \
        --with-pcre \
        --pid-path=/var/run/nginx.pid \
        --with-http_ssl_module && \
    make && make install && \
    cd / && rm -rfv /${FILENAME} && \
    apk del .build-deps

CMD ["nginx", "-g", "daemon off;"]

# now run the command 
-- docker image build --tag custom-nginx:built .