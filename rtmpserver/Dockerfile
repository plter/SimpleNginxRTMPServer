FROM ubuntu:20.04

RUN apt-get update
RUN apt-get install -y gcc g++ make libssl-dev

ENV NGINX_RTMP_MODULE_VERSION 1.2.2

COPY nginx-1.17.6.tar.gz /opt/
COPY nginx-rtmp-module-${NGINX_RTMP_MODULE_VERSION}.tar.gz /opt/
COPY pcre-8.34.tar.gz /opt
COPY zlib-1.2.11.tar.gz /opt

RUN cd /opt/ \
    &&tar -xzvf pcre-8.34.tar.gz \
    &&tar -xzvf zlib-1.2.11.tar.gz \
    &&tar -xzvf nginx-1.17.6.tar.gz \
    &&tar -xzvf nginx-rtmp-module-${NGINX_RTMP_MODULE_VERSION}.tar.gz

RUN cd /opt/pcre-8.34 \
    &&./configure \
    &&make \
    &&make install

RUN cd /opt/zlib-1.2.11 \
    &&./configure \
    &&make \
    &&make install

RUN cd /opt/nginx-1.17.6 \
    &&./configure --add-module=/opt/nginx-rtmp-module-${NGINX_RTMP_MODULE_VERSION} \
    &&make \
    &&make install

RUN mv /usr/local/nginx/conf/nginx.conf /usr/local/nginx/conf/nginx.conf.bak

COPY nginx.conf /usr/local/nginx/conf/

