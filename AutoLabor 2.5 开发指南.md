# Autolabor 2.5 开发指南

标签：ROS Autolabor2.5
---

## **目标：以Autolabor2.5为范例，学习基于ROS系统的机器人底盘设计方法**

### 范例1：[将ROS应用于机器人项目开发-古月居][1]
### 范例2：[Getting Starting with Autonomous Robots in ROS via Simulations][16]（可能需要翻墙）
> 
Our code simulates a differential drive robot that navigates autonomously in ROS. The write-ups are split into three sections:
Part 1: Create a Gazebo model that is compatible with ROS.
Part 2: Add necessary exteroceptive sensors
Part 3: Enable autonomous navigation

注意：开始之前，请保证已安装Ubuntu16.04，并安装ROS Kinetic！！

## 1. 获取Autolabor文档与资料
[Autolabor2.5官网使用文档][2]   包括：
> * 零件
> * 产品组装指南
> * 初始配置方法
> * App控制方法与一键建图
> * SSH远程连接方法

在官网上，同样可以查到：
> * 产品图片
> * 机械结构
> * 硬件架构
> * 软件框架图
> * 功能示意图

其他代码与文档
> * [软件下载][3]
> * [源代码下载][4]

## 2. 熟悉ROS

如果没有ROS基础，可以先听下面的网课，并尝试调试网课自带的代码包

>[ROS机器人操作系统入门-中国大学MOOC][5]
>[课程讲义（不稳定，可能需要翻墙）][6]
>[课程配套代码包-GitHub][7]


预期掌握的知识点包括：
> * ROS操作系统及意义
> * ROS的安装与配置
> * catkin_ws
> * package
> * topic & msg
> * service & srv
> * parameter server
> * action
> * Gazebo
> * Rviz
> * Rqt
> * 通信方式的编写
> * tf，urdf
> * SLAM & Gmapping
> * Navigation Stack
> * move_base
> * costmap
> * ACML

>参考来源：

> * [ROS探索总结-古月居][8]
> * [ROS机器人操作系统相关书籍、资料和学习路径][9]
> * [ROS官方提供的书籍列表][10]
> * [Programming Robots with ROS（E-book)][11]

## 3. ROS Basic
## 4. ROS Perception
## 5. ROS Navigation
## 6. 硬件设计
### 电机选型；主控板原理；PID控制；下位机代码编写；上下位机通讯，上位机设计
[autolabor开源ros机器人笔记：硬件结构][12]
[ROS探索总结（三十一）——ros_control][13]
## 7. 实车建图与调试

[autolabor2.5入门教程-SLAM导航][14]
[官网视频][15]

### 8*. ROS Manipulation


  [1]: http://www.guyuehome.com/2120
  [2]: http://www.autolabor.com.cn/usedoc/autolabor2_5/radarVersion
  [3]: http://www.autolabor.com.cn/download
  [4]: https://download-autolabor-1255388470.cos.ap-beijing.myqcloud.com/File/Autolabor2.5%E8%B5%84%E6%96%99.zip
  [5]: https://www.bilibili.com/video/av24585414?from=search&seid=3793999139419634004
  [6]: https://sychaichangkun.gitbooks.io/ros-tutorial-icourse163/content/
  [7]: https://github.com/sychaichangkun/ROS-Academy-for-Beginners
  [8]: http://www.guyuehome.com/column/ros-explore
  [9]: https://zhuanlan.zhihu.com/p/30391098
  [10]: http://wiki.ros.org/Books
  [11]: https://b-ok.cc/book/2577773/f02462
  [12]: https://blog.csdn.net/fantasysolo/article/details/80178681
  [13]: http://www.guyuehome.com/tag/ros_control
  [14]: https://www.ncnynl.com/archives/201904/2995.html
  [15]: http://www.autolabor.com.cn/lib
  [16]: http://moorerobots.com/blog/post/6