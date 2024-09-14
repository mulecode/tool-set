FROM node:22.4.0-slim

LABEL org.opencontainers.image.source="https://github.com/mulecode/tool-set"
LABEL org.opencontainers.image.description="Node Tool-set"

WORKDIR /opt/app

ENV CHROME_BIN='/usr/bin/chromium'
ENV NG_CLI_ANALYTICS=false

RUN apt -y update && \
    apt -y upgrade && \
    apt -y install chromium && \
    apt -y install make && \
    npm install -g npm@10.8.3 && \
    npm install -g @angular/cli@18 && \
    npm install -g @aws-amplify/cli@12.12.6 && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /var/cache/apt/* && \
    rm -rf /var/cache/debconf/*

EXPOSE 4200

# Image command entry point
ENTRYPOINT ["node"]
# # Default command
CMD ["--version"]
