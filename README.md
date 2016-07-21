# movesense_sensor(rosbuild)

## Depends
1. before you build your movesense_sensor package, please make sure you have installed the [movesense] libaries.
  see **./MoveSenseSDK1.0.1/README.md**

  you can also get the source code form **https://github.com/MoveSense-HumanPlus/MoveSenseSDK-linux.git** 

## ROS
2. Ubuntu install of [ROS] Indigo 
  http://wiki.ros.org/indigo/Installation/Ubuntu

## MoveSenseSensor package 
3. complie the [movesense_sensor] source code
  before you build samples source code, please make sure you have finished step 1 & 2.
 
 **The package can not be compiled without ROS**
  **this package will build with rosbuild**
  
		cd movesense_sensor
		chmod +x build.sh
		./build.sh

  This will executables **movesense_sensor_LR_node, movesense_sensor_LD_node, movesense_sensor_LRD_node**in *movesense_sensor* folder.

4. run the movesense_sensor package
  you shuld run following command to add your package in ROS PATH.

		$ source ./build/devel/setup.bash
  
  before run the movesense_sensor package, you shuld open a new termina and run:

		$ roscore
 

  to run the LR mode of MoveSenseSensor,use
		
		$ rosrun movesense_sensor movesense_sensor_LR_node 
  
  now you can open a new termina to see the topic:
  
		$ rostopic list
		$ rostopic echo /movesense/left/image_raw
  
  open a new termina to display images:

		$ rosrun image_view image_view image:=/movesense_sensor/left/image_raw

  lauch rviz with the following command. Then click on **add** (bottom left), select the **By Topic** tab, select **movesense_sensor->left->image_raw** and click **OK**.

		$ rosrun rviz rviz
  
  
  when run **movesense_sensor_LR_node**, the MoveSenseSensor while work in default mode:
             
		The camera default launch mode is : 'CAM_STEREO_752X480_LR_30FPS'.
		default param path  is: ./config
		default topic is :
		/movesense_sensor/left/image_raw
		/movesense_sensor/left/camera_info
		/movesense_sensor/right/image_raw
		/movesense_sensor/right/camera_info);
             
  to change the default param of movesense_sensor, use:

		$ rosrun movesense_sensor movesense_sensor_LR_node mode:=CAM_STEREO_752X480_LR_30FPS param:=./config.

  you can use the following keyword to change the sensor work mode
  
		CAM_STEREO_752X480_LR_30FPS			'LR_NODE'
		CAM_STEREO_752X480_LD_30FPS			'LD_NODE'
		CAM_STEREO_752X480_LRD_30FPS		'LRD_NODE'
		CAM_STEREO_376X240_LR_30FPS			'LR_NODE'
		CAM_STEREO_376X240_LD_30FPS			'LD_NODE'
		CAM_STEREO_376X240_LRD_30FPS		'LRD_NODE'
  
  you can stop you movesense_sensor node whit the command:

		CTRL+C
  
## ORB_SLAME packge
  get the source code form **https://github.com/raulmur/ORB_SLAM2.git**

  complite the [ORB_SLAM2] follow the README.md

  run the stereo node with

		$ rosrun ORB_SLAM2 Stereo Vocabulary/ORBvoc.txt Examples/Stereo/EuRoC.yaml false

  and run the movesense node with
		
		$ rosrun movesense_sensor movesense_sensor_LR_node __name:=image
  
  don't forget update the camera param from **movesense_sensor/config/camera_param.yaml** to **ORB_SLAM2/Examples/Stereo/EuRoC.yaml**
