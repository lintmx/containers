# stage 1 拉取源码
FROM alpine as git-stage

ARG VERSION=v1.6.0

WORKDIR /app

RUN apk --no-cache add git \
    && git clone https://github.com/MCSManager/UI \
    && cd UI \
    && git checkout ${VERSION}

# stage 2 构建页面
FROM node:lts-alpine as build-stage

WORKDIR /app

COPY --from=git-stage /app/UI .

RUN npm install \
    && npm run build

# stage 3 运行
FROM nginx:stable-alpine as prod-stage

WORKDIR /app

COPY --from=build-stage /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
