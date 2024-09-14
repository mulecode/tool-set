FROM ubuntu:24.10

LABEL org.opencontainers.image.source="https://github.com/mulecode/tool-set"
LABEL org.opencontainers.image.description="python-playwright Tool-set"

WORKDIR /opt/app

# Update and install dependencies
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
     build-essential \
     make \
     zip \
     tar \
     gzip \
     gcc \
     g++ \
     libffi-dev \
     libssl-dev \
     libbz2-dev \
     libxslt1-dev \
     sqlite3 \
     libsqlite3-dev \
     libpango1.0-dev \
     wget \
     zlib1g-dev \
     git \
     libnss3 \
     dbus \
     at-spi2-core \
     libcups2 \
     libdrm-dev \
     libxcomposite1 \
     libxdamage1 \
     libxfixes3 \
     libxrandr2 \
     mesa-common-dev \
     libxkbcommon0 \
     alsa-base && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

## Install Python 3.12.5
RUN wget -q https://www.python.org/ftp/python/3.12.5/Python-3.12.5.tgz --no-check-certificate && \
    tar -xvf Python-3.12.5.tgz && \
    cd Python-3.12.5 && \
    ./configure --enable-optimizations --enable-loadable-sqlite-extensions --with-ensurepip=install && \
    make && \
    make install && \
    cd /opt/app && \
    rm -rf Python-* && \
    ln -sf /usr/local/bin/python3.12 /usr/bin/python3 && \
    ln -sf /usr/local/bin/pip3.12 /usr/bin/pip3

## Install pip
RUN python3 -m pip install --no-cache-dir --upgrade pip==24.2 && \
    pip3 install --no-cache-dir black==24.8.0 && \
    pip3 install --no-cache-dir playwright==1.45.1 && \
    playwright install-deps && \
    playwright install

# Image command entry point
ENTRYPOINT ["python3"]
# # Default command
CMD ["--version"]
