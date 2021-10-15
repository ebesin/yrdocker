ARG FROM_IMAGE=ros:melodic
FROM $FROM_IMAGE

WORKDIR /ros/catkin_ws/
VOLUME [ "/ros/data" ]

# install build tools
RUN apt-get update \
    && apt-get install -y python-catkin-tools \
    && rm -rf /var/lib/apt/lists/*

# install ros packages
RUN apt-get update \
    && apt-get install -y ros-melodic-rosbridge-server \
    && apt-get install -y libasio-dev \
    && apt-get install -y ros-melodic-teleop-twist-keyboard \
    && apt install -y libasio-dev \
    && apt-get install -y ros-melodic-move-base-msgs \
    && apt-get install -y ros-melodic-joint-state-publisher-gui \
    && apt-get install -y python-pip \
    && pip install --upgrade pip \
    && pip install  PySide2 \
    && rm -rf /var/lib/apt/lists/*


# some other settings
RUN echo "source /opt/ros/melodic/setup.bash" >> /root/.bashrc

CMD [ "bash" ]