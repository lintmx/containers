# stage 1 拉取源码
FROM alpine as build-stage

ARG VERSION=v1.2.0

WORKDIR /app

RUN apk --no-cache add git \
    && git clone https://github.com/MCSManager/Daemon \
    && cd Daemon \
    && git checkout ${VERSION}

# stage 2 运行
FROM node:lts-alpine as prod-stage

WORKDIR /app

COPY --from=build-stage /app/Daemon .

RUN npm install \
    && npm run build

EXPOSE 24444

CMD ["node", "/app/dist/app.js"]
