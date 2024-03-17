# <div align="center">SLAM with Obstacle Avoidance</div>
![image](https://github.com/WinstonHChou/winter-2024-final-project-team-7/assets/68310078/0ba1c6cb-c9e0-4cf7-905a-f5f16e6bb2ca)
### <div align="center"> MAE 148 Final Project </div>
#### <div align="center"> Team 7 Winter 2024 </div>

<div align="center">
    <img src="images\ucsdrobocar-148-07.webp" width="800" height="600">
</div>

## Table of Contents
  <ol>
    <li><a href="#team-members">Team Members</a></li>
    <li><a href="#abstract">Abstract</a></li>
    <li><a href="#what-we-promised">What We Promised</a></li>
    <li><a href="#accomplishments">Accomplishments</a></li>
    <li><a href="#challenges">Challenges</a></li>
    <li><a href="#final-project-videos">Final Project Videos</a></li>
    <li><a href="#software">Software</a></li>
        <ul>
            <li><a href="#slam-simultaneous-localization-and-mapping">SLAM (Simultaneous Localization and Mapping)</a></li>
            <li><a href="#obstacle-avoidance">Obstacle Avoidance</a></li>
        </ul>
    <li><a href="#hardware">Hardware</a></li>
    <li><a href="#gantt-chart">Gantt Chart</a></li>
    <li><a href="#course-deliverables">Course Deliverables</a></li>
    <li><a href="#project-reproduction">Project Reproduction</a></li>
    <li><a href="#acknowledgements">Acknowledgements</a></li>
    <li><a href="#contacts">Contacts</a></li>
  </ol>

<hr>

## Team Members
Winston Chou - MAE Ctrls & Robotics (MC34) - Class of 2026 - [LinkedIn](https://www.linkedin.com/in/winston-wei-han-chou-a02214249/)

Amir Riahi - ECE - UPS Student

Rayyan Khalid - MAE Ctrls & Robotics (MC34) - Class of 2025
<hr>

## Abstract
The project's goal is to develop a robotic system capable of mapping a new enclosed environment, determining a path from a specified starting point to a desired destination while avoiding obstacles in its path. This involves integrating sensors for environmental perception, implementing mapping and localization algorithms, designing path planning and obstacle avoidance strategies, and creating a robust control system for the robot's navigation.

The robot utilizes the ROS2 Navigation 2 stack and integrating LiDAR for SLAM (Simultaneous Localization and Mapping) along with the OAK-D Lite depth point cloud camera for real-time obstacle avoidance.

<hr>

## What We Promised
### Must Have
* Integrate LiDAR sensor(s) into the ROS2 system. Utilize the ROS2 Navigation 2 stack to perform SLAM using LiDAR data.

### Nice to Have
* Integrate the OAK-D Lite depth camera, and Develop algorithms within ROS2 to process the point cloud data generated by OAK-D Lite for real-time obstacle detection. (ONLY Detection, for now)
* To move the robot from a given location A to a desired location B using the ROS2 Navigation 2 stack and integrated sensors. (Not implemented yet)
<hr>

## Accomplishments
* SLAM development accomplished
  * It enables the robot to map an unknown environment, and to locate its position.
  * Seeed IMU setup for better localization (Extended Kalman Filter).
* Obstacle Avoidance
  * Utilize its depth sensing capabilities to generate a point cloud representation of the environment. (Rviz2 and Foxglove Studio)
  * Simple obstacle detection algorithm
<hr>

## Challenges
* Nav2 Stack is a complex but useful system for developing an autonomous robot.
* Futher Actions:
  * PointCloud Dyanmic Obstacle Detection:  
    - Develop an algorithm to mark down position of obstacle group, and add them to Nav2 obstacle layer
  * Nav2 Path Planning & ROS 2 Control:  
    - Path Planning Server Development, and communication to ROS 2 Control System
<hr>

## Final Project Videos
**Click** any of the clips below to **reroute to the video**. 

#### **Mapping**

[<img src="images\mapping.webp" width="300">](https://youtu.be/1juHBhWz0MQ?si=Pjw60vCCNlXvP-IJ)

#### **Localization**

[<img src="images\localization.webp" width="300">](https://youtu.be/MX7kB6Jm7y0?si=0zmViTiaanLxiC1R)

#### **PCL Obstacle Detection**

[<img src="images\foxglove_pcl.webp" width="300">](https://youtu.be/iBNiwRAd4vU?si=_p8UwEmmzGuZwT1X)


#### Odom Frame Demo

[<img src="images\odom.webp" width="300">](https://youtu.be/PYMze0eOyS8?si=Nz3BIUGNAnoSLkpe)

#### Scan Correction Demo

[<img src="images\laser_frame.webp" width="300">](https://youtu.be/-2ELt_U10Mc?si=TWcBfC-b9EcZiGpV)

<hr>

## Software

### Overall Architecture
The project was successfully completed using the **Slam-Toolbox** and **ROS2 Navigation 2 Stack**, with a significant adaptation to the [djnighti/ucsd_robocar container](https://hub.docker.com/r/djnighti/ucsd_robocar). The adaptation allowed for seamless integration and deployment of the required components, facilitating efficient development and implementation of the robotic system.

### SLAM (Simultaneous Localization and Mapping)
- The **Slam Toolbox** proved indispensable in our project, enabling us to integrate the LD19 Lidar – firmware-compatible with the LD06 model – into the ROS2 framework. This integration allowed us to implement SLAM, empowering our robot to autonomously map its environment while concurrently determining its precise location within it. Additionally, we enhanced this capability by incorporating nav2 amcl localization, further refining the accuracy and dependability of our robot's localization system. By combining these technologies, our robot could navigate confidently, accurately mapping its surroundings and intelligently localizing itself within dynamic environments.<br>

- The **Online Async Node** from the Slam Toolbox is a crucial component that significantly contributes to the creation of the map_frame in the project. This node operates asynchronously, meaning it can handle data processing tasks independently of other system operations, thereby ensuring efficient utilization of resources and enabling real-time performance. The map_frame is a fundamental concept in SLAM, representing the coordinate frame that defines the global reference frame for the environment map being generated. The asynchronous online node processes Lidar data, and fuses this information together to construct a coherent and accurate representation of the surrounding environment.<br>

- The **VESC Odom Node** plays a pivotal role in supplying vital odometry frame data within the robotics system. This node is responsible for gathering information from the VESC (Vedder Electronic Speed Controller), and retrieves essential data related to the robot's motion, such as wheel velocities and motor commands. The odometry frame, often referred to as the "odom_frame," is a critical component in localization and navigation tasks. It represents the robot's estimated position and orientation based on its motion over time. This information is crucial for accurately tracking the robot's trajectory and determining its current pose within the environment. By utilizing the data provided by the VESC Odom Node, the system can update the odometry frame in real-time, reflecting the robot's movements and changes in its position. This dynamic updating ensures that the odometry frame remains synchronized with the robot's actual motion, providing an accurate representation of its trajectory.

<br>
<div align="center">
    <img src="images\Frames_Relationships.png" height="300"><br>
    <b>from https://answers.ros.org/question/387751/difference-between-amcl-and-odometry-source/</b><br>
    <img src="images\tf_tree.webp" height="600"><br>
    <b>Our Robot TF Tree</b><br>
</div><br>

- The **URDF Publisher** is a tool used to generate and publish Unified Robot Description Format (URDF) models within the ROS 2 ecosystem.
<br>
<div align="center">
    <img src="images\URDF.png" height="300"><br>
    <b>URDF Model of the robot</b><br>
    <img src="images\robot_on_ground.webp" height="300"><br>
    <b>Physical Robot</b><br>
</div><br>

- The **Seeed IMU Node** is used to publish IMU data Seeed Studio XIAO nRF52840 Sense. By integrating the Seeed Studio XIAO nRF52840 Sense's 6-Axis IMU and implementing an Extended Kalman Filter (Not Done), the robot gains improved localization accuracy and reduced odometry drift. The IMU provides orientation and acceleration data, complementing other sensors like wheel encoders and GPS. The Extended Kalman Filter fuses IMU and odometry measurements, dynamically adjusting uncertainties to mitigate noise and inaccuracies, resulting in enhanced navigation performance and reliability.<br>

<div align="center">
    <img src="https://github.com/WinstonHChou/winter-2024-final-project-team-7/assets/68310078/897b3a72-5760-4389-8faf-1873f8b8709a" height="300"><br>
    <b><a href="https://youtu.be/QrzTvfnHyqE">Seeed IMU Demo</a></b>
</div><br>

- The **Scan Correction Node** becomes particularly useful when there are specific sections of Lidar data that we wish to exclude from being collected by SLAM. This node allows us to define undesired ranges within the Lidar data and effectively filter them out, ensuring that only relevant and accurate information is utilized in the SLAM process. This capability enhances the overall quality and reliability of the generated map by preventing erroneous or irrelevant data from influencing the mapping and localization algorithms.
<br>
<div align="center">
    <img src="images\Non-filtered_map.png" height="300"><br>
    <b>Before filtered</b><br><br>
    <img src="images\Filtered_map.png" height="300"><br>
    <b>After filtered</b>
</div>

### Obstacle Avoidance
We utlized the OAK-D Lite depth camera to implement obstacle avoidance functionality within the ROS2 framework. Leveraging its depth sensing capabilities, we utilized the camera to generate a point cloud representation of the environment. The program logic is straightforward: the robot detects obstacles by identifying areas where the height is less than 2 meters (customizable) in front of it. If an object is detected within this distance threshold, the robot dynamically adjusts its trajectory to avoid collision, typically by making a turn. This simple yet effective approach allows the robot to navigate safely through its environment, reacting to potential obstacles in real-time to ensure smooth and obstacle-free movement.
<br>
<div align="center">
    <img src="images\rviz_pcl.jpg" height="300"><br>
    <b>PointCloud Visualization with Rviz2</b><br><br>
    <img src="images\foxglove_pcl.webp" height="300"><br>
    <b>PointCloud Visualization with Foxglove Studio</b>
</div><br>

We integrated the DepthAI ROS package into our ROS2 setup to enable object detection functionality. Within the package, we utilized the provided YOLO (You Only Look Once) neural network setup for object detection. This configuration allowed our robot to detect objects in its environment in real-time using deep learning techniques. By leveraging the YOLO neural network, our robot could accurately identify and classify various objects, enhancing its perception and autonomy for effective navigation in dynamic environments.
<br>
<div align="center">
    <img src="images\6_yolo_v3_tf_object_detection.webp" height="300"><br>
    <b>yolo_v3_tf_object_detection</b><br><br>
</div>

<hr>

## Hardware 

* __3D Printing:__ Camera Stand, Jetson Nano Case, GPS Plate, Lidar Mount
* __Laser Cut:__ Base plate to mount electronics and other components.

__Parts List__

* Traxxas Chassis with steering servo and sensored brushless DC motor
* Jetson Nano
* WiFi adapter
* 64 GB Micro SD Card
* Adapter/reader for Micro SD Card
* Logitech F710 controller
* OAK-D Lite Camera
* LD19 Lidar (LD06 Lidar)
* VESC
* Point One GNSS with antenna
* Anti-spark switch with power switch
* DC-DC Converter
* 4-cell LiPo battery
* Battery voltage checker/alarm
* DC Barrel Connector
* XT60, XT30, MR60 connectors

*Additional Parts used for testing/debugging*

* Car stand
* USB-C to USB-A cable
* Micro USB to USB cable
* 5V, 4A power supply for Jetson Nano

### __Mechanical Design Highlight__

__Base Plate__

<img src="images\BasePlate_1.webp" height="350"> <img src="images\BasePlate_2.webp" height="350">

__Camera Stand__

Camera Stand components were designed in a way that it's an adjustable angle and height This design feature offers versatility and adaptability, ensuring optimal positioning of the camera to capture desired perspectives and accommodate various environments or setups.

<img src="images\Camera_Stand_1.webp" height="160"> <img src="images\Camera_Stand_2.webp" height="160"><br>
<img src="images\Camera_Stand_3.webp" height="350">

__GPS Plate__

<img src="images\GPS_Plate.webp" height="300">

__Circuit Diagram__

Our team made use of a select range of electronic components, primarily focusing on the OAK-D Lite camera, Jetson NANO, a GNSS board / GPS, and an additional Seeed Studio XIAO nRF52840 Sense (for IMU usage).
Our circuit assembly process was guided by a circuit diagram provided by our class TAs.

<img src="images\circuitDiagram.PNG" height="300">

<hr>

## Gantt Chart
<div align="center">
    <img src="images\gantt_chart.webp" height="500">
</div>
<hr>

## Course Deliverables
Here are our autonomous laps as part of our class deliverables:

* DonkeyCar Reinforcement Laps: https://youtu.be/UEGGQz-GSq4
* Line Following: https://youtu.be/GaKq_m8Ola0
* Lane Following: https://youtu.be/1v2-Dgx5fyk
* GPS Laps: https://youtu.be/92Q-JpYGPZk?si=UYrh6Mo9-b4TGgYO

Team 7's the weekly project Status Update and Final Presentation:  
* [Team 7 weekly status updates](https://docs.google.com/presentation/d/e/2PACX-1vSWm0AW0yZ6IKFCnXcJtbBB0NPDEejXtwTStLtW3yOxjlFvpV0wWUp3y91MQgVq3j63RR5WNTfaSFZW/pub?start=false&loop=false&delayms=3000)
* [Team 7 Final Presentation](https://docs.google.com/presentation/d/e/2PACX-1vRGnL11PP4RDo87JKWF-kLgD4dVyRBdL_eSWTUIe0eLQumJOI_wawX6sBa7MOMksFe8tPUjdFZBWRRE/pub?start=false&loop=false&delayms=3000)
<hr>

## Project Reproduction
If you are interested in reproducing our project, here are a few steps to get you started with our repo:

<ol>
  <li>Follow instuctions on <a href="https://docs.google.com/document/d/1YS5YGbo8evIo9Mlb0J-w2r3bZfju37Zl4UmdaN2CD2A/">UCSD Robocar Framework Guidebook</a>, <br> pull <code>devel</code> image on your JTN: <code>docker pull djnighti/ucsd_robocar:devel</code></li>
  <li>
      <code>sudo apt update && sudo apt upgrade</code><br>
      (make sure you upgrade the packages, or else it won't work; maybe helpful if you run into some error <url>https://askubuntu.com/questions/1433368/how-to-solve-gpg-error-with-packages-microsoft-com-pubkey</url>)<br>
      check if <code>slam_toolbox</code> is installed and launchable:<br>
<pre>
sudo apt install ros-foxy-slam-toolbox
source_ros2
ros2 launch slam_toolbox online_async_launch.py
</pre>
      Output should be similar to:
<pre>
[INFO] [launch]: All log files can be found below /root/.ros/log/2024-03-16-03-57-52-728234-ucsdrobocar-148-07-14151
[INFO] [launch]: Default logging verbosity is set to INFO
[INFO] [async_slam_toolbox_node-1]: process started with pid [14173]
[async_slam_toolbox_node-1] 1710561474.218342 [7] async_slam: using network interface wlan0 (udp/192.168.16.252) selected arbitrarily from: wlan0, docker0
[async_slam_toolbox_node-1] [INFO] [1710561474.244055467] [slam_toolbox]: Node using stack size 40000000
[async_slam_toolbox_node-1] 1710561474.256172 [7] async_slam: using network interface wlan0 (udp/192.168.16.252) selected arbitrarily from: wlan0, docker0
[async_slam_toolbox_node-1] [INFO] [1710561474.517037334] [slam_toolbox]: Using solver plugin solver_plugins::CeresSolver
[async_slam_toolbox_node-1] [INFO] [1710561474.517655574] [slam_toolbox]: CeresSolver: Using SCHUR_JACOBI preconditioner.
</pre>
  </li>
  <li>
      Since we upgrade all existing packges, we need to rebuild VESC pkg under <code>/home/projects/sensor2_ws/src/vesc/src/vesc</code><br>
<pre>
cd /home/projects/sensor2_ws/src/vesc/src/vesc
git pull
git switch foxy
</pre><br>
      make sure you are on foxy branch
      <img src="https://github.com/WinstonHChou/winter-2024-final-project-team-7/assets/68310078/10398bc9-f546-497e-8e5f-9f380b39e018)"/><br>
      Then, build 1st time under <code>sensor2_ws/src/vesc/src/vesc</code><br>
<pre>
colcon build
source install/setup.bash
</pre>
      Then, 2nd time but under <code>sensor2_ws/src/vesc</code><br>
<pre>
cd /home/projects/sensor2_ws/src/vesc
colcon build
source install/setup.bash
</pre>
      Now, try <code>ros2 pkg xml vesc</code>, check if VESC pkg version has come to <code>1.2.0</code><br>
  </li>
  <li>
      Install <b>Navigation 2</b> package, and related packages:<br>
      <code>sudo apt install ros-foxy-navigation2 ros-foxy-nav2* ros-foxy-robot-state-publisher ros-foxy-joint-state-publisher</code>
  </li>
  <li>
      <b>Clone</b> this repository, 
<pre>
cd /home/projects/ros2_ws/src
git clone https://github.com/WinstonHChou/winter-2024-final-project-team-7.git
cd winter-2024-final-project-team-7/
</pre>
      There a <code>Replace_to_ucsd_robocar_nav2</code> folder, which includes several files you'd like to replace/place to <code>ucsd_robocar_nav2_pkg</code><br>
      <ol>
          <li><code>scan_correction.yaml</code>, <code>mapper_params_online_async.yaml</code>, <code>node_config.yaml</code>, <code>node_pkg_locations_ucsd.yaml</code><br>should be placed to <code>/home/projects/ros2_ws/src/ucsd_robocar_hub2/ucsd_robocar_nav2_pkg/config/</code></li>
          <li><code>sensor_visualization.rviz</code><br>should be placed to <code>/home/projects/ros2_ws/src/ucsd_robocar_hub2/ucsd_robocar_nav2_pkg/rviz/</code></li>
          <li><code>ucsdrobocar-148-07.urdf</code><br>should be placed to <code>/home/projects/ros2_ws/src/ucsd_robocar_hub2/ucsd_robocar_nav2_pkg/urdf/</code><br>(you can edit URDF if you want to, <url>https://docs.ros.org/en/foxy/Tutorials/Intermediate/URDF/URDF-Main.html</url>)</li>
          <li><code>urdf_publisher_launch.launch.py</code><br>should be placed to <code>/home/projects/ros2_ws/src/ucsd_robocar_hub2/ucsd_robocar_nav2_pkg/launch/</code></li>
          <li><code>package.xml</code><br>should be placed to <code>/home/projects/ros2_ws/src/ucsd_robocar_hub2/ucsd_robocar_nav2_pkg/</code></li>
      </ol><br>
      Next, modify <code>setup.py</code> in <code>/home/projects/ros2_ws/src/ucsd_robocar_hub2/ucsd_robocar_nav2_pkg/</code>,<br>
      and add <code>(os.path.join('share', package_name, 'urdf'), glob('urdf/*.urdf'))</code><br>
      Then,
<pre>
build_ros2
ros2 launch ucsd_robocar_nav2_pkg all_nodes.launch.py
</pre>If <b>functional</b>, pre-setting for SLAM is done. Note: <b>scan_correction</b> and <b>urdf_publisher</b> nodes are now able to be launch by <code>all_nodes.launch.py</code>. Remember to toggle settings for them <code>node_config.yaml</code>.<br>
      <ul> 
          <li><code>scan_correction.yaml</code> can define the lidar undesired range, and filter them out using <code>scan_correction</code> node</li>
          <li>Follow this instuction if you <b>only want to do SLAM</b>, <a href="https://youtu.be/ZaiA3hWaRzE?si=heDZifDYEvBQl7yD"/>Easy SLAM Instruction Video on ROS 2 Foxy</a></li>
          <li>Since you might adjust setting of VESC pkg for <b>vesc_odom</b>, here's additonal resource <a href="https://f1tenth.readthedocs.io/en/foxy_test/getting_started/driving/drive_calib_odom.html#calibrating-the-steering-and-odometry"/>f1tenth calibrating VESC Odom</a></li>
          <li>Change odom direction by
              <ul> 
                  <li>
                      adjust <code>vesc_to_odom.cpp</code> <code>line 100</code><br>
                      <code>double current_speed = -1 * (-state->state.speed - speed_to_erpm_offset_) / speed_to_erpm_gain_;</code> (adding a negative sign)
                  </li>
                  <li>
                      adjust <code>vesc_to_odom.cpp</code> <code>line 107</code>(if you invert steering_angle at joy_teleop.yaml)<br>
                      <code>-1 * (last_servo_cmd_->data - steering_to_servo_offset_) / steering_to_servo_gain_;</code> (adding a negative sign)
                  </li>
              </ul>
          </li>
          <li>If you made changes in <code>vesc_to_odom.cpp</code>, must repeat <b>Step. 3 to rebuild VESC pkg</b></li>
      </ul>
  </li>
  <li> Setting up <b>Seeed IMU</b>, follow instructions 
      <ul> 
          <li><a href="https://wiki.seeedstudio.com/XIAO_BLE/"/>Seeed Seeed Studio XIAO nRF52840 Sense</a></li> 
          <li><a href="https://github.com/NikitaB04/razorIMU_9dof"/>razorIMU_9dof</a></li> 
      </ul>
      In <code>src/winter-2024-final-project-team-7/team_7_external/config/</code>,you may adjust setting in <code>Seeed_imu.yaml</code> (<b>equivalent</b> for <code>razor.yaml</code> in razorIMU_9dof) and <code>Seeed_imu_config.yaml</code>.<br>
      Then, 
<pre>
build_ros2
ros2 launch team_7_external Seeed_imu.launch.py
</pre>
  </li>
  <li> <b>DepthAI ROS & team_7_obstacle_detection Installation</b>
    <ol>
      <li>Install Depthai and related packages,<br><code>sudo apt install ros-foxy-depthai* ros-foxy-sensor-msgs-py</code></li>
      <li>If you're using an OAK-D Lite,
          <ul>
              <li>adjust <code>camera.yaml</code>,<br><code>nano /opt/ros/foxy/share/depthai_ros_driver/config/camera.yaml</code><br>Disable imu and ir<br><br><img src="https://github.com/WinstonHChou/winter-2024-final-project-team-7/assets/68310078/aff6c5af-6798-4a3a-9db8-c4d04e6da298" width="300"></li>
              <li>adjust <code>pcl.yaml</code>,<br><code>nano /opt/ros/foxy/share/depthai_ros_driver/config/pcl.yaml</code><br>Disable imu and ir, and comment out "oak:"<br><br><img src="https://github.com/WinstonHChou/winter-2024-final-project-team-7/assets/68310078/d4ec90b2-f20f-46f5-8474-c70a546a5cb5" height="200"></li>
          </ul>
      </li>                  
      <li>Open an additional terminal, <br><code>ros2 launch depthai_ros_driver pointcloud.launch.py</code> to publish <code>/oak/points</code> ros 2 topic.</li>
      <li>Open an additional terminal, <br><code>ros2 launch team_7_obstacle_detection obstacle_detection.launch.py</code>. Now, you are able to detect a simple obstacle using height < 2 meters. (<b>Adjustable</b> in the launch file)</li>
    </ol>
  </li>
  <li>
      <b>Foxglove Studio</b>, using rosbridge_server<br>
      Download <a href="https://foxglove.dev/download">Foxglove Studio</a>. And Follow instructions <url>https://docs.foxglove.dev/docs/introduction/</url>
  </li>
</ol>

That's it! Most of settings are above. If you need any assistance on how to utilize this repo, you may create new issue on this GitHub repo, or contact w3chou@ucsd.edu if needed.

<hr>

## Acknowledgements
Special thanks to Professor Jack Silberman and TA Arjun Naageshwaran for delivering the course!  
Thanks to Raymond on Triton AI giving suggestions on our project!  
Thanks to Nikita on Triton AI providing support on razorIMU_9dof repo for IMU usage!

**Programs Reference:**
* [UCSD Robocar Framework](https://gitlab.com/ucsd_robocar2)
* [Slam Toolbox](https://github.com/SteveMacenski/slam_toolbox.git)
* [DepthAI_ROS_Driver](https://github.com/luxonis/depthai-ros)
* [razorIMU_9dof](https://github.com/NikitaB04/razorIMU_9dof)
* [Foxglove Studio](https://app.foxglove.dev/)


README.md Format, reference to [spring-2023-final-project-team-5](https://github.com/UCSD-ECEMAE-148/spring-2023-final-project-team-5)

<hr>

## Contacts

* Winston Chou - w3chou@ucsd.edu | winston.ckhs@gmail.com | [LinkedIn](https://www.linkedin.com/in/winston-wei-han-chou-a02214249/)
* Amir Riahi - amirriahi760@yahoo.com
* Rayyan Khalid - rkhalid@ucsd.edu