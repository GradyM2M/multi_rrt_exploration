# multi_rrt_exploration

This package is adapted from rrt_exploration. You could run the following command on the terminal:  
$ roslaunch multi_rrt_exploration rrt_three_robots.launch   

#### 介绍
该功能包改编于GitHub上的开源项目[rrt_exploration](https://github.com/hasauino/rrt_exploration)，笔者已在ROS melodic下跑通（采用三台turtlebot3机器人测试），整体来看，该项目中所使用的RRT算法扩展性与稳定性较好，在计算机算力允许的范围内，能够扩展至更多的机器人数量。

#### 软件依赖
要在ROS melodic上成功运行该功能包并非一件容易的事，笔者花费了整整１个周才将其从ROS kinetic成功移植到ROS melodic中，所需依赖如下：
1. 地图融合：[m-explore](https://github.com/hrnr/m-explore)
2. 探索插件：[frontier_exploration](https://github.com/paulbovbel/frontier_exploration)
3. 机器人模型：[turtlebot3](https://github.com/ROBOTIS-GIT/turtlebot3)
4. [turtlebot3_msgs](https://github.com/ROBOTIS-GIT/turtlebot3_msgs)

#### 使用说明
1. 仿真:  
$ roslaunch multi_rrt_exploration rrt_three_robots.launch  

2. 实物（导航）:  
master: roscore  

robot_0: export ROS_NAMESPACE=robot_0  
robot_0: roslaunch rikirobot lidar_slam_multi.launch tf_prefix:=robot_0  

robot_1: export ROS_NAMESPACE=robot_1  
robot_1: roslaunch robot_navigation robot_slam_laser_multi.launch tf_prefix:=robot_1  

master: roslaunch multirobot_test robots_merge.launch  

3. 实物（探索）:  
master: roslaunch multirobot_test robots_merge.launch  
robot_: export ROS_NAMESPACE=robot_  
robot_: roslaunch rikirobot lidar_slam_multi.launch tf_prefix:=robot_  
master: roslaunch explore_lite explore.launch  

4. 修改说明:  
robot_: 配置 launch文件中加入 move_base explore_robot_.launch 配置使用公共 /map 话题  
修改 move_base global_costmap_params.yaml 、local_costmap_params.yaml中坐标系  
