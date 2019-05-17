TurtleBot3 running **ROS Kinetic**  
# Basic Operations: BringUp and Remote Launch
**REMOTE PC**
1. Modify .bashrc on Remote PC as:  
```bash
export TURTLEBOT3_MODEL=burger
export ROS_MASTER_URI=http://<RemotePC_IP>:11311 
export ROS_HOSTNAME=<RemotePC_IP>
```
2. Apply the variables on the current shell, by using:
```bash
source ~/.bashrc
```
3. launch roscore
```bash
roscore
```
**TURTLEBOT**
1. Open a new terminal SSH into Turtle bot
2. Modify .bashrc on Turtlebot:  
```bash
export ROS_MASTER_URI=http://<RemotePC_IP>:11311  
export ROS_HOSTNAME=<Turtlebot_IP>
```
3. Apply the variables on the current shell, by using
```bash 
source ~/.bashrc
```
4. Finally run this:
```bash
roslaunch turtlebot3_bringup turtlebot3_robot.launch //BRINGUP
```
**REMOTE PC**
1. Enable remote monitoring on PC, in a new terminal (Necessary for multi_slam, although not needed for teleOp)
```bash
roslaunch turtlebot3_bringup turtlebot3_remote.launch
```

# Teleop
**REMOTE PC**
1. Open a new terminal and run:  
```bash
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch // Activate remote navigation
```
# SLAM

**REMOTE PC**
1. Launch SLAM on turtlebot:
```bash
roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping
```
2. gmapping is a mapping technique. Other mapping techniques are **karto, hector, cartographer and frontier_exploration**. They **may need installation before use**, but gmapping is installed by default.
