ARG FROM_IMAGE=osrf/ros:melodic-desktop-full
FROM $FROM_IMAGE

# 换源
RUN cp /etc/apt/sources.list /etc/apt/sources.list_backup \
    && rm /etc/apt/sources.list
COPY ./sources.list /etc/apt/

RUN apt-get update \
    && apt-get install -y python-catkin-tools \
    libeigen3-dev \
    libpcl-dev \
    liblapack-dev \
    libsuitesparse-dev \
    libcxsparse3 \
    libgflags-dev \
    libgoogle-glog-dev \
    libgtest-dev \
    qt5-qmake \
    qt5-default \
    libqglviewer-dev-qt5 \
    libcholmod3 \
    ros-melodic-serial \
    tree \
    ros-melodic-slam-gmapping \
    ros-melodic-velodyne \
    python-catkin-tools \
    ros-melodic-jsk-rviz-plugins \
    ros-melodic-plotjuggler-ros \
    ros-melodic-usb-cam \
    ros-melodic-laser-*  \
    ros-melodic-slam-gmapping \
    ros-melodic-vision-opencv \
    ros-melodic-depthimage-to-laserscan \
    ros-melodic-move-base \
    ros-melodic-map-server \
    ros-melodic-fake-localization \
    ros-melodic-robot-localization \
    ros-melodic-amcl  \
    ros-melodic-navigation \
    ros-melodic-gazebo-ros-pkgs \
    ros-melodic-gazebo-ros-control \
    ros-melodic-gazebo-plugins \
    ros-melodic-ros-controllers \
    ros-melodic-ros-control \ 
    ros-melodic-stage-ros \
    python-pip \
    && rm -rf /var/lib/apt/lists/*


RUN pip install pyserial \
    && pip install pyyaml \
    && pip install paho-mqtt \
    && pip install rospkg


WORKDIR /pkgs
RUN git clone  https://gitee.com/ebesin/gtsam.git \
    && cd gtsam/ \
    && mkdir build && cd build && cmake .. \
    && make && make install \
    && rm -rf /pkgs

WORKDIR /pkgs
RUN git clone https://gitee.com/ebesin/sophus.git \
    && cd sophus/ \
    && mkdir build && cd build && cmake .. \
    && make && make install \
    && rm -rf /pkgs

WORKDIR /pkgs
RUN git clone https://gitee.com/ebesin/ceres.git \
    && cd ceres/ \
    && mkdir build && cd build && cmake .. \
    && make && make install \
    && rm -rf /pkgs

WORKDIR /pkgs
RUN git clone https://gitee.com/ebesin/g2o.git \
    && cd g2o/ \
    && mkdir build && cd build && cmake .. \
    && make && make install \
    && rm -rf /pkgs

RUN echo "source /opt/ros/melodic/setup.bash" >> /root/.bashrc

WORKDIR /root/catkin_ws/
VOLUME [ "/root/data" ]
CMD [ "bash" ]