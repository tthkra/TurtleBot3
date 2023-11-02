# TurtleBot3
use TurtleBot3 in a virtual environment to create a map using SLAM method

## ROS
before you start, you need first to have ROS installed, to do so, you can follow this guide repository: https://github.com/tthkra/ROSInstallation-task1 .

## TurtleBot3 
first, install TurtleBot3 pakages

create a new workspace and navigate to it
```bash
mkdir -p ~/catkin_ws/src 
cd ~/catkin_ws/src/ 
```
Clone TurtleBot3 packages (replace "melodic" with the version your working with or romove "-b melodic-devel" if you dont want to specify a version)
```bash
git clone -b melodic-devel https://github.com/ROBOTIS-GIT/DynamixelSDK.git
git clone -b melodic-devel https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git
git clone -b melodic-devel https://github.com/ROBOTIS-GIT/turtlebot3.git
```
```bash
cd ~/catkin_ws && catkin_make
```
```bash
echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
```
specify a turtleBot model 
```bash
source ~/.bashrc
```
add the highlighted line to the end of file then save the file and close it

<img width="486" alt="Screenshot 2023-10-31 204941" src="https://github.com/tthkra/TurtleBot3/assets/142266646/6be5708a-d73f-47c5-93ae-4a410592539a">

```bash
source ~/.bashrc
```

## TurtleBot3 Simulation
install TurtleBot3 simulation packages
```bash
cd ~/catkin_ws/src/
git clone -b melodic-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
cd ~/catkin_ws && catkin_make
```
### simulate TurtleBot3 using Gazebo
to sumulate the the TurtleBot3, you nedd first to install Rviz packages. follow this guide [here](https://classic.gazebosim.org/tutorials?tut=ros_installing&cat=connect_ros)

install TurtleBot3 Packages for Gazebo
```bash
sudo apt-get install ros-melodic-turtlebot3-gazebo
```
launch TurtleBot3 in an empty space environment
```bash
export TURTLEBOT3_MODEL=burger
roslaunch turtlebot3_gazebo turtlebot3_empty_world.launch
```
<img width="584" alt="Screenshot 2023-11-01 054825" src="https://github.com/tthkra/TurtleBot3/assets/142266646/29df9248-5922-46d8-8182-7a92374a5d75">

### Create New Environment With Obstacles
you can change the empty environment to a one with obstacles whichs where the SLAM method will take place.

#### TurtleBot3 World
launch TurtleBot3 World environment
```bash
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```
<img width="583" alt="Screenshot 2023-11-01 114944" src="https://github.com/tthkra/TurtleBot3/assets/142266646/faa9afb7-b449-4f63-b933-0b4332e4ff5b">
<img width="584" alt="Screenshot 2023-11-02 022718" src="https://github.com/tthkra/TurtleBot3/assets/142266646/38903780-dfaf-4042-acab-667b21c138f7">

#### TurtleBot3 House
launch TurtleBot3 House
```bash
roslaunch turtlebot3_gazebo turtlebot3_house.launch
```
<img width="582" alt="Screenshot 2023-11-02 034608" src="https://github.com/tthkra/TurtleBot3/assets/142266646/bcf6063b-2b30-4552-a40c-00996fe62aaf">

move and condtrol Turtulebots direction
open a new terminal tab
```bash
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```
<img width="666" alt="Screenshot 2023-11-02 040345" src="https://github.com/tthkra/TurtleBot3/assets/142266646/c6a0a78f-30f0-45ca-8aeb-1e1770cb01d3">

## TurtleBot3 SLAM 
SLAM (Simultaneous Localization and Mapping) is a method for mapping an unknown area while at the same time determining the location within that area. this works when the robot start moving and
navigating around the whole area so that it scan and map every datail of that area. now apply this method on the TurtleBot3 World with Gazebo and visualize the mapping process through Rviz and then
save the drawn map after the robot finish.

before you start, install Rviz and moveit packages so you can see the robot mapping the area.

see Rviz installation guide [here](https://installati.one/install-rviz-ubuntu-18-04/?expand_article=1) <br>
see Moveit installation guide [here](http://docs.ros.org/en/melodic/api/moveit_tutorials/html/doc/getting_started/getting_started.html)

install SLAM package
```bash
sudo apt install ros-melodic-slam-gmapping
```
launch Gazebo 
```bash
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```
let the robot start moving and navigating the area. open a new terminal tab  
```bash
roslaunch turtlebot3_gazebo turtlebot3_simulation.launch
```
<img width="552" alt="Screenshot 2023-11-02 182825" src="https://github.com/tthkra/TurtleBot3/assets/142266646/7f482a12-0547-4c1c-a442-792d8d8bfa93"> <br>
start the SLAM in Rviz
```bash
roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping
```
now watch the robot moving around and mapping the environment <br>
<img width="614" alt="Screenshot 2023-11-02 195510" src="https://github.com/tthkra/TurtleBot3/assets/142266646/8f4b79e7-ffb3-4c27-93ba-556cf1a804f6">
<img width="614" alt="Screenshot 2023-11-02 200013" src="https://github.com/tthkra/TurtleBot3/assets/142266646/9193122a-573b-46cf-a0d1-65b14cdcdd83">

finally, save the map after the robot finish mapping the area
```bash
rosrun map_server map_saver -f ~/test_map
```
