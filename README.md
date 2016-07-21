# movesense_sensor(ros)

## Depends
1. before you build your movesense_sensor package, please make sure you have installed the **movesense** libaries.
  see **./MoveSenseSDK1.0.1/README.md**

  you can also get the source code form **https://github.com/MoveSense-HumanPlus/MoveSenseSDK-linux.git** 

## ROS
2. Ubuntu install of ROS Indigo 
  http://wiki.ros.org/indigo/Installation/Ubuntu

## MoveSenseSensor package 
3. complie the movesense_sensor source code
  before you build samples source code, please make sure you have finished step 1 & 2.
  **The package can not be compiled without ROS**
  **this package will build with rosbuild**
  
  cd movesense_sensor
  chmod +x build.sh
  ./build.sh

  This will executables **movesense_sensor_LR_node, movesense_sensor_LD_node, movesense_sensor_LRD_node**in *movesense_sensor* folder.

4. run the movesense_sensor package
  you shuld run command **$ source ./build/devel/setup.bash** to add your package in ROS PATH
  and run a new terminal, input the command **$ roscore** and run

  use **rosrun movesense_sensor movesense_sensor_LR_node** to run the LR mode of MoveSenseSensor
  
  now you can 
  use **$ rostopic list** in a new terminal to see the topic list and **rostopic echo /movesense/left/image_raw** to see the image data;
  use **$ rosrun rviz rviz** in a new terminal to run the Rviz to see the image;
  use **$ rosrun image_view image_view image:=/movesense/left/image_raw**in a new terminal to run the image view to see the image.
  
  when run **movesense_sensor_LR_node**, the MoveSenseSensor while work in default mode:
             "The camera default launch mode is : 'CAM_STEREO_752X480_LR_30FPS'."
             "default param path  is: ./config"
             "default topic is :"
             "/movesense_sensor/left/image_raw"
             "/movesense_sensor/left/camera_info"
             "/movesense_sensor/right/image_raw"
             "/movesense_sensor/right/camera_info");  
  you can use **rosrun movesense_sensor movesense_sensor_LR_node mode:=New_Mode param:=You_Param_Path** to change the default param.
  
  you can stop you movesense_sensor node whit **CTRL+C** command.
  
## ORB_SLAME packge

