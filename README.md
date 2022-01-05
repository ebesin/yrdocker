# yrdocker
## 简介
为跃然创客创建的docker镜像，集成了跃然创客项目运行所需要的所有环境及依赖。
## 使用方式
- **最佳实践**

    - 本实验室的项目会用到`rviz`工具，因此在容器中最好能有可视化的功能。由于`linux`中的界面服务为`c/s`架构的，只需要在宿主机中配置好`xserver`服务允许容器中的客户端访问即可。

      1. 在宿主机中输入以下命令

         ```bash
         $ sudo apt install x11-xserver-utils	#安装xserver-utils工具
         
         $ xhost +	#允许所有客户端访问xserver服务
         ```

      2. 启动容器时挂载相关目录及配置环境变量

         - 启动时需要添加如下参数：

           ```bash
           -v /tmp/.X11-unix:/tmp/.X11-unix
           -e DISPLAY=$DISPLAY
           ```

         - 示例：

           ```bash
           docker run -dit --name yrtest \
           -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY \
           ebesin/yrdocker:1.0.3 bash
           ```

          上述命令启动了一个以`ebesin/yrdocker:1.0.3`镜像为基础层的容器，并能在容器中支持可视化展示。

    - 创建容器时最好将工作空间挂载到`/ros/catkin_ws`目录下：

      ```bash
      docker run -dit --name yrtest \
      -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY \
      --mount type=bind,source=/home/amov/dwayne/catkin_ws,target=/ros/catkin_ws \
      ebesin/yrdocker:1.0.3 bash
      ```

      该命令将宿主机中工作空间下的源文件挂载到了`ros/catkin_ws`目录，这样，在启动容器后可以直接编译源文件。

    - 容器运行时产生一些程序结果数据一定要保存在`/ros/data`目录下，这样才是持久化保存的，保存到其他位置的话在容器删除时，数据也会丢失！。

    - 运行实例：

      ```bash
      # 启动容器
      amov@yr:~$ docker run -dit --name yrtest \
      > -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY -v /etc/localtime:/etc/localtime:ro --privileged\
      > --mount type=bind,source=/home/amov/dwayne/catkin_ws,target=/ros/catkin_ws \
      > ebesin/yrdocker:1.0.4 bash
      e93361012c35a56e9be4887fe57abc49d054049166a3ae8561feedb83a2481e8
      
      # 进入容器，并编译代码
      root@e93361012c35:/ros/catkin_ws# catkin_make
      Base path: /ros/catkin_ws
      Source space: /ros/catkin_ws/src
      Build space: /ros/catkin_ws/build
      Devel space: /ros/catkin_ws/devel
      Install space: /ros/catkin_ws/install
      ####
      ......
      
      # 这样代码就编译完成，接下来source一下，就可以直接执行对应的程序了
      ```

    
