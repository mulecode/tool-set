FROM alpine:3.19.1

LABEL org.opencontainers.image.source="https://github.com/mulecode/tool-set"
LABEL org.opencontainers.image.description="OpenAPI Tool-set"

WORKDIR /opt/app

RUN apk update && \
    apk upgrade && \
    apk add --no-cache make=4.4.1-r2 && \
    apk add --no-cache nodejs=20.12.1-r0 && \
    apk add --no-cache npm=10.2.5-r0 && \
    rm -rf /var/cache/apk/*

# https://github.com/alexlafroscia/yaml-merge
# https://github.com/IBM/openapi-validator
# https://github.com/APIDevTools/swagger-cli
RUN npm install -g @alexlafroscia/yaml-merge@4.1.0 && \
    npm install -g ibm-openapi-validator@1.16.9 && \
    npm install -g @redocly/cli@1.11.0

# Image command entry point
ENTRYPOINT ["node"]
# # Default command
CMD ["--version"]
