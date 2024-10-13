# hadolint global ignore=DL3015
FROM node:22.8-alpine

LABEL org.opencontainers.image.source="https://github.com/mulecode/tool-set"
LABEL org.opencontainers.image.description="Node Tool-set"

WORKDIR /opt/app

ENV CHROME_BIN='/usr/bin/chromium'
ENV NG_CLI_ANALYTICS=false

RUN apk update && \
    apk upgrade && \
    apk add --no-cache chromium=~129 && \
    apk add --no-cache make=~4.4 && \
    npm install -g npm@~10.8 && \
    npm install -g @angular/cli@~18 && \
    npm install -g @aws-amplify/cli@~12 && \
    rm -rf /var/cache/apk/*

EXPOSE 4200

# Image command entry point
ENTRYPOINT ["node"]
# # Default command
CMD ["--version"]
