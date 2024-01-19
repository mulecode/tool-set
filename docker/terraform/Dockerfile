FROM hashicorp/terraform:1.7.4

LABEL org.opencontainers.image.source="https://github.com/mulecode/tool-set"
LABEL org.opencontainers.image.description="Terraform 1.7.4 Tool-set"

WORKDIR /opt/app

# Updates apk
RUN apk update &&  \
    apk upgrade && \
    apk add --no-cache make=4.4.1-r2 && \
    rm -rf /var/cache/apk/*

# Default entry point
ENTRYPOINT ["/bin/terraform"]
# Default command
CMD ["--version"]
