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

RUN pip install dlib aihub Keras tensorflow
COPY ./build/ /app
