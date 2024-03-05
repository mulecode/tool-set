FROM amazonlinux:2

LABEL org.opencontainers.image.source="https://github.com/mulecode/tool-set"
LABEL org.opencontainers.image.description="Python 3.9.18 Tool-set"

ENV VERSION=3.9.18

WORKDIR /opt/app

# Updates yum
RUN yum -y update && \
    yum -y upgrade && \
    yum install -y make-3.82-24.amzn2 \
        zip-3.0-11.amzn2.0.2 \
        tar-1.26-35.amzn2.0.3 \
        gzip-1.5-10.amzn2.0.1 \
        gcc-7.3.1-17.amzn2 \
        libffi-devel-3.0.13-18.amzn2.0.12 \
        openssl-devel-1.0.2k-24.amzn2.0.12 \
        bzip2-devel-1.0.6-13.amzn2.0.3 \
        libxslt-1.1.28-6.amzn2 \
        sqlite-devel-3.7.17-8.amzn2.1.2 \
        pango-1.42.4-4.amzn2 \
        wget-1.14-18.amzn2.1 && \
    yum -y clean all && \
    rm -rf /var/cache

# install python 3
RUN wget -q https://www.python.org/ftp/python/${VERSION}/Python-${VERSION}.tgz && \
    tar -xvf Python-${VERSION}.tgz

WORKDIR /opt/app/Python-${VERSION}
RUN ./configure --enable-loadable-sqlite-extensions --with-ensurepip=install && make && make install && \
    pip3 install --no-cache-dir --upgrade pip==24.0 && \
    pip3 install --no-cache-dir black==23.3.0

WORKDIR /opt/app
RUN rm -rf Python-*

# Image command entry point
ENTRYPOINT ["python3"]
# # Default command
CMD ["--version"]
