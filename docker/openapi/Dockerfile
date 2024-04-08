FROM node:18.10.0-alpine3.15
WORKDIR /opt/app


RUN apk update && \
    apk upgrade && \
    apk add --no-cache make=4.4.1-r2 && \
    apk add --no-cache openjdk21=21.0.2_p13-r0 && \
    apk add --no-cache maven=3.9.5-r0 && \
    apk add --no-cache nodejs && \
    apk add --no-cache npm && \
    rm -rf /var/cache/apk/*

# https://github.com/alexlafroscia/yaml-merge
# https://github.com/IBM/openapi-validator
# https://github.com/APIDevTools/swagger-cli
RUN npm install -g @alexlafroscia/yaml-merge && \
    npm install -g ibm-openapi-validator && \
    npm install -g @apidevtools/swagger-cli

# Image command entry point
ENTRYPOINT ["node"]
# # Default command
CMD ["--version"]
