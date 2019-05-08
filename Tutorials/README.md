# BringUp and Launch for TeleOperation
Added on **9th May, 2019**, TurtleBot running **ROS Kinetic**  
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
1. Open a new terminal and run:  
```bash
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch // Activate remote navigation
```
