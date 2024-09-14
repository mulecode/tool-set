FROM amazonlinux:2023.5.20240903.0

LABEL org.opencontainers.image.source="https://github.com/mulecode/tool-set"
LABEL org.opencontainers.image.description="Python 3.9.19 Tool-set"

ENV PYTHON_VERSION=3.9.18
ENV BLACK_VERSION=24.8.0
ENV PIP_VERSION=24.2

WORKDIR /opt/app

# Updates yum
RUN yum -y update && \
    yum -y upgrade && \
    yum install -y make-4.3-5.amzn2023.0.2 \
     zip-3.0-28.amzn2023.0.2 \
     tar-2:1.34-1.amzn2023.0.4 \
     gzip-1.12-1.amzn2023.0.1 \
     gcc-11.4.1-2.amzn2023.0.2 \
     libffi-devel-3.4.4-1.amzn2023.0.1 \
     openssl-devel-1:3.0.8-1.amzn2023.0.14 \
     bzip2-devel-1.0.8-6.amzn2023.0.2 \
     libxslt-1.1.34-5.amzn2023.0.2 \
     sqlite-devel-3.40.0-1.amzn2023.0.4 \
     pango-1.48.10-1.amzn2023.0.3 \
     wget-1.21.3-1.amzn2023.0.4 \
     zlib-devel-1.2.11-33.amzn2023.0.5 \
     git-0:2.40.1-1.amzn2023.0.3 && \
    yum -y clean all && \
    rm -rf /var/cache

# install python 3
RUN wget -q https://www.python.org/ftp/python/${PYTHON_VERSION}/Python-${PYTHON_VERSION}.tgz && \
    tar -xvf Python-${PYTHON_VERSION}.tgz

WORKDIR /opt/app/Python-${PYTHON_VERSION}
RUN ./configure --enable-loadable-sqlite-extensions --with-ensurepip=install && make && make install && \
    pip3 install --no-cache-dir --upgrade pip==${PIP_VERSION} && \
    pip3 install --no-cache-dir black==${BLACK_VERSION}

WORKDIR /opt/app
RUN rm -rf Python-*

# Image command entry point
ENTRYPOINT ["python3"]
# # Default command
CMD ["--version"]
