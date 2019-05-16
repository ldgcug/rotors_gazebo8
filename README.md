# rotors_gazebo8
u16 + ros kinetic + gazebo8安装文档  

## 操作系统：ubuntu16.04  
## ROS：kinetic  
## Gazebo：8.6

## 安装步骤：  
### 1.安装Gazbeo8环境  
    (1)添加sources.list  
    sudo sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-stable `lsb_release -cs` main" > /etc/apt/sources.list.d/gazebo-stable.list'
    (2)添加key
    wget http://packages.osrfoundation.org/gazebo.key -O - | sudo apt-key add -
    (3)更新软件
    sudo apt-get update
    (4)安装gazebo8
    sudo apt-get install gazebo8
    sudo apt-get install libgazebo8-dev
### 2.安装ros kinetic（不安装full版）  
    (1)添加sources.list
    sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
    (2)添加key
    sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
    (3)更新软件
    sudo apt-get update
    (4)安装ros-kinetic-desktop 及其他相关ros包
    sudo apt-get install ros-kinetic-desktop ros-kinetic-joy ros-kinetic-octomap-ros 
    ros-kinetic-mavlink python-wstool python-catkin-tools protobuf-compiler 
    libgoogle-glog-dev ros-kinetic-control-toolbox
    (5)初始化rosdep
    sudo rosdep init
    rosdep update
    (6)环境变量配置
    echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
    source ~/.bashrc
    (7)安装rosinstall
    sudo apt-get install python-rosinstall python-rosinstall-generator python-wstool build-essential  
    
### 3.安装相关ros包 和其他python库
    (1)安装ros包
    sudo apt-get install ros-kinetic-ardrone-autonomy
    sudo apt-get install ros-kinetic-gazebo8-msgs
    sudo apt-get install ros-kinetic-gazebo8-ros-control
    sudo apt-get install ros-kinetic-gazebo8-plugins
    sudo apt-get install ros-kinetic-gazebo8-ros-pkgs
    sudo apt-get install ros-kinetic-gazebo8-ros
    sudo apt-get install ros-kinetic-image-view  
    
    sudo apt-get install libgeographic-dev ros-kinetic-geographic-msgs
    sudo apt-get install ros-kinetic-tf2-eigen
    sudo apt-get install ros-kinetic-mavros
    
    （2）安装python库
    sudo apt-get install python-pip
    pip install future
    
### 4.搭建仿真环境
    （1）创建工作空间
    mkdir -p ~/catkin_ws/src
    
    （2）clone文件
    cd 
    git clone https://github.com/ldgcug/rotors_gazebo8.git
    
    （3）将下载的文件加拷贝到~/catkin_ws/src目录下（主要为：mav_comm、mavlink、mavros、rotors_simulator）
    
    （4）编译环境
    cd ~/catkin_ws
    catkin build
    
    （5）添加源到.bashrc文件
    echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
    source ~/.bashrc
    source ~/catkin_ws/devel/setup.bash

### 5.运行仿真环境
    (1)启动launch文件，打开gazebo仿真世界模型
    cd catkin_ws
    source devel/setup.bash
    roslaunch rotors_gazebo mav_hovering_example_with_vi_sensor.launch mav_name:=iris  world_name:=basic

启动后，界面如下：  

![gazebo.png](https://github.com/ldgcug/rotors_gazebo8/raw/master/rotors.png)
