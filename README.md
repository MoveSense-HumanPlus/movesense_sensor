# movesense_sensor(rosbuild)

## Library Dependency
1. Before you build your movesense_sensor package, please make sure you have installed the [movesense] libraries.
  For further information, please refer to  **./MoveSenseSDK-linux/README.md**

  You can also get the source codes from the website:**https://github.com/MoveSense-HumanPlus/MoveSenseSDK-linux.git** 

## ROS
2. Installation of [ROS] Indigo in Ubuntu  
  Please visit the website: http://wiki.ros.org/indigo/Installation/Ubuntu

## MoveSenseSensor package 
3. Compiling the [movesense_sensor] source codes
  Before you build source codes, please make sure you have operated correctly according to step 1 & 2.
 
 **The package can not be compiled without ROS**
  **This package will be built with rosbuild**
  
		cd movesense_sensor
		chmod +x build.sh
		./build.sh

  Executing these commands above will generate executable programs which include **movesense_sensor_LR_node, movesense_sensor_LD_node, movesense_sensor_LRD_node**in *movesense_sensor* folder.

4. Run the movesense_sensor
  You should execute following command to add your package to ROS PATH:

		$ source ./build/devel/setup.bash
  
  You should execute following command in a new terminal before running the movesense_sensor package:

		$ roscore
 
  Run movesense_sensor_LR_node:
		
		$ rosrun movesense_sensor movesense_sensor_LR_node 
  
  Now you can open a new terminal to see following topics:
  
		$ rostopic list
		$ rostopic echo /movesense/left/image_raw
  
  Open a new terminal to display images:

		$ rosrun image_view image_view image:=/movesense_sensor/left/image_raw

  Launch rviz using the following command. Then click on **add** (bottom left), select the **By Topic** tab, select **movesense_sensor->left->image_raw** and click **OK**.

		$ rosrun rviz rviz
  
  When running **movesense_sensor_LR_node**, the MoveSenseSensor will work in default mode:
             
		The camera default mode is : 'CAM_STEREO_752X480_LR_30FPS'.
		default param path  is: ./config
		default topic is :
		/movesense_sensor/left/image_raw
		/movesense_sensor/left/camera_info
		/movesense_sensor/right/image_raw
		/movesense_sensor/right/camera_info);
             
  Change the default param of movesense_sensor:

		$ rosrun movesense_sensor movesense_sensor_LR_node mode:=CAM_STEREO_752X480_LR_30FPS param:=./config.

  You can use the following keywords to change the sensor work mode:
  
		CAM_STEREO_752X480_LR_30FPS			'LR_NODE'
		CAM_STEREO_752X480_LD_30FPS			'LD_NODE'
		CAM_STEREO_752X480_LRD_30FPS		'LRD_NODE'
		CAM_STEREO_376X240_LR_30FPS			'LR_NODE'
		CAM_STEREO_376X240_LD_30FPS			'LD_NODE'
		CAM_STEREO_376X240_LRD_30FPS		'LRD_NODE'
  
  You can stop you movesense_sensor node:

		CTRL+C
  
## ORB_SLAME packge
  Get the source codes from the website:**https://github.com/raulmur/ORB_SLAM2.git**

  Compile the [ORB_SLAM2] according to the README.md

  Run the stereo node:

		$ rosrun ORB_SLAM2 Stereo Vocabulary/ORBvoc.txt Examples/Stereo/EuRoC.yaml false

  Run the movesense node:
		
		$ rosrun movesense_sensor movesense_sensor_LR_node __name:=image
  
  Don't forget to update the camera param of **ORB_SLAM2/Examples/Stereo/EuRoC.yaml** referring to **movesense_sensor/config/camera_param.yaml**
