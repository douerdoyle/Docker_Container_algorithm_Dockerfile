FROM tiangolo/uwsgi-nginx-flask:python2.7

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

RUN apt-get install -y libprotobuf-dev \
						libleveldb-dev \
						libsnappy-dev \
						libopencv-dev \
						libhdf5-serial-dev \
						protobuf-compiler \
						libboost-all-dev \
						libatlas-base-dev \
						python-dev \
						libgflags-dev \
						libgoogle-glog-dev \
						liblmdb-dev
RUN cd / && \
	apt-get install -y git && \
	git clone https://github.com/BVLC/caffe.git
RUN apt-get install -y python-numpy \
						python-scipy \
						python-matplotlib \
						python-sklearn \
						python-skimage \
						python-h5py \
						python-protobuf \
						python-leveldb \
						python-networkx \
						python-nose \
						python-pandas \
						python-gflags \
						cython \
						ipython
COPY ./Makefile.config /caffe/
RUN cd /caffe/ && \
	make all
RUN apt-get install -y gfortran && \
	cd /caffe/python/ && \
	for req in $(cat requirements.txt); do pip install $req; done
RUN cd /caffe/ && \
	make pycaffe
RUN echo "export PYTHONPATH=\$PYTHONPATH:/caffe/python" >> ~/.bashrc
RUN pip install numpy scikit-image grpcio protobuf
RUN apt-get clean autoclean

COPY ./build/ /app