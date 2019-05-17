# Multi Robot operation, and Map Merge

Uses **ROS_NAMESPACE** environment variable and use of **multi_robot_name** argument in command line.  
You will need to run a lot of terminals at the same time. Use tabs within the same window.  
References:  
https://wiki.nps.edu/pages/viewpage.action?pageId=1160183818
http://emanual.robotis.com/docs/en/platform/turtlebot3/simulation/#virtual-slam-by-multiple-turtlebot3s
http://wiki.ros.org/multirobot_map_merge

## Single Operation and SLAM with Namespace:  
Important feature required to operate multi_map_merge is the multiple NAMESPACE for turtlebots and the use of multi_robot_name argument with ros commands. Here we use names: tb3_0 and tb3_1  

### **1. BringUp and Remote Launch:**

**REMOTE PC**  
```bash
  roscore
```
**TURTLEBOT**:  
```bash
  ROS_NAMESPACE=tb3_0 roslaunch turtlebot3_bringup turtlebot3_robot.launch multi_robot_name:="tb3_0" set_lidar_frame_id:="tb3_0/base_scan"
```
**REMOTE PC**  
```bash
  ROS_NAMESPACE=tb3_0 roslaunch turtlebot3_bringup turtlebot3_remote.launch multi_robot_name:=tb3_0
```
### **2. TeleOp Launch:**

**REMOTE PC**  
```bash
  ROS_NAMESPACE=tb3_0 roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch multi_robot_name=tb3_0
```

### **3. SLAM launch and RViz Launch:**

**REMOTE PC**  
```bash
  ROS_NAMESPACE=tb3_0 roslaunch turtlebot3_slam turtlebot3_gmapping.launch set_base_frame:=tb3_0/base_footprint set_odom_frame:=tb3_0/odom set_map_frame:=tb3_0/map
  rosrun rviz rviz -d `rospack find turtlebot3_gazebo`/rviz/multi_turtlebot3_slam.rviz
```    

## Two Bot Operation and Map Merge:  
### **1. BringUp and Remote Launch:**  
_Export the necessary environment variables to .bashrc and source it._ 

**REMOTE PC**  
```bash
  roscore
```
**TURTLEBOT (separately)**  

```bash
  ROS_NAMESPACE=tb3_0 roslaunch turtlebot3_bringup turtlebot3_robot.launch multi_robot_name:="tb3_0" set_lidar_frame_id:="tb3_0/base_scan"
  ROS_NAMESPACE=tb3_1 roslaunch turtlebot3_bringup turtlebot3_robot.launch multi_robot_name:="tb3_1" set_lidar_frame_id:="tb3_1/base_scan"
```
**REMOTE PC**  
```bash
  ROS_NAMESPACE=tb3_0 roslaunch turtlebot3_bringup turtlebot3_remote.launch multi_robot_name:=tb3_0
  ROS_NAMESPACE=tb3_1 roslaunch turtlebot3_bringup turtlebot3_remote.launch multi_robot_name:=tb3_1
```
### **2. SLAM Launch**  

**REMOTE PC**  
```bash
  ROS_NAMESPACE=tb3_0 roslaunch turtlebot3_slam turtlebot3_gmapping.launch set_base_frame:=tb3_0/base_footprint set_odom_frame:=tb3_0/odom set_map_frame:=tb3_0/map
  ROS_NAMESPACE=tb3_1 roslaunch turtlebot3_slam turtlebot3_gmapping.launch set_base_frame:=tb3_1/base_footprint set_odom_frame:=tb3_1/odom set_map_frame:=tb3_1/map
```
### **3. Multi Map Merge and Visualization:**  

**REMOTE PC**  
Install Multi-Map merge
```bash
  sudo apt-get install ros-kinetic-multirobot-map-merge
```
Initialize map merge and visualise  
```bash
  roslaunch turtlebot3_gazebo multi_map_merge.launch
  rosrun rviz rviz -d `rospack find turtlebot3_gazebo`/rviz/multi_turtlebot3_slam.rviz
```
### **4. Launch TeleOp:**  

**REMOTE PC**  
In Separate Terminals launch teleoperation.  
```bash
  ROS_NAMESPACE=tb3_0 rosrun turtlebot3_teleop turtlebot3_teleop_key	ROS_NAMESPACE=tb3_1 rosrun turtlebot3_teleop turtlebot3_teleop_key
  ```
  
