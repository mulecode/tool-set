# hadolint global ignore=DL3015
FROM ubuntu:24.10

LABEL org.opencontainers.image.source="https://github.com/mulecode/tool-set"
LABEL org.opencontainers.image.description="python-playwright Tool-set"

ENV PYTHON_VERSION=3.12.5
ENV BLACK_VERSION=24.8.0
ENV PIP_VERSION=24.2
ENV PLAYWRIGHT_VERSION=1.45.1

WORKDIR /opt/app

# Update and install dependencies
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
     build-essential=12.10ubuntu1 \
     make=4.3-4.1build2 \
     zip=3.0-14 \
     tar=1.35+dfsg-3build1 \
     gzip=1.12-1.1ubuntu1 \
     gcc=4:14.1.0-2ubuntu1 \
     g++=4:14.1.0-2ubuntu1 \
     libffi-dev=3.4.6-1build1 \
     libssl-dev=3.3.1-2ubuntu1 \
     libbz2-dev=1.0.8-6 \
     libxslt1-dev=1.1.39-0exp1ubuntu1 \
     sqlite3=3.46.1-1 \
     libsqlite3-dev=3.46.1-1 \
     libpango1.0-dev=1.54.0+ds-2 \
     wget=1.24.5-1ubuntu2 \
     zlib1g-dev=1:1.3.dfsg+really1.3.1-1ubuntu1 \
     git=1:2.45.2-1ubuntu1 \
     libnss3=2:3.103-1 \
     dbus=1.14.10-4ubuntu5 \
     at-spi2-core=2.53.1-2 \
     libcups2=2.4.10-1ubuntu1 \
     libdrm-dev=2.4.122-1 \
     libxcomposite1=1:0.4.5-1build3 \
     libxdamage1=1:1.1.6-1build1 \
     libxfixes3=1:6.0.0-2build1 \
     libxrandr2=2:1.5.4-1 \
     mesa-common-dev=24.2.2-1ubuntu1 \
     libxkbcommon0=1.6.0-1build1 \
     alsa-base=1.0.25+dfsg-0ubuntu7 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

## Install Python 3.12.5
RUN wget -q https://www.python.org/ftp/python/${PYTHON_VERSION}/Python-${PYTHON_VERSION}.tgz --no-check-certificate && \
    tar -xvf Python-${PYTHON_VERSION}.tgz

WORKDIR /opt/app/Python-${PYTHON_VERSION}
RUN ./configure --enable-optimizations --enable-loadable-sqlite-extensions --with-ensurepip=install && make && make install

WORKDIR /opt/app
RUN rm -rf Python-* && \
    ln -sf /usr/local/bin/python3.12 /usr/bin/python3 && \
    ln -sf /usr/local/bin/pip3.12 /usr/bin/pip3

## Install pip and Playwright
RUN python3 -m pip install --no-cache-dir --upgrade pip==${PIP_VERSION} --root-user-action=ignore && \
    pip3 install --no-cache-dir black==${BLACK_VERSION} && \
    pip3 install --no-cache-dir playwright==${PLAYWRIGHT_VERSION}

RUN playwright install-deps && \
    playwright install

# Image command entry point
ENTRYPOINT ["python3"]
CMD ["--version"]
