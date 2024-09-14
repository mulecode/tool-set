FROM alpine:3.20

LABEL org.opencontainers.image.source="https://github.com/mulecode/tool-set"
LABEL org.opencontainers.image.description="OpenAPI Tool-set"

WORKDIR /opt/app

RUN apk update && \
    apk upgrade && \
    apk add --no-cache make=4.4.1-r2 && \
    apk add --no-cache nodejs=20.15.1-r0 && \
    apk add --no-cache npm=10.8.0-r0 && \
    rm -rf /var/cache/apk/*

RUN npm install -g @redocly/cli@1.25.2

# Image command entry point
ENTRYPOINT ["redocly"]
# # Default command
CMD ["--version"]
