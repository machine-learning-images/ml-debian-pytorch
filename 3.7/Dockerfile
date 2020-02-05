FROM debian:stable

# ensure our python is preferred over distribution python
ENV PATH /usr/local/bin:$PATH

ENV LANG C.UTF-8

ENV PYTHON_VERSION 3.7.6

ENV PYTHON_PIP_VERSION 20.0.2

RUN apt-get update \
&& apt-get install build-essential cmake git libreadline-gplv2-dev libncursesw5-dev libssl-dev \
    libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev libffi-dev libprotobuf-dev libprotoc-dev protobuf-compiler wget -y

RUN cd /usr/src \
&& wget https://www.python.org/ftp/python/$PYTHON_VERSION/Python-$PYTHON_VERSION.tgz \
&& tar xzf Python-$PYTHON_VERSION.tgz \
&& cd Python-$PYTHON_VERSION \
&& ./configure --enable-optimizations \
&& make altinstall

RUN ln -s /usr/local/bin/python3.7 /usr/local/bin/python3 \
&& ln -s /usr/local/bin/pip3.7 /usr/local/bin/pip3 \
&& ln -s /usr/local/bin/python3.7 /usr/local/bin/python \
&& ln -s /usr/local/bin/pip3.7 /usr/local/bin/pip \
&& ln -s /usr/local/bin/pydoc3.7 /usr/local/bin/pydoc3 \
&& ln -s /usr/local/bin/python3.7m-config /usr/local/bin/python3-config \
&& ln -s /usr/local/bin/pydoc3.7 /usr/local/bin/pydoc \
&& ln -s /usr/local/bin/python3.7m-config /usr/local/bin/python-config

RUN pip3 install --upgrade pip setuptools wheel torch==1.4.0 torchvision==0.5.0 future==0.18.2 onnx==1.6.0 protobuf==3.11.3

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

ONBUILD COPY requirements.txt .
ONBUILD RUN pip3 install -r requirements.txt
ONBUILD COPY . /usr/src/app

