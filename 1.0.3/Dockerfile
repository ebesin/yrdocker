ARG FROM_IMAGE=ros:melodic
FROM $FROM_IMAGE

# clone ros package
WORKDIR /ros/catkin_ws/
VOLUME [ "/ros/data" ]
COPY catkin_ws/src ./src

# install build tools
RUN apt-get update \
    && apt-get install -y python-catkin-tools \
    && rm -rf /var/lib/apt/lists/*

# install ros package dependencies
RUN apt-get update \
    && rosdep install -y --from-paths src \
    && rm -rf /var/lib/apt/lists/*

# build ros package source
RUN apt-get update \
    && /bin/bash -c "source /opt/ros/melodic/setup.bash;catkin_make" \
    && rm -rf /var/lib/apt/lists/* 

# some other settings
RUN echo "source /opt/ros/melodic/setup.bash" >> /root/.bashrc \
    && echo "source /ros/catkin_ws/devel/setup.bash" >> /root/.bashrc

CMD [ "bash" ]