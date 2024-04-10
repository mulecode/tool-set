FROM amazonlinux:2023.4.20240401.1
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
     openssl-devel-1:3.0.8-1.amzn2023.0.11 \
     bzip2-devel-1.0.8-6.amzn2023.0.2 \
     libxslt-1.1.34-5.amzn2023.0.2 \
     sqlite-devel-3.40.0-1.amzn2023.0.4 \
     pango-1.48.10-1.amzn2023.0.3 \
     wget-1.21.3-1.amzn2023.0.3 \
     zlib-devel-1.2.11-33.amzn2023.0.5 \
     git-2.40.1-1.amzn2023.0.1 && \
    yum -y clean all && \
    rm -rf /var/cache

# install python 3
RUN wget -q https://www.python.org/ftp/python/3.9.19/Python-3.9.19.tgz && \
    tar -xvf Python-3.9.19.tgz && \
    cd Python-*/ && ./configure --enable-optimizations --enable-loadable-sqlite-extensions --with-ensurepip=install && make && make install && \
    cd ../ && rm -rf Python-*

# Install pip
RUN python3 -m pip install --upgrade pip==24.0
# Install Black formatter
RUN pip3 install --no-cache-dir black==24.3.0

# Image command entry point
ENTRYPOINT ["python3"]
# # Default command
CMD ["--version"]
