# turtlebot_move_base_navigation_patrol_random
Sending random points continuously for Turtlebot3 move_base/goals on predefined area

## Requirements:

<ul>
  <li>ROS Noetic</li>
  <li>[Turtlebot3 PC Setup](https://emanual.robotis.com/docs/en/platform/turtlebot3/quick-start/#pc-setup)</li>
</ul> 

```bash
$sudo apt-get install ros-kinetic-joy ros-kinetic-teleop-twist-joy \
  ros-kinetic-teleop-twist-keyboard ros-kinetic-laser-proc \
  ros-kinetic-rgbd-launch ros-kinetic-depthimage-to-laserscan \
  ros-kinetic-rosserial-arduino ros-kinetic-rosserial-python \
  ros-kinetic-rosserial-server ros-kinetic-rosserial-client \
  ros-kinetic-rosserial-msgs ros-kinetic-amcl ros-kinetic-map-server \
  ros-kinetic-move-base ros-kinetic-urdf ros-kinetic-xacro \
  ros-kinetic-compressed-image-transport ros-kinetic-rqt* \
  ros-kinetic-gmapping ros-kinetic-navigation ros-kinetic-interactive-markers
$sudo apt install ros-noetic-dynamixel-sdk
$sudo apt install ros-noetic-turtlebot3-msgs
$sudo apt install ros-noetic-turtlebot3
```
## Setup
```bash
$cd ~/catkin_ws/src
$git clone https://github.com/hansenmaster/turtlebot_move_base_navigation_patrol_random
$cd ..
$catkin_make
$source devel/setup.bash
```

### Move base package:
Move base is a navigation stack package on ROS that receive predefined map by SLAM, robot information (transform, odometry, sensor reading), and goals to output /cmd_vel topics and costmap. On real robot, the cmd_vel will be converted by its controller using the SDK.

Subscribe to:
<ul>
  <li>/map (occupancy grid by SLAM)</li>
  <li>/tf /odom /scan (robot information and sensors reading) </li>
  <li>/move_base_simple/goals (goals for navigation) </li>
</ul> 

## Disclaimer

<ul>
  <li>The contribution of this repository is to continously sends /move_base_simple/goals by sending action. The SLAM map and all navigation stack are available from the Turtlebot3 repository. </li>
  <li>A bash script of auto pose initialization is also on the initial_pose.sh </li>
  <li>The package is based on https://github.com/FiorellaSibona/turtlebot3_nav/tree/devel/catkin_ws/src/simple_navigation_goals . Instead of doing patrol on predefined points, I made random points to showcase that move_base really works autonomously while doing obstacle avoidance. </li>
</ul> 

## Goals generation
![image](https://user-images.githubusercontent.com/36762228/172047213-cc0de060-2b59-4a7c-ba01-c123bda5271c.png)
The code will pick random area 1-4, then pick random coordinate inside the area.
The goals generation is repeated forever for each time action is finished means the current target is reached.

![image](https://user-images.githubusercontent.com/36762228/172049601-5aed9b4f-ae16-472c-9932-92eb0bfa181e.png)


## How to run
### Run Gazebo world simulation
```bash
$export TURTLEBOT3_MODEL=burger
$roslaunch turtlebot3_gazebo turtlebot3_world.launch
```
### Run Navigation
```bash
$export TURTLEBOT3_MODEL=burger
$roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/map.yaml (change dir to map.yaml location)
```

### Run pose initialization:
```bash
%sh initial_pose.sh 
```
This code is simply pub topic once at the spawn position of Gazebo world simulation. Then do rotation for 3 seconds to reduce the particle variance.

![image](https://user-images.githubusercontent.com/36762228/172047645-065b9ab4-9d2a-493c-85c6-be5990353e10.png)


### Run send_move_base_goals launchfile:
```bash
$roslaunch send_move_base_goals movebase_continuous.launch
```


https://user-images.githubusercontent.com/36762228/172050549-6df5b3a6-bcf0-416e-bd7f-fb40ed40da58.mp4



## Reference
https://github.com/FiorellaSibona/turtlebot3_nav/tree/devel/catkin_ws/src/simple_navigation_goals

