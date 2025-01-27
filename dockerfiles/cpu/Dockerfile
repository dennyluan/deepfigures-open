# image for running DeepFigures

FROM tensorflow/tensorflow:1.5.1-py3
# FROM tensorflow/tensorflow:latest-py3

ENV LC_ALL C.UTF-8


# Set timezone to avoid docker from asking timezone and getting stuck.
ENV TZ=Europe/Minsk
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Install lib-jasper
RUN apt-get update
RUN apt-get install -y software-properties-common
RUN add-apt-repository "deb http://security.ubuntu.com/ubuntu xenial-security main"
RUN apt-get update
RUN apt-get install -y libjasper1 libjasper-dev

# install system packages

RUN apt-get clean \
 && apt-get update --fix-missing \
 && apt-get install -y \
    git \
    curl \
    gcc \
    build-essential \
    tcl \
    g++ \
    zlib1g-dev \
    libjpeg8-dev \
    libtiff5-dev \
    libjasper-dev \
    libpng12-dev \
    tcl-dev \
    tk-dev \
    python3 \
    python3-pip \
    python3-tk \
    ghostscript \
    openjdk-8-jre \
    poppler-utils \
    texlive-latex-base \
    texlive-fonts-recommended \
    texlive-fonts-extra \
    texlive-latex-extra

WORKDIR /work

# install python packages

ADD ./requirements.txt /work

RUN pip3 install --upgrade pip \
 && pip install Cython==0.25.2
RUN pip3 install --no-use-pep517 -r ./requirements.txt

ADD ./vendor/tensorboxresnet /work/vendor/tensorboxresnet
RUN pip3 install --no-use-pep517 -e /work/vendor/tensorboxresnet

ADD . /work
RUN pip3 install --quiet -e /work

CMD [ "/bin/bash" ]
