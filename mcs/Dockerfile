# stage 1 拉取源码
FROM alpine as build-stage

ARG VERSION=v9.2.0

WORKDIR /app

RUN apk --no-cache add git \
    && git clone https://github.com/MCSManager/MCSManager \
    && cd MCSManager \
    && git checkout ${VERSION}

# stage 2 运行
FROM node:lts-alpine as prod-stage

WORKDIR /app

COPY --from=build-stage /app/MCSManager .

RUN npm install \
    && npm run build

EXPOSE 23333

CMD ["node", "/app/dist/app.js"]
