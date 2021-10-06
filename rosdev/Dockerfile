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
    && rm -rf /var/lib/apt/lists/*

# some other settings
RUN echo "source /opt/ros/melodic/setup.bash" >> /root/.bashrc

CMD [ "bash" ]