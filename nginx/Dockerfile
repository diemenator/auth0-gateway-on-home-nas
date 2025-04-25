FROM openresty/openresty:alpine-fat
# Install dependencies
RUN apk add --no-cache openssl ca-certificates && update-ca-certificates \
    && /usr/local/openresty/luajit/bin/luarocks install lua-cjson \
    && /usr/local/openresty/luajit/bin/luarocks install lua-resty-http \
    && /usr/local/openresty/luajit/bin/luarocks install lua-resty-openssl \
    && /usr/local/openresty/luajit/bin/luarocks install lua-resty-session \
	&& /usr/local/openresty/luajit/bin/luarocks install lua-resty-openidc \
	&& echo done


# Make sure the nginx-module-lua can access environment variables
RUN echo "env SERVER_NAME;" >> /usr/local/openresty/nginx/conf/nginx.conf \
    && echo "env DNS_RESOLVER;" >> /usr/local/openresty/nginx/conf/nginx.conf \
    && echo "env AUTH0_PROTECTED_DOMAIN;" >> /usr/local/openresty/nginx/conf/nginx.conf \
    && echo "env AUTH0_DOMAIN;" >> /usr/local/openresty/nginx/conf/nginx.conf \
    && echo "env AUTH0_CLIENT_ID;" >> /usr/local/openresty/nginx/conf/nginx.conf \
    && echo "env AUTH0_CLIENT_SECRET;" >> /usr/local/openresty/nginx/conf/nginx.conf \
    && echo "env PROXY_TARGET;" >> /usr/local/openresty/nginx/conf/nginx.conf
