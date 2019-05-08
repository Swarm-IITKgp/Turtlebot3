Save this package into catkin_ws/src/.

Run gazebo simulation by running 'roslaunch turtlebot3_gazebo turtlebot3_world.launch' or bringing up the actual turtlebot.

If you are running ROS Melodic, then replace 'gmapping' with 'karto' in step 1 and make sure you have karto slam package installed.

Then run the following commands:
1) Run 'roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping'
2) Run 'rosrun turtlebot3_autonomous mapping.py'. This will run the mapping service.
3) Run 'rosrun turtlebot3_autonomous control.py'. This will run the control script.
