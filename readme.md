# multi_rrt_exploration

This package is adapted from rrt_exploration. You could run the following command on the terminal:  
```sh
$ roslaunch multi_rrt_exploration rrt_three_robots.launch
```

#### 介绍
该功能包改编于GitHub上的开源项目[rrt_exploration](https://github.com/hasauino/rrt_exploration)，笔者已在ROS melodic下跑通（采用三台turtlebot3机器人测试），整体来看，该项目中所使用的RRT算法扩展性与稳定性较好，在计算机算力允许的范围内，能够扩展至更多的机器人数量。

#### 软件依赖
要在ROS melodic上成功运行该功能包并非一件容易的事，笔者花费了整整１个周才将其从ROS kinetic成功移植到ROS melodic中，所需依赖如下：
1. 地图融合：[m-explore](https://github.com/hrnr/m-explore)
2. 探索插件：[frontier_exploration](https://github.com/paulbovbel/frontier_exploration)
3. 机器人模型：[turtlebot3](https://github.com/ROBOTIS-GIT/turtlebot3)
4. [turtlebot3_msgs](https://github.com/ROBOTIS-GIT/turtlebot3_msgs)
5. python库：OpenCV、Numpy、Sklearn

```sh
$ sudo apt-get install python-opencv
$ sudo apt-get install python-numpy
$ sudo apt-get install python-scikits-learn
```

#### 使用说明
1. 仿真:  
```sh
$ roslaunch multi_rrt_exploration rrt_three_robots.launch
```

2. 实物（导航）:  
```sh
master: roscore
robot_0: export ROS_NAMESPACE=robot_0
robot_0: roslaunch rikirobot lidar_slam_multi.launch tf_prefix:=robot_0
robot_1: export ROS_NAMESPACE=robot_1
robot_1: roslaunch robot_navigation robot_slam_laser_multi.launch tf_prefix:=robot_1
master: roslaunch multirobot_test robots_merge.launch
```  

3. 实物（探索）:  
```sh  
master: roslaunch multirobot_test robots_merge.launch
robot_: export ROS_NAMESPACE=robot_
robot_: roslaunch rikirobot lidar_slam_multi.launch tf_prefix:=robot_
master: roslaunch explore_lite explore.launch
```
  ### 修改说明: 
  1. robot_: 配置 launch文件中加入 move_base explore_robot_.launch 配置使用公共 /map 话题
  2. 修改 move_base global_costmap_params.yaml 、local_costmap_params.yaml中坐标系

## 部分实验结果：

#### 多机器人协同探索实验

<img src="https://github.com/GradyM2M/mobile_manipulator/blob/melodic-devel/%E4%BB%BF%E7%9C%9F-%E6%A0%B7%E6%9C%BA%E5%AE%9E%E9%AA%8C/1.%E5%A4%9A%E6%9C%BA%E5%99%A8%E4%BA%BA%E5%8D%8F%E5%90%8C%E6%8E%A2%E7%B4%A2%E5%AE%9E%E9%AA%8C/%E4%BB%BF%E7%9C%9F%E5%9C%BA%E6%99%AF3/Screenshot%20from%202021-08-31%2019-28-45.png" width="1000">
<img src="https://github.com/GradyM2M/mobile_manipulator/blob/melodic-devel/%E4%BB%BF%E7%9C%9F-%E6%A0%B7%E6%9C%BA%E5%AE%9E%E9%AA%8C/1.%E5%A4%9A%E6%9C%BA%E5%99%A8%E4%BA%BA%E5%8D%8F%E5%90%8C%E6%8E%A2%E7%B4%A2%E5%AE%9E%E9%AA%8C/%E4%BB%BF%E7%9C%9F%E5%9C%BA%E6%99%AF3/Screenshot%20from%202021-08-31%2018-38-55.png" width="1000">
