# micro-ROS Agent
(Agent)本身是”代理“或者“网桥”的意思，是运行在PC（树莓派等）上的一个ROS节点，充当ESP32和ROS2生态之间的桥梁
```txt
┌────────────────────┐         WiFi/UDP          ┌─────────────────────┐
│   ESP32 (FishBot)  │ ◄──────────────────────►   │   PC (ROS 2 Host)  │
│                    │     port 8888              │                     │
│  micro-ROS Client  │                            │  micro-ROS Agent    │
│  (订阅 cmd_vel      │                            │  (ros2 run          │
│   发布 odom)        │                            │   micro_ros_agent)  │
└────────────────────┘                           └─────────────────────┘
                                                           │
                                                    ┌──────┴──────┐
                                                    │  ROS 2 网络  │
                                                    │ (其他节点)    │
                                                    └─────────────┘

```
PC端运行`ros2 run micro_ros_agent micro_ros_agent udp4 --port 8888`
使用udp4和esp32在8888端口创建连接
Linux使用`ip addr`查看当前ip地址

# DDS
