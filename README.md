# The Project
This is the capstone project for Udacity's Self Driving Car Engineer Nanodegree. The project is a culmination of other projects to integrate into a self driving car.

## Contributors

Timothy Ta timothyta12@gmail.com

### The Parts
To build an entire system to power a self driving car, there needs to be a unifying element between all the components. Here the components consist of ROS Nodes which are able to run independently and communicate with each other. 

* Waypoint Updater
* Controller
* Traffic Light Detection

### Waypoint Updater
The goal of the updater is to calculate the waypoints the car needs to take. The car is initally given a set of initial waypoints to work with. Only a small subset is used at anytime. The subset is created based off the current position of the car.
The final waypoint output depends on the actions of the car. For this project the main focus was slowing down when there is a traffic light. When the car senses there is a red light, the car calculates a trajectory to slow down the car.  
This updater can later be extended to include lane shifting and possible obstacle avoidance.

### Controller
The three main inputs of a car are steering, throttle, and braking. These inputs all depend on what the car is supposed to do. Using the given waypoints, a desired set of velocities are calculated. Since the car cannot instantaneously accelerate, the controller must adjust itself to match these velocities. Several models are used for controlling these componenents.  
The throttle is controlled using a PID controller to provide smooth acceleration.  
The steering is controlled by calculating the how to match the correct angle without oversteering.
The brakes are applied exclusively from the throttle. Brakes should only be applied when there is no throttle and the car wants to slow down. This is done by brute calculation with the car's current position and the desired stopping location.

### Traffic Light Detection
Currently, the simulator provides the position and states of the traffic lights. Using this information, if the light is red, the car will calculate a deccelerating trajectory to stop near the line. If the light is green the car will continue normally.  
The next goal of this part is to automate the detection of traffic lights using a camera. This can be achieved through a CNN to give a classification of traffic lights.

This is the project repo for the final project of the Udacity Self-Driving Car Nanodegree: Programming a Real Self-Driving Car. For more information about the project, see the project introduction [here](https://classroom.udacity.com/nanodegrees/nd013/parts/6047fe34-d93c-4f50-8336-b70ef10cb4b2/modules/e1a23b06-329a-4684-a717-ad476f0d8dff/lessons/462c933d-9f24-42d3-8bdc-a08a5fc866e4/concepts/5ab4b122-83e6-436d-850f-9f4d26627fd9).

Please use **one** of the two installation options, either native **or** docker installation.

### Native Installation

* Be sure that your workstation is running Ubuntu 16.04 Xenial Xerus or Ubuntu 14.04 Trusty Tahir. [Ubuntu downloads can be found here](https://www.ubuntu.com/download/desktop).
* If using a Virtual Machine to install Ubuntu, use the following configuration as minimum:
  * 2 CPU
  * 2 GB system memory
  * 25 GB of free hard drive space

  The Udacity provided virtual machine has ROS and Dataspeed DBW already installed, so you can skip the next two steps if you are using this.

* Follow these instructions to install ROS
  * [ROS Kinetic](http://wiki.ros.org/kinetic/Installation/Ubuntu) if you have Ubuntu 16.04.
  * [ROS Indigo](http://wiki.ros.org/indigo/Installation/Ubuntu) if you have Ubuntu 14.04.
* [Dataspeed DBW](https://bitbucket.org/DataspeedInc/dbw_mkz_ros)
  * Use this option to install the SDK on a workstation that already has ROS installed: [One Line SDK Install (binary)](https://bitbucket.org/DataspeedInc/dbw_mkz_ros/src/81e63fcc335d7b64139d7482017d6a97b405e250/ROS_SETUP.md?fileviewer=file-view-default)
* Download the [Udacity Simulator](https://github.com/udacity/CarND-Capstone/releases).

### Docker Installation
[Install Docker](https://docs.docker.com/engine/installation/)

Build the docker container
```bash
docker build . -t capstone
```

Run the docker file
```bash
docker run -p 4567:4567 -v $PWD:/capstone -v /tmp/log:/root/.ros/ --rm -it capstone
```

### Port Forwarding
To set up port forwarding, please refer to the [instructions from term 2](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/0949fca6-b379-42af-a919-ee50aa304e6a/lessons/f758c44c-5e40-4e01-93b5-1a82aa4e044f/concepts/16cf4a78-4fc7-49e1-8621-3450ca938b77)

### Usage

1. Clone the project repository
```bash
git clone https://github.com/udacity/CarND-Capstone.git
```

2. Install python dependencies
```bash
cd CarND-Capstone
pip install -r requirements.txt
```
3. Make and run styx
```bash
cd ros
catkin_make
source devel/setup.sh
roslaunch launch/styx.launch
```
4. Run the simulator

### Real world testing
1. Download [training bag](https://s3-us-west-1.amazonaws.com/udacity-selfdrivingcar/traffic_light_bag_file.zip) that was recorded on the Udacity self-driving car.
2. Unzip the file
```bash
unzip traffic_light_bag_file.zip
```
3. Play the bag file
```bash
rosbag play -l traffic_light_bag_file/traffic_light_training.bag
```
4. Launch your project in site mode
```bash
cd CarND-Capstone/ros
roslaunch launch/site.launch
```
5. Confirm that traffic light detection works on real life images
