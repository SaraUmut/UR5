The detailed steps to work with ROS and UR (using ROS kinetic and ubuntu 16.04, or ROS indigo and ubuntu 14.04):
(it may be obvious but it was a problem for me)

1- download ubuntu 16.04 (or ubuntu 14.04)
http://releases.ubuntu.com/16.04.5/ (ubuntu-16.04.5-desktop-amd64.iso )

2- install ROS kinetic (or ROS indigo)
http://wiki.ros.org/kinetic/Installation/Ubuntu (all the steps from 1.1 to 1.7, using Desktop-Full Install version)

3- source: 
`$ source /opt/ros/kinetic/setup.bash`

4- create catkin_ws (src), as:

```
$ mkdir -p ~/catkin_ws/src
$ cd ~/catkin_ws/
$ catkin_make

$ source devel/setup.bash

$ echo $ROS_PACKAGE_PATH
```
should gives: /home/youruser/catkin_ws/src:/opt/ros/kinetic/share

5- write those:
```
source /opt/ros/kinetic/setup.bash
mkdir -p $HOME/catkin_ws/src
cd $HOME/catkin_ws
git -C src/ clone -b kinetic-devel https://github.com/ros-industrial/ur_modern_driver.git
rosdep update
rosdep install --from-paths src/ --ignore-src
catkin_make
source $HOME/devel/setup.bash
```
6- then in new terminal: `roscore`

7- in another new terminal (pc ip: 10.1.1.5, robot ip: 10.1.1.4):
```
source catkin_ws/devel/setup.bash
roslaunch ur_modern_driver ur5_bringup.launch robot_ip:=10.1.1.4
```

8- in another new terminal:
```
source devel/setup.bash
rosrun ur_modern_driver test_move.py
```
...........................
note: in every new terminal you should '`source devel/setup.bash`'
or you can add that to the bash file:
`sudo nano ~/.bashrc`
go to the end of it, you will find this line:
`source /opt/ros/indigo/setup.bash`
after it you should add this line:
`source ~/catkin_ws/devel/setup.bash`

press ctrl+o to save and press enter
then ctrl+x to exit

close the terminal then open it again
...........................

Thanks for gavanderhoorn and miguelprada for their help.
