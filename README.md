1. build px4 sitl firmware
- cd ~
- git clone https://github.com/PX4/PX4-Autopilot.git
- cd ~/PX4-Autopilot
- git checkout -b simulation_test v1.12.3
- ./Tools/setup/ubuntu.sh
- git submodule update --init --recursive
- make px4_sitl

2. build ros package
- mkdir ~/catkin_ws/src
- cd ~/catkin_ws/src
- git clone https://MAD-CRAZY-MAN/precland
- cd ~/catkin_ws/
- catkin_make

3. set environment varibale
- vim ~/.bashrc 
export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH:~/catkin_ws/src/precland/models
export px4_dir=~/PX4-Autopilot
source $px4_dir/Tools/setup_gazebo.bash $px4_dir $px4_dir/build/px4_sitl_default
export ROS_PACKAGE_PATH=${ROS_PACKAGE_PATH}:$px4_dir

4. roslaunch precland_simul mavros_posix_sitl.launch
- QGC 실행
- rostopic list //topic 확인
- rviz //camera 확인 

5. 움직이기
- example code 실행
    - chmod +x ~/catkin_ws/src/precland/scripts/offb_node
    - rosrun precland_simul offb_node