# Copyright 2019 The TensorFlow Authors. All Rights Reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
# ============================================================================
#
# THIS IS A GENERATED DOCKERFILE.
#
# This file was assembled from multiple pieces, whose use is documented
# throughout. Please refer to the TensorFlow dockerfiles documentation
# for more information.

# this is a static copy of the tensorflow dockerfile that I have heavily modified

ARG UBUNTU_VERSION=18.04

ARG ARCH=
ARG CUDA=10.1
FROM nvidia/cuda${ARCH:+-$ARCH}:${CUDA}-cudnn7-devel-ubuntu${UBUNTU_VERSION} as devel
# ARCH and CUDA are specified again because the FROM directive resets ARGs
# (but their default value is retained if set previously)
#ARG ARCH
ARG CUDA
#ARG CUDNN=7.6.4.38-1
#ARG CUDNN_MAJOR_VERSION=7
ARG LIB_DIR_PREFIX=x86_64
#ARG LIBNVINFER=6.0.1-1
#ARG LIBNVINFER_MAJOR_VERSION=6
ENV cvVersion="4.2.0"

# setup environment
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8

# Needed for string substitution
SHELL ["/bin/bash", "-c"]

# setup timezone
RUN echo 'Etc/UTC' > /etc/timezone && \
    ln -s /usr/share/zoneinfo/Etc/UTC /etc/localtime && \
    apt-get update && apt-get install -q -y tzdata

RUN apt-get install -y --no-install-recommends \
    build-essential \
    curl \
    openjdk-8-jdk \
    swig \
    netbase \
    wget \
    git \
    # cuda-command-line-tools-${CUDA/./-} \
    # # There appears to be a regression in libcublas10=10.2.2.89-1 which
    # # prevents cublas from initializing in TF. See
    # # https://github.com/tensorflow/tensorflow/issues/9489#issuecomment-562394257
    # libcublas10=10.2.1.243-1 \ 
    # libcublas-dev=10.2.1.243-1 \
    # cuda-nvrtc-${CUDA/./-} \
    # cuda-nvrtc-dev-${CUDA/./-} \
    # cuda-cudart-dev-${CUDA/./-} \
    # cuda-cufft-dev-${CUDA/./-} \
    # cuda-curand-dev-${CUDA/./-} \
    # cuda-cusolver-dev-${CUDA/./-} \
    # cuda-cusparse-dev-${CUDA/./-} \
    # libcudnn7=${CUDNN}+cuda${CUDA} \
    # libcudnn7-dev=${CUDNN}+cuda${CUDA} \
    libcurl3-dev \
    libfreetype6-dev \
    libhdf5-serial-dev \
    libzmq3-dev \
    libsm6 libxext6 libxrender1 libfontconfig1 \
    pkg-config \
    rsync \
    software-properties-common \
    unzip \
    zip \
    zlib1g-dev \
    wget \
    git \
    vim \
    ca-certificates \
    libfltk1.3-dev \
    fluid \
    libgl1-mesa-dev \
    doxygen \
    vim \
    less \
    gettext-base \
    netbase \
    iputils-ping \
    ninja-build \
    libeigen3-dev \
    debconf-utils \
    dirmngr \
    gnupg2 \
    python3 \
    python3-pip \
    python3-dev \
    virtualenv \
    python3-tk \
    gfortran \
    libjpeg8-dev \
    libpng-dev \
    libtiff5-dev \
    libtiff-dev \
    libavcodec-dev \
    libavformat-dev \
    libswscale-dev \
    libdc1394-22-dev \
    libxine2-dev \
    libv4l-dev \
	libgstreamer1.0-dev \
	libgstreamer-plugins-base1.0-dev \
	libgtk2.0-dev \
	libtbb-dev \
	qt5-default \
	libatlas-base-dev \
	libfaac-dev \
	libmp3lame-dev \
	libtheora-dev \
	libvorbis-dev \
	libxvidcore-dev \
	libopencore-amrnb-dev \
	libopencore-amrwb-dev \
	libavresample-dev \
	x264 \
	v4l-utils \
	libprotobuf-dev \
	protobuf-compiler \
	libgoogle-glog-dev \
	libgflags-dev \
	libgphoto2-dev \
	libeigen3-dev \
	libhdf5-dev \
	doxygen && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    find /usr/local/cuda-${CUDA}/lib64/ -type f -name 'lib*_static.a' -not -name 'libcudart_static.a' -delete && \
    rm /usr/lib/${LIB_DIR_PREFIX}-linux-gnu/libcudnn_static_v7.a




RUN apt-get update && apt-get install -y --no-install-recommends \
    python-virtualenv \
    ccache  \
    libopenblas-dev \
    liblapacke-dev \
    libjpeg-dev \
    libeigen-stl-containers-dev \
    zlib1g \
    libatlas3-base \
    libvtk6-jni \
    libvtk6.3 \
    libvtk6-dev \ 
    libvtk6-java \
    libopenjp2-tools \
    libgtkglext1-dev \
    libceres-dev \
    libcaffe-cuda-dev \
    libleptonica-dev \
    coinor-libclp-dev \
    libtesseract-dev \
    tesseract-ocr \
    libogre-1.9-dev \ 
    ogre-1.9-tools \
    ocl-icd-opencl-dev \
    ocl-icd-libopencl1 \
    opencl-headers \
    clinfo \
    ocl-icd-dev \
    hdf5-tools \
    pybind11-dev \
    python-dev \
    python-pip \
    gdb \
    tmux \ 
    sudo \
    libuv1-dev \
    libssl-dev 

ARG USERNAME=vscode
ARG USER_UID=262
ARG USER_GID=818

# Create the non-root user - see https://aka.ms/vscode-remote/containers/non-root-user.
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
    # [Optional] Add sudo support for non-root user
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

RUN mkdir -p /opt/venv_py2 && chmod a+rwx /opt/venv_py2
RUN mkdir -p /opt/venv_py3 && chmod a+rwx /opt/venv_py3

USER vscode

ENV VIRTUAL_ENV=/opt/venv_py3
RUN /usr/bin/python3 -m virtualenv --python=/usr/bin/python3 $VIRTUAL_ENV
ENV PATH="$VIRTUAL_ENV/bin:$PATH"

ENV VIRTUAL_ENV=/opt/venv_py2
RUN /usr/bin/python -m virtualenv --python=/usr/bin/python $VIRTUAL_ENV
ENV PATH="$VIRTUAL_ENV/bin:$PATH"


#RUN cd /usr/include/linux && \
#RUN	ln -s -f /usr/include/libv4l1-videodev.h /usr/include/linuxvideodev.h

RUN pip3 --no-cache-dir install --upgrade \
    pip \
    setuptools \
    ipython \
    numpy \
    scipy \
    pybind11 \
    pygame \
    vtk \
    matplotlib 

RUN pip3 --no-cache-dir install --upgrade \
    pyqt5 \
    pyside2 \ 
    pytesseract \
    tesserocr \
    jupyter \
    gnupg \
    pyopencl \
    argcomplete

USER root

RUN ln -s /usr/include/x86_64-linux-gnu/cblas.h /usr/include/cblas.h

RUN update-alternatives --install /usr/bin/vtk vtk /usr/bin/vtk6 10

# install a newer version of cmake
RUN mkdir /cmake \
    && cd /cmake \
    && wget https://github.com/Kitware/CMake/releases/download/v3.15.5/cmake-3.15.5-Linux-x86_64.sh \
    && chmod +x cmake-3.15.5-Linux-x86_64.sh \
    && ./cmake-3.15.5-Linux-x86_64.sh --prefix=/usr/local --skip-license 

RUN git clone https://github.com/opencv/opencv.git && \
	cd opencv && \
	git checkout $cvVersion && \
	cd ..

RUN git clone https://github.com/opencv/opencv_contrib.git && \
	cd opencv_contrib && \
	git checkout $cvVersion && \
	cd ..

RUN git clone https://github.com/opencv/opencv_extra.git && \
	cd opencv_extra && \
	git checkout $cvVersion && \
	cd ..

USER vscode

RUN /opt/venv_py2/bin/pip --no-cache-dir install --upgrade \
    pip \
    setuptools \
    numpy \
    scipy \
    matplotlib \
    vtk

USER root

RUN cd opencv && \
	mkdir build && \
	cd build && \
	cmake \
    -DCMAKE_BUILD_TYPE=RELEASE \
	-DCMAKE_INSTALL_PREFIX=/usr/local \
    -DWITH_CUDA=ON \
    -DENABLE_FAST_MATH=1 \
    -DCUDA_FAST_MATH=1 \
    -DWITH_CUBLAS=1 \
	-DINSTALL_C_EXAMPLES=OFF \
    -DINSTALL_PYTHON_EXAMPLES=OFF \
    -DENABLE_PRECOMPILED_HEADERS=OFF \
    -DWITH_OPENMP=ON \
    -DWITH_NVCUVID=ON \
    -DBUILD_opencv_cudacodec=OFF \
    -DPYTHON_DEFAULT_EXECUTABLE=$(which python3) \
    -DBUILD_USE_SYMLINKS=ON \
    -DBUILD_PERF_TESTS=OFF \
    -DBUILD_TESTS=OFF \
    -DBUILD_JAVA=OFF \
    -DBUILD_PROTOBUF=ON \
    -DBUILD_opencv_java_bindings_gen=OFF \
    -DBUILD_opencv_cnn_3dobj=OFF \
    -DWITH_GDAL=ON \
    -DWITH_CLP=ON \
    -DTesseract_INCLUDE_DIR=/usr/include/tesseract \
    -DTesseract_LIBRARY=/usr/lib/x86_64-linux-gnu/libtesseract.so \
    -DOpenBLAS_LIB=/usr/lib/x86_64-linux-gnu/openblas/libblas.so \
    -DWITH_TBB=ON \
    -DOpenGL_GL_PREFERENCE=GLVND \
    -DCUDA_ARCH_BIN=6.1 \
    -DCUDA_TOOLKIT_ROOT_DIR=/usr/local/cuda-10.1 \
    -DWITH_OPENGL=ON \
    -DWITH_VULKAN=ON \
    -DPYTHON3_INCLUDE_DIR2=~/.local/include/python3.6m \
	-DOPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules \
	-DBUILD_EXAMPLES=OFF .. && \
    cmake -DOPENCV_PYTHON3_VERSION=ON .. && \
    make -j$(nproc) && make install && \
	cd ..

# Configure the build for our CUDA configuration.
ENV LD_LIBRARY_PATH /usr/local/cuda/extras/CUPTI/lib64:/usr/local/cuda/lib64:/usr/local/cuda/lib64/stubs:/usr/include/x64_64-linux-gnu:$LD_LIBRARY_PATH


RUN add-apt-repository ppa:ubuntu-toolchain-r/test && \
    apt -y install gcc-10 g++-10 && \
    update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-10 90 --slave /usr/bin/g++ g++ /usr/bin/g++-10 --slave /usr/bin/gcov gcov /usr/bin/gcov-10

# RUN ln -s /usr/local/cuda/lib64/stubs/libcuda.so /usr/local/cuda/lib64/stubs/libcuda.so.1 \
#     && echo "/usr/local/cuda/lib64/stubs" > /etc/ld.so.conf.d/z-cuda-stubs.conf \
#     && ldconfig

# # # Some TF tools expect a "python" binary
# # RUN ln -s $(which python3) /usr/local/bin/python


# setup keys
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654

# setup sources.list
RUN echo "deb http://packages.ros.org/ros/ubuntu bionic main" > /etc/apt/sources.list.d/ros1-latest.list

# setup entrypoint
COPY ./.devcontainer/ros_entrypoint.sh /

#ENV ROS_DISTRO melodic
ENV ROS_DISTRO melodic

# install ros packages
RUN apt-get update && apt-get install -y --no-install-recommends \
    ros-melodic-ros-core=1.4.1-0* \
    python-rosdep \
    python-rosinstall \
    python-vcstools \
    && rm -rf /var/lib/apt/lists/*

# bootstrap rosdep
RUN rosdep init 

USER vscode

RUN rosdep update --rosdistro $ROS_DISTRO

USER root

# install ros packages
RUN apt-get update && apt-get install -y --no-install-recommends \
    ros-melodic-ros-base=1.4.1-0* \
    ros-melodic-robot=1.4.1-0* \
    ros-melodic-desktop=1.4.1-0* \
    ros-melodic-desktop-full=1.4.1-0* \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir /uWebSockets && \
    pushd /uWebSockets && \
    git clone https://github.com/uWebSockets/uWebSockets . && \
    git checkout e94b6e1 && \
    mkdir build && \
    cd build && \
    cmake .. && \
    make -j$(nproc) && \
    make install && \
    ln -s /usr/lib64/libuWS.so /usr/lib/libuWS.so && \
    popd && \
    rm -rf /uWebSockets

#WORKDIR /workspaces/mpath
EXPOSE 8888

ENV PYTHONPATH=/usr/lib/python2.7/dist-packages:$PYTHONPATH

ENTRYPOINT ["/ros_entrypoint.sh"]

COPY .devcontainer/bashrc /home/vscode/.bashrc
COPY .devcontainer/.tmux.conf /home/vscode/
RUN chmod a+rwx /home/vscode/.bashrc
RUN chmod a+rwx /home/vscode/.tmux.conf
RUN chmod a+rwx /ros_entrypoint.sh

CMD ["bash", "-c", "source /etc/bash.bashrc"]
