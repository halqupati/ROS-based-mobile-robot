# ROS based mobile robot
 Mobile robot used ROS to naviagtion and SLAM.


#yemenbot navigation
![yemen_robot](https://user-images.githubusercontent.com/48286288/133316567-83c062c2-7f85-48fc-a539-48482f5c1bc4.gif)


# yemenbot

This ROS package implements SLAM on a 2 wheeled differential drive robot to map an unknown environment. A joystick or keyboard is used to teleoperate the robot in Gazebo. The map generated is then used for autonomous navigation using the ROS Navigation stack.


## Installation
1. Build package from source: navigate to the source folder of your catkin workspace and build this package using:
	```
	$ git clone https://github.com/halqupati/ROS-based-mobile-robot.git
	$ cd ..
	$ catkin_make
	```
2. Install Required dependencies:
	```
	$ sudo apt-get install ros-noetic-dwa-local-planner
	$ sudo apt-get install ros-noetic-joy
	```

## Simultaneous Localization And Mapping (SLAM)

The package uses [slam_gmapping](http://wiki.ros.org/slam_gmapping) to map the environment. For the purpose of this demonstration, we use the Gazebo simulation environment to move around the robot. 



1. Load the robot in the Gazebo environment. Default model is the turtlebot3_house. You can change this from ```/worlds/mybot.world```. To continue with default model:
	```
	$ roslaunch yemenbot gazebo.launch 
	```
2. Launch the **slam_gmapping** node. This will also start **rviz** where you can visualize the map being created:
	```
	$ roslaunch yemenbot gmapping.launch
	```
3. Move the robot around. by teleop using keyboard:
	 ```
	 $ rosrun yemenbot keyboard_teleop.py 
	 ```
4. Move the robot in your environment till a satisfactory map is created. 
5. Save the map using:
	```
	$ rosrun map_server map_saver -f ~/test_map
	```
6. Copy the map file to ```~/yemenbot/maps/``` directory and edit the .yaml file to match the path. 
	
 
# 3D mapping 
![Screenshot from 2021-09-15 22-05-57](https://user-images.githubusercontent.com/48286288/134371526-b84ce18d-d77d-46af-81d9-34f247835c95.png)


## Autonomous Navigation
This package uses the [ROS Navigation stack](http://wiki.ros.org/navigation) to autonomously navigate through the map created using gmapping. 

![yemen_robot](https://user-images.githubusercontent.com/48286288/133316567-83c062c2-7f85-48fc-a539-48482f5c1bc4.gif)
  
0. To use your generated map, edit ```/launch/navigation.launch``` and add map .yaml location and name to map_server node launch.
1. Load the robot in gazebo environment:
	```
	$ roslaunch yemenbot gazebo.launch 
	```
2. Start the **amcl**, **move_base** and **rviz** nodes:
	```
	$ roslaunch yemenbot navigation.launch
	```
3. In rviz, click on ***2D Pose Estimate*** and set initial pose estimate of the robot.
4. To move to a goal, click on ***2D Nav Goal*** to set your goal location and pose.  


## yemenbot hardware

![photo_2021-09-13_21-32-28 (2)](https://user-images.githubusercontent.com/48286288/134373881-0d97f86f-be57-4d8f-997a-0ceeb52f3940.jpg)

https://user-images.githubusercontent.com/48286288/134375639-04e31d4f-ec47-4d65-a786-871e8bfd88e3.MOV
)
