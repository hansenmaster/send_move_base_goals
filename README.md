# turtlebot_move_base_navigation_patrol_random
Sending random points continuously for Turtlebot3 move_base/goals on predefined area

## Requirements:

<ul>
  <li>ROS Noetic</li>
  <li>[Turtlebot3 PC Setup](https://emanual.robotis.com/docs/en/platform/turtlebot3/quick-start/#pc-setup)</li>
</ul> 

```bash
sudo apt-get install ros-kinetic-joy ros-kinetic-teleop-twist-joy \
  ros-kinetic-teleop-twist-keyboard ros-kinetic-laser-proc \
  ros-kinetic-rgbd-launch ros-kinetic-depthimage-to-laserscan \
  ros-kinetic-rosserial-arduino ros-kinetic-rosserial-python \
  ros-kinetic-rosserial-server ros-kinetic-rosserial-client \
  ros-kinetic-rosserial-msgs ros-kinetic-amcl ros-kinetic-map-server \
  ros-kinetic-move-base ros-kinetic-urdf ros-kinetic-xacro \
  ros-kinetic-compressed-image-transport ros-kinetic-rqt* \
  ros-kinetic-gmapping ros-kinetic-navigation ros-kinetic-interactive-markers
sudo apt install ros-noetic-dynamixel-sdk
sudo apt install ros-noetic-turtlebot3-msgs
sudo apt install ros-noetic-turtlebot3
```

## Explanation
Move base is a navigation stack package on ROS that receive predefined map by SLAM, robot information (transform, odometry, sensor reading), and goals to output /cmd_vel topics and costmap. On real robot, the cmd_vel will be converted by its controller using the SDK.

### Move base package:
Subscribe to:
<ul>
  <li>/map (occupancy grid by SLAM)</li>
  <li>/tf /odom /scan (robot information and sensors reading) </li>
  <li>/move_base_simple/goals (goals for navigation) </li>
</ul> 

## Disclaimer
The contribution of this repository is to continously sends /move_base_simple/goals by sending action. The SLAM map and all navigation stack are available from the Turtlebot3 repository

## How to run


