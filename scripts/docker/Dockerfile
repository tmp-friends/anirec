# TODO: versionを指定する
FROM node:16-alpine

USER root
ENV TZ=Asia/Tokyo \
    LANG=ja_JP.UTF-8

ARG uid
ARG gid
ARG user

RUN chown -R $user:$user /var \
    && chmod -R 0755 /var \
    && install -m 0755 -o $user -g $user -d /var/www \
    && ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime


WORKDIR /var/www
USER $user

COPY --chown=$user:$user /app/package*.json ./

# user権限でnpm iするための設定
# @see: https://zenn.dev/ikeo/articles/8d0c88dcedf256b09f73
RUN install -m 0755 -o $user -g $user -d ~/.npm-global \
    && npm config set prefix "~/.npm-global"
ENV PATH=~/.npm-global/bin:$PATH

RUN npm i

COPY --chown=$user:$user /app ./

CMD [ "npm", "run", "dev" ]
