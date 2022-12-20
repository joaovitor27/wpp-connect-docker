FROM node:16.19-alpine3.16 as builder

RUN apk add wget && \
    apk add --no-cache git

WORKDIR /home/node
RUN git clone https://github.com/wppconnect-team/wppconnect-frontend-vue /home/node/app 

WORKDIR /home/node/app
COPY ./config.js /home/node/app/public
RUN yarn install

FROM node:16.19-alpine3.16
ENV PUPPETEER_SKIP_CHROMIUM_DOWNLOAD="true"
ENV CHROME_BIN="/usr/bin/chromium-browser"

WORKDIR /home/node/app

RUN set -x \
    && apk update \
    && apk upgrade \
    && apk add --no-cache \
    udev \
    ttf-freefont \
    chromium \
    && npm install puppeteer

COPY --from=builder /home/node/app/ .
EXPOSE 3000