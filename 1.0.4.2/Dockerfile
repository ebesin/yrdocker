ARG FROM_IMAGE=ebesin/yrdocker:1.0.3
FROM $FROM_IMAGE

RUN apt-get update

#install OpenCV
WORKDIR /pkgs
COPY ./opencv-3.4.10 ./opencv-3.4.10
RUN cd opencv-3.4.10/ \
    && mkdir build && cd build && cmake .. \
    && make && make install

#install Gtsam4.0.2
WORKDIR /pkgs
COPY ./gtsam-4.0.2 ./gtsam-4.0.2
RUN cd gtsam-4.0.2/ \
    && mkdir build && cd build && cmake .. \
    && make && make install

#install Eigen and PCL
RUN apt-get install -y libeigen3-dev \
    && apt-get install -y libpcl-dev 

#install Sophus
WORKDIR /pkgs
COPY ./Sophus ./Sophus
RUN cd Sophus/ \
    && mkdir build && cd build && cmake .. \
    && make && make install

COPY ./sources.list /

RUN cp /etc/apt/sources.list /etc/apt/sources.list_backup \
    && rm /etc/apt/sources.list \
    && mv /sources.list /etc/apt/ \
    && apt-get update


#install dependences of g2o and Ceres
RUN apt-get install -y liblapack-dev \
    libsuitesparse-dev \
    libcxsparse3 \
    libgflags-dev \
    libgoogle-glog-dev \
    libgtest-dev \
    qt5-qmake \
    qt5-default \
    libqglviewer-dev-qt5 \
    libcholmod3


#install ceres
WORKDIR /pkgs
COPY ./ceres-solver ./ceres-solver
RUN cd ceres-solver/ \
    && mkdir build && cd build && cmake .. \
    && make && make install

#install g2o
WORKDIR /pkgs
COPY ./g2o ./g2o
RUN cd g2o/ \
    && mkdir build && cd build && cmake .. \
    && make && make install

# #install miniconda
# WORKDIR /pkgs/miniconda
# COPY Miniconda3-py37_4.10.3-Linux-x86_64.sh .
# RUN chmod +x Miniconda3-py37_4.10.3-Linux-x86_64.sh \
#     && bash Miniconda3-py37_4.10.3-Linux-x86_64.sh -bfp /usr/local

# #设置conda环境变量
# ENV PATH /opt/conda/bin:$PATH

# #初始化conda
# RUN conda init

#remove files
RUN rm -rf /pkgs

#install pkgs
RUN apt-get install -y ros-melodic-serial \
    tree \
    ros-melodic-slam-gmapping \
    ros-melodic-velodyne \
    python-catkin-tools \
    ros-melodic-jsk-rviz-plugins \
    ros-melodic-plotjuggler-ros \
    && pip install --upgrade pip \
    && pip install pyyaml \
    && pip install paho-mqtt \
    && pip install rospkg


# RUN apt-get install 
# RUN pip3 install torch==1.10.0+cpu \
#     torchvision==0.11.1+cpu \
#     torchaudio==0.10.0+cpu \
#     -f https://download.pytorch.org/whl/cpu/torch_stable.html




WORKDIR /ros/catkin_ws/

CMD [ "bash" ]