# yrdocker

## 使用`yrdocker`镜像

#### 准备工作

1. 在宿主机中配置，输入以下命令

   ```bash
   $ sudo apt install x11-xserver-utils	#安装xserver-utils工具
   
   $ xhost +	#允许所有客户端访问xserver服务
   ```

2. 拉取镜像到本地

   ```bash
   $ docker pull ebesin/yrdocker:1.0.5
   ```

#### 使用镜像

1. 以`yrdocker`镜像为基础层启动容器

   ```bash
   $ docker run -dit --name yrdocker \
   -v /tmp/.X11-unix:/tmp/.X11-unix -v /etc/localtime:/etc/localtime:ro \
   --privileged -e DISPLAY=$DISPLAY -p 9091:9091 -P\
   --mount type=bind,source=/home/dwayne/workspace/src,target=/ros/catkin_ws/src \
   ebesin/yrdocker:1.0.5
   ```

   - 参数解释

     - `-dit`参数对应的完整参数是`-d -i -t`：后台运行容器，并且容器会被分配终端。

     - `--name yrtest`参数：为容器设置名字为`yrtest`

     - `-v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY`:挂载与显示输出相关的目录

     - `--mount type=bind,source=/home/amov/dwayne/catkin_ws/src,target=/ros/catkin_ws/src`:将宿主机中的原代码目录挂载到容器中，使用时需要将`/home/amov/dwayne/catkin_ws/src`替换为自己电脑中的src目录。该行也可以写为

       `-v /home/amov/dwayne/catkin_ws/src:/ros/catkin_ws/src`

     - `ebesin/yrdocker:1.0.5:`指定要基于哪个镜像创建容器，本例中为`ebesin/yrdocker:1.0.5`

   启动成功后应该会返回该容器的`ID`

2. 进入容器

   ```bash
   $ docker exec -it yrtest bash
   ```

   - 参数解释
     - `-it`:与`docker run`命令的参数含义一样
     - `yrtest`:要进入的容器名，也可以替换为容器`ID`
     - `bash`:进入容器所运行的进程，这里就写`bash`就好

3. 在容器中操作

   进入容器后就可以和正常的ubuntu电脑一样操作了，进入容器后的默认目录为`/ros/catkin_ws`，可以直接运行`catkin_make`命令进行编译。

#### 一些注意事项

- 在创建镜像时设置了默认的工作空间为`/ros/catkin_ws`，所以最好将宿主机中的工作区下的源码目录挂载到该目录下，就如上面的例子所示。
- **\*在容器里面运行代码时，如果有需要保存的运行时数据，一定要保存在`/ros/data`目录下，因为容器运行时产生的数据不是持久化的，如果不保存在该目录下，在容器删除时数据也会丢失！**
