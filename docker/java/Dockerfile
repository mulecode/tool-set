FROM alpine:3.19.1

LABEL org.opencontainers.image.source="https://github.com/mulecode/tool-set"
LABEL org.opencontainers.image.description="Java 21 Tool-set"

# Set environment variables for configuration
ENV JAVA_HOME=/usr/lib/jvm/java-21-openjdk
ENV MAVEN_HOME=/usr/share/java/maven-3

WORKDIR /opt/app

RUN apk update && \
    apk upgrade && \
    apk add --no-cache make=4.4.1-r2 && \
    apk add --no-cache openjdk21=21.0.4_p7-r0 && \
    apk add --no-cache maven=3.9.5-r0 && \
    rm -rf /var/cache/apk/*

# Set default values for environment variables
ENV PATH=$JAVA_HOME/bin:$MAVEN_HOME/bin:$PATH

# Image command entry point
ENTRYPOINT ["java"]
# Default command
CMD ["--version"]
