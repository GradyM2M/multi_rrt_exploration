# multi_rrt_exploration

This package is adapted from rrt_exploration. You could run the following command on the terminal:  
$ roslaunch multi_rrt_exploration rrt_three_robots.launch  

# real_robots_exploration  

导航:  
master: roscore  

robot_0: export ROS_NAMESPACE=robot_0  
robot_0: roslaunch rikirobot lidar_slam_multi.launch tf_prefix:=robot_0  

robot_1: export ROS_NAMESPACE=robot_1  
robot_1: roslaunch robot_navigation robot_slam_laser_multi.launch tf_prefix:=robot_1  

master: roslaunch multirobot_test robots_merge.launch  

探索:  
#robot_0: 配置 launch文件中加入 move_base explore_robot_0.launch 配置使用公共 /map 话题  
修改 move_base global_costmap_params.yaml 、local_costmap_params.yaml中坐标系  
master: roscore  
robot_0: export ROS_NAMESPACE=robot_0  
robot_0: roslaunch rikirobot lidar_slam_multi.launch tf_prefix:=robot_0  
master: roslaunch explore_lite explore.launch  
