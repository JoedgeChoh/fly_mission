# README
## 1. 介绍
本repo通过mavsdk库向无人机模型发布任务指令，配置文件保存在config文件中

## 2. 应用
(1) 启动gazebo:
$ roslaunch px4 out3.launch
(2) 启动QGC
(3) 启动本repo
$ mkdir build && cd build 
$ cmake .. && make install
$ cd .. && ./fly_misson udp://:14030 config_raceway.yaml
