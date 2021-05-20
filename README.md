# ROS_Package_RBX1

_All documentation is based on ROS classes (2021-I) on class notes and the interpretation of 3rd party packages_

## Robot RBX1 

### First step: Create a workspace

* In a first terminal, the following statement is executed to create the workspace "catkin_ws" in home and inside the scr folder:
```
mkdir -p ~/catkin_ws/scr
```

* In the same terminal, the following statement is executed to go to the created workspace: 
```
cd catkin_ws
```

* And again in the same terminal the following sentence is executed to compile the workspace and start creating packages within it: 
```
catkin_make
```

### Step Two: Install RBX1 Repository

To install directly from the ROS repository, execute the following statement in a terminal:
```
sudo apt-get install ros-kinetic-rbx1
```
_Note: For this repository the kinectic distribution is used, in this case of having a different distribution, check and change the statement for your version of ROS_   

Or if you want to install from a github repository you should do the following:

* In a terminal to go to the source folder of the workspace, the following sentence is executed:
```
cd ~/catkin_ws/src
```

* And in the same terminal the following statement is executed to copy the RBX1 repository from the author's github: 
```
git clone https://github.com/pirobot/rbx1.git
```
### Third step: Run the _.launch_ file
Launch files are used to run multiple files or nodes at the same time, without having to be running node by node on different terminals. First we must initialize the ROS environment to be able to work with the nodes and others, for this the following sentence is executed in a terminal:
```
roscore
```
The RBX1 package contains several .launch, the specific file which will work is _fake_turtlebot.launch_ which can be found in the directory _catkin_ws/src/rbx1/rbx1_bringup/launch_ and is executed with the following statement:
```
roslaunch rbx1_bringup fake_turtlebot.launch
```
One way to visualize the nodes that a .launch file executes is through the _rqt_grahp_ which provides a graphic element to visualize topics and nodes currently connected, to execute it can be done through the following sentences:
```
rosrun rqt_graph rqt_graph
```
O well:
```
rqt_graph
```
And to graphically display the robot has executed the file .launch used rviz which opens a graphical interface from which you can see different processes or 3D simulations for libraries that require it in this case load the model within an environment 3D, to execute it is done through the following sentence:
```
rosrun rviz rviz -d`rospack find rbx1_nav`/sim.rviz
```
### Step Four: Modify the _.launch_ file
For this example we will modify the file with which we are working _fake_turtlebot.launch_. In this specific case, a topic will be modified within the file so that the RBX1 robot is compatible with the teleop_key feature of the turtlebot example included in ROS. 
_Note: To perform this step, the third step must have been completed correctly_

* In a new terminal to use the teleoperator, it is necessary to execute the following statement:
```
rosrun turtlesim turtle_teleop_key
```
* And in another terminal to know the topic to modify, the following sentence is executed:
```
rostopic list
```
In the current topics, it can be seen that there are two similar topics: _/cmd_vel_ and _/turtle1/cmd_vel_. The topic to modify is precisely _/turtle1/cmd_vel_, when killing the _teleop_key_ process you can see that the topic called _/turtle1/cmd_vel_ will disappear. To make the changes you must do the following::

* First you have to go to the specific directory that contains the _.launch_ which mentioned before _catkin_ws/src/rbx1/rbx1_bringup/launch_. You can search the files directly by going to the folder or access it using the following statement:
```
cd ~/catkin_ws/src/rbx1/rbx1_bringup/launch
```
* If it was accessed through the folder, the file can be opened with any text editor, and if it was through the terminal, the best way to edit it graphically is with the following statement:
```
gedit fake_turtlebot.launch
```
* Inside the file you must find the part of the code that executes the node called arbotix marked with the symbols </>, in a new line within this code segment you must write the following:
```
<remap from="/cmd_vel" to="/turtle1/cmd_vel"/>
```
* Finally, it must be saved, the running processes are killed and step 3 is repeated together with the teleoperator's sentence. The _arbotix RBX1_ robot can now be controlled within the _rviz_ environment with the _teleop_key_ feature from the ROS turtle bot example. 

_NOTE: In this repository I attach the modified .launch file to check the changes or if you want to replace it with the one from your project_ 


## Authors

* Eymer S. Tapias
* Mauricio Goméz
* Nikcolas Rojas
