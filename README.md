# realsense_gazebo_description

This ROS package contains the models to simulate in Gazebo the Intel Realsense D435, D435i and T265 camera.
To function properly it require the gazebo plugins found in [m-tartari/realsense_gazebo_plugin](https://github.com/m-tartari/realsense_gazebo_plugin).

## Use

In the urdf file where you want to use the simulated realsense add the following code (replace ```parent```, ```name```, ```topics_ns```, and ```origin```  with you are using).

```xml
  <!-- d435 frame definition can be found at https://github.com/IntelRealSense/librealsense/blob/master/doc/d435i.md -->
  <xacro:include filename="$(find realsense_gazebo_description)/urdf/_d435.urdf.xacro"/>
  <xacro:sensor_d435 parent="base_link" name="D435_camera" topics_ns="D435_camera">
    <origin xyz="0.0 0.0 0.0" rpy="0.0 0.0 0.0"/>
  </xacro:sensor_d435>

  <!-- d435i frame definition can be found at https://github.com/IntelRealSense/librealsense/blob/master/doc/d435i.md -->
  <xacro:include filename="$(find realsense_gazebo_description)/urdf/_d435i.urdf.xacro"/>
  <xacro:sensor_d435i parent="base_link" name="D435i_camera" topics_ns="D435i_camera"
                      enable_pointCloud="true" unite_imu_method="false"> <!-- unite_imu_method can be false, copy or linear_interpolation -->
    <origin xyz="0.0 0.0 0.0" rpy="0.0 0.0 0.0"/>
  </xacro:sensor_d435i>

  <!-- t265  frame definition can be found at https://github.com/IntelRealSense/librealsense/blob/master/doc/t265.md 
  xyz and rpy paramenters are used as a base for odometry, they represent the traspformation from the robot base_link -->
  <xacro:include filename="$(find realsense_gazebo_description)/urdf/_t265.urdf.xacro"/>
  <xacro:sensor_t265  parent="parent_link" name="T265_camera" topics_ns="T265_camera"
                      xyz="0.0 0.0 0.0" rpy="0.0 0.0 0.0"
                      unite_imu_method="false"> <!-- unite_imu_method can be false, copy or linear_interpolation -->
    <origin xyz="0.0 0.0 0.0" rpy="0.0 0.0 0.0"/>
  </xacro:sensor_t265>
```

You can run an example on Gazebo using:

```shell
roslaunch realsense_gazebo_description multicamera.launch
```
