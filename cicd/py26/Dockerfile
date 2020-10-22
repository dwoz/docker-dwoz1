FROM debian:buster

WORKDIR /root
RUN apt-get update -qy && apt-get install -y \
	gcc-7 build-essential zlib1g-dev libreadline-dev libsqlite3-dev \
        wget curl llvm libncurses5-dev xz-utils tk-dev libxml2-dev \
        libxmlsec1-dev libffi-dev liblzma-dev libbz2-dev \
   && wget -q https://ftp.openssl.org/source/old/1.0.2/openssl-1.0.2u.tar.gz \
   && tar xf openssl-1.0.2u.tar.gz \
   && cd openssl-1.0.2u \
   && ./Configure linux-x86_64 \
   && ./config --openssldir=/usr/local enable-shared \
   && make && make install \
   && cd .. \
   && rm -r openssl-1.0.2u \
   && rm openssl-1.0.2u.tar.gz \
   && ln -s /lib/x86_64-linux-gnu/libz.so.1 /lib/x86_64-linux-gnu/libz.so \
   && ln -s /lib/x86_64-linux-gnu/libbz2.so.1 /lib/x86_64-linux-gnu/libbz2.so \
   && ln -s /lib/x86_64-linux-gnu/libreadline.so.7 /lib/x86_64-linux-gnu/libreadline.so \
   && ldconfig \
   && wget -q https://www.python.org/ftp/python/2.6.9/Python-2.6.9.tgz \
   && tar xf Python-2.6.9.tgz \
   && cd Python-2.6.9 \
   && CC=gcc-7 LDFLAGS="-L/usr/local/lib -L/lib/x86_64-linux-gnu  -L/usr/lib/x86_64-linux-gnu" ./configure \
   && make && make install \
   && cd .. \
   && rm -r Python-2.6.9 \
   && rm Python-2.6.9.tgz \
   && wget -q https://bootstrap.pypa.io/2.6/get-pip.py \
   && python2.6 get-pip.py \
   && /usr/local/bin/pip install virtualenv \
   && rm get-pip.py \
   && apt-get remove -y --purge gcc-7 build-essential wget curl \
   && apt-get autoremove --purge -y \
   && rm -rf /var/lib/apt/lists/*
