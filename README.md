You can Download the Source file from below D-link. 
https://drive.google.com/drive/u/1/folders/1mJvreppxEcgUzITCHb9a_fVgvYxyoQ7Z

All the testing and simulation done with these environment
System support:-
1. Ubuntu 22.04.5 LTS
2. Humble
3. ROS 2 

**Once extract all the file from above link with same system support. Just go with below prompt for launching the Vision Based Quadruped robot. **
**Terminal 1:- Now Gazebo will open and you see robot model in it.**
source /opt/ros/humble/setup.bash
source ~/go2_ws/install/setup.bash
ros2 launch go2_config gazebo.launch.py
<img width="534" height="291" alt="Screenshot from 2026-04-18 14-36-42" src="https://github.com/user-attachments/assets/4060f643-cd73-4d7e-a1b2-3af4a0a8ea43" />

**Terminal 2:- Control motion of robot using keyboard, After this commond Press "i" in terminal itself to see robot in farword motion.** 
source /opt/ros/humble/setup.bash
source ~/go2_ws/install/setup.bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard

**Terminal 3:- If you don't see the world in the pop window. just drop and select the raw image in it.**
source /opt/ros/humble/setup.bash
source ~/go2_ws/install/setup.bash
ros2 run ros_gz_bridge parameter_bridge \
/front_camera/image@sensor_msgs/msg/Image[ignition.msgs.Image \
/front_camera/camera_info@sensor_msgs/msg/CameraInfo[ignition.msgs.CameraInfo

**Terminal 4:-**
source /opt/ros/humble/setup.bash
source ~/go2_ws/install/setup.bash
ros2 run rqt_image_view rqt_image_view
<img width="673" height="692" alt="Screenshot from 2026-04-12 11-36-36" src="https://github.com/user-attachments/assets/4a81d78b-f2cf-4063-b73f-41e8ea87a5c2" />

**Terminal 5:- Vision start**
source /opt/ros/humble/setup.bash
source ~/go2_ws/install/setup.bash
ros2 launch go2_vision vision.launch.py

** Terminal 6:-**
source /opt/ros/humble/setup.bash
source ~/go2_ws/install/setup.bash
ros2 run go2_vision terrain_detector

**Terminal 7:-**
source /opt/ros/humble/setup.bash
source ~/go2_ws/install/setup.bash
ros2 topic echo /vision/terrain

**Terminal 8:- It will pop up the vision terrain classification window**
source /opt/ros/humble/setup.bash
source ~/go2_ws/install/setup.bash
ros2 run go2_vision vision_node --ros-args -p input_topic:=/front_camera/image
<img width="775" height="713" alt="Screenshot from 2026-04-21 11-59-49" src="https://github.com/user-attachments/assets/c3264052-0a42-4d54-9af2-54421e02bce3" />
<img width="594" height="441" alt="Screenshot from 2026-04-22 14-48-34" src="https://github.com/user-attachments/assets/1f64ba4d-3de4-4fa3-8334-9377922e9e97" />


**Terminal 9:- We can see the live terrain dataset in this terminal**
source /opt/ros/humble/setup.bash
source ~/go2_ws/install/setup.bash
ros2 topic echo /vision/detections

**Terminal 10: Start Autonomous adaptive gait control motion**
source /opt/ros/humble/setup.bash
source ~/go2_ws/install/setup.bash
python3 /home/rai/go2_ws/src/terrain_adaptive_controller.py
source /opt/ros/humble/setup.bash
source ~/go2_ws/install/setup.bash
python3 ~/go2_ws/src/go2_vision/scripts/capture_images.py
{it will use to capture the image for model dataset terraining }

**If we see multiple robots in gazebo while launching it again and again run this**
pkill -9 ign
pkill -9 gzserver
pkill -9 gzclient
rm -rf /dev/shm/fastdds*
source /opt/ros/humble/setup.bash
cd ~/go2_ws
rm -rf build install log
colcon build --symlink-install
source install/setup.bash
