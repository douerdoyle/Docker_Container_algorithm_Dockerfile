FROM tiangolo/uwsgi-nginx-flask:python3.6

RUN apt-get update
RUN apt-get install -y \
        default-libmysqlclient-dev \
        libopenblas-base \
        python-numpy \
        python-scipy \
        python-h5py \
        python-yaml \
        python-pydot \
        unzip \
        libboost-all-dev \
        build-essential \
        cmake \
        libgtk-3-dev \
        libusb-1.0-0-dev
RUN apt-get clean

RUN pip install -U pip
RUN pip install --upgrade setuptools

WORKDIR /app/src

RUN pip install dlib

RUN apt-get install -y fftw3
RUN wget http://www.fftw.org/fftw-3.3.8.tar.gz && \
        tar zxvf fftw-3.3.8.tar.gz && \
        cd fftw-3.3.8 && \
        ./configure --enable-type-prefix --with-gcc --disable-fortran --enable-i386-hacks --enable-shared=yes && \
        make && \
        make install && \
        make clean && \
        ./configure --enable-float --enable-type-prefix --with-gcc --disable-fortran --enable-i386-hacks --enable-shared=yes && \
        make && \
        make install && \
        cd ../ && \
        rm -rf fftw-3.3.8 fftw-3.3.8.tar.gz
RUN cd /app/src/
RUN pip install aihub
COPY ./build/ /app