FROM registry.cn-hangzhou.aliyuncs.com/jtz/contos:ContOS

MAINTAINER jtz

#yum
RUN yum -y update &&\
    yum install telnet -y &&\
    yum -y install wget &&\
    yum -y install gcc gcc-c++ autoconf automake make &&\
    yum -y install pcre pcre-devel zlib openssl openssl-devel &&\
	yum clean all

#nginx
ENV NGINX_VERSION 1.15.0

WORKDIR /tmp
RUN wget http://nginx.org/download/nginx-$NGINX_VERSION.tar.gz &&\
    tar xzf nginx-$NGINX_VERSION.tar.gz &&\
    cd /tmp/nginx-$NGINX_VERSION &&\
    ./configure \
        --prefix=/usr/local/nginx \
        --with-http_ssl_module \
        --with-http_sub_module \
        --with-http_dav_module \
        --with-http_flv_module \
        --with-http_gzip_static_module \
        --with-http_stub_status_module \
        --with-debug && \
    make && \
    make install

# 设置环境变量
ENV PATH /usr/local/nginx/sbin:$PATH

#开放端口
EXPOSE 80 443

# 执行命令
ENTRYPOINT ["nginx", "-g", "daemon off;"] 

