ARG FROM_IMAGE=ebesin/yrdocker:1.0.4
FROM $FROM_IMAGE

RUN rm /usr/local/lib/libfontconfig.so.1 \
    && ln -s /lib/x86_64-linux-gnu/libfontconfig.so.1 /usr/local/lib/libfontconfig.so.1


WORKDIR /ros/catkin_ws/

CMD [ "bash" ]