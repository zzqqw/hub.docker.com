# RUN

~~~
//Loading the default configuration
docker run --name nginx -p 8080:80 -d zhiqiangwang/docker:openresty-alpine
//Download the remote nginx configuration to the local computer for loading
docker run --name nginx -p 8080:80 -e NGINX_CONF_PATH="https://cdn.jsdelivr.net/gh/izhiqiang/hub.docker.com@main/openresty/nginx.conf/localfile.conf" -d zhiqiangwang/docker:openresty-alpine
//Load the nginx configuration in the project
docker run --name nginx -p 8080:80 -e NGINX_CONF_PATH="/data/wwwroot/laravel/nginx.conf" -d zhiqiangwang/docker:openresty-alpine
~~~

# luarocks包管理

~~~
# 安装第三方包
ARG LUAROCKS_VERSION=3.9.0
RUN apk add --no-cache --virtual .build-deps perl-dev
RUN apk add --no-cache bash build-base libintl linux-headers make musl outils-md5 perl unzip wget gettext curl
RUN cd /tmp && curl -fSL https://luarocks.github.io/luarocks/releases/luarocks-${LUAROCKS_VERSION}.tar.gz -o luarocks-${LUAROCKS_VERSION}.tar.gz && \
    tar -xzvf luarocks-${LUAROCKS_VERSION}.tar.gz && \
    cd luarocks-${LUAROCKS_VERSION} && \
    ./configure --prefix=/usr/local/openresty/luajit --with-lua=/usr/local/openresty/luajit --lua-suffix=jit-2.1.0-beta3 --with-lua-include=/usr/local/openresty/luajit/include/luajit-2.1 && \
    make build && make install
# 将luarocks包管理工具加入到环境变量中
ENV PATH=$PATH:/usr/local/openresty/luajit/bin
~~~

