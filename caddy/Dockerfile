FROM easypi/alpine-arm

LABEL AUTHOR=黄祖林<335882264@qq.com>

WORKDIR /root

ENV RPC_SECRET=Hello
ENV ENABLE_AUTH=false
ENV DOMAIN=0.0.0.0:80
ENV ARIA2_USER=user
ENV ARIA2_PWD=password

# For build image in local quickly in China
# RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories

RUN apk update && apk add wget bash curl openrc gnupg screen aria2 tar --no-cache

RUN curl https://getcaddy.com | bash -s personal http.filemanager

ADD conf /root/conf
COPY aria2c.sh /root

COPY Caddyfile SecureCaddyfile /usr/local/caddy/

RUN mkdir -p /usr/local/www && mkdir -p /usr/local/www/aria2

#AriaNg
RUN mkdir /usr/local/www/aria2/Download && cd /usr/local/www/aria2 \
 && chmod +rw /root/conf/aria2.session \
 && wget -N --no-check-certificate https://github.com/mayswind/AriaNg/releases/download/0.4.0/aria-ng-0.4.0.zip && unzip aria-ng-0.4.0.zip && rm -rf aria-ng-0.4.0.zip \
 && chmod -R 755 /usr/local/www/aria2 \
 && chmod +x /root/aria2c.sh

#The folder to store ssl keys
VOLUME /root/conf/key
# User downloaded files
VOLUME /data

EXPOSE 6800 80 443

CMD ["/bin/sh", "/root/aria2c.sh" ]


