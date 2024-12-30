# ROS-based-autonomous-navigation-and-excavation-control-for-excavators  
## 环境安装
### 1.ros
https://wiki.ros.org/melodic/Installation/Ubuntu 
### 2.TBB
参考 https://blog.csdn.net/Twilightzr/article/details/126533557 
git clone https://github.com/oneapi-src/oneTBB
git checkout v2020.1
cd oneTBB_202001
cmake -DTBB_ROOT=/home/weiding/oneTBB-2020.1 -DTBB_OS=Linux -P cmake/tbb_config_generator.cmake
cd oneTBB_202001
make
cd build
sudo chmod +x *.sh
sh generate_tbbvars.sh
sh tbbvars.sh
# 在TBB源码目录下
cd oneTBB_202001/build
cd linux_intel64_gcc_cc5.5.0_libc2.31_kernel5.11.0_release #该目录根据系统gcc版本和kernal版本自动生成
sudo cp *.so /usr/local/lib #或者/usr/lib
sudo cp *.so.2 /usr/local/lib #或者/usr/lib
sudo /sbin/ldconfig
cd include
sudo cp -rf ./* /usr/local/include
cd cmake
sudo mkdir TBB
sudo cp TBBConfig.cmake  TBBConfigVersion.cmake /usr/local/lib/cmake/TBB/.
### 3.GTSAM
参考  https://blog.csdn.net/2301_79970562/article/details/136237507
sudo apt-get install cmake
sudo apt-get install cmake
sudo apt-get install libtbb-dev
sudo apt-get install intel-mkl-full
git clone https://bitbucket.org/gtborg/gtsam.git
cd ~/gtsam 
mkdir build
cd build
cmake ..
sudo  make install
## catkin_ws工作空间下的各功能包使用、功能说明
### 1.controller_manager
控制功能包。此功能为对挖掘机进行控制的基础。  
### 2.pudong
模型功能包。用于存放挖掘机的基础模型。  
### 3.pudong_gazebo
带有gazebo借口、算法和可执行程序的功能包。此功能包是本次项目设计的主要部分，包含挖掘环境、机械臂控制、指定导航点位脚本以及挖掘动作控制脚本等重要文件。  
### 4.pudong_moveit
机械臂控制功能包。此功能包用于对挖掘机的机械臂进行控制，在使用过程中注意关节其接口要与pudong_gazebo中关节相对应。  
### 5.mbot_teleop
键盘控制节点功能包。运行此功能包下launch文件，可以通过键盘控制挖掘机，从而完成建图。  
### 6.mbot_navigation
建图导航功能包。此功能包下的gmmapping.launch用于部署建图算法，nav_cloister_demo.launch用于进行导航。config下的mbot文件夹下的配置文件是导航算法的参数配置，可以根据实际情况进行调节。  
### 7.velodyne_description\velodyne_gazebo_plugins\velodyne_simulator
雷达仿真功能包。此功能包从官网获取，用来配置激光雷达，进行雷达仿真。  
### 8.LIO-SAM-master
三维建图功能包。成功安装此功能包后可以观察到所处环境的三维扫描图。  
#### 建图命令：  
roslaunch pudong_gazebo model_spawn.launch  
roslaunch pudong_gazebo joint_state_node.launch  
roslaunch pudong_gazebo moveit_excution.launch  
roslaunch pudong_gazebo pointcloud_to_laserscan.launch  
roslaunch pudong_gazebo rviz_slam.launch  
rosrun pudong_gazebo guding_cswj.py  
roslaunch mbot_navigation gmapping.launch  
roslaunch mbot_teleop mbot_teleop.launch  
#### 导航命令：  
roslaunch pudong_gazebo model_spawn.launch   
roslaunch pudong_gazebo joint_state_node.launch  
roslaunch pudong_gazebo moveit_excution.launch  
rosrun pudong_gazebo guding_cswj.py  
roslaunch mbot_navigation nav_cloister_demo.launch  
#### 整体仿真运行说明  
roslaunch pudong_gazebo model_spawn.launch   
roslaunch pudong_gazebo joint_state_node.launch  
roslaunch pudong_gazebo moveit_excution.launch  
roslaunch mbot_navigation nav_cloister_demo.launch  
rosrun pudong_gazebo number_statistic.py  
rosrun pudong_gazebo reconstructed_excavator_control.py  
#### MATLAB  
MATLAB程序在pudong_gazebo/scripts/MATLAB内  
