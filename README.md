# realsense_gazebo_description

This ROS package contains the models to simulate in Gazebo the Intel Realsense D435, D435i and T265 camera.
To function properly it require the gazebo plugins found in [m-tartari/realsense_gazebo_plugin](https://github.com/m-tartari/realsense_gazebo_plugin).

## Use

In the xacro file where you want to use the simulated cameras add the following code (replace the content of ```parent```, ```name```, ```topics_ns```, and ```origin```  with you are using).
```xml
  <!-- d435  frame definition can be found at https://github.com/IntelRealSense/librealsense/blob/master/doc/d435i.md -->
  <xacro:include filename="$(find realsense_gazebo_description)/urdf/_d435.urdf.xacro"/>
  <xacro:sensor_d435  parent="base_link" name="D435_camera" topics_ns="D435_camera" >
    <origin xyz="0.0 -0.5 0.1" rpy="0.0 0.0 0.0"/>
  </xacro:sensor_d435>

  <!-- d435i frame definition can be found at https://github.com/IntelRealSense/librealsense/blob/master/doc/d435i.md -->
  <xacro:include filename="$(find realsense_gazebo_description)/urdf/_d435i.urdf.xacro"/>
  <xacro:sensor_d435i parent="base_link" name="D435i_camera" topics_ns="D435i_camera"> 
    <origin xyz="0.0 0.5 0.1" rpy="0.0 0.0 0.0"/>
  </xacro:sensor_d435i>

  <!-- t265  frame definition can be found at https://github.com/IntelRealSense/librealsense/blob/master/doc/t265.md
  odom_xyz and odom_rpy paramenters are used as a base for odometry, they represent the traspformation from the robot base_link -->
  <xacro:include filename="$(find realsense_gazebo_description)/urdf/_t265.urdf.xacro"/>
  <xacro:sensor_t265  parent="base_link" name="T265_camera" topics_ns="T265_camera"
                      odom_xyz="0.0 0.0 0.25" odom_rpy="0.0 0.0 0.0">
    <origin xyz="0.0 0.0 0.25" rpy="0.0 0.0 0.0"/>
  </xacro:sensor_t265>
```

### Notes

- You can launch an example on Gazebo using: ```roslaunch realsense_gazebo_description multicamera.launch```.
- For a full list of the optional params and their default values you can look at [multicamera_params.urdf.xacro](https://github.com/m-tartari/realsense_gazebo_description/blob/master/urdf/multicamera_params.urdf.xacro).
- When using a single camera, ```name``` and ```topic_ns``` can be removed. They will default to ```camera```.
- For multi-camera simulations, ```name``` and ```topic_ns``` are required to avoid errors due to conflicting names. Multiple istances of the same camera can be used used if they are given different ```name``` and ```topic_ns```.
- As described in the offical [IntelRealSense/realsense-ros/README.md](https://github.com/IntelRealSense/realsense-ros/blob/development/README.md) when the param ```align_depth``` is set true, the topics ```/camera/aligned_depth_to_color/image_raw``` and ```/camera/aligned_depth_to_color/camera_info``` are added. However, to lighten the simulation (differently for the real camera), the topics ```/camera/depth/image_rect_raw``` and ```/camera/depth/camera_info``` are removed when this happens.