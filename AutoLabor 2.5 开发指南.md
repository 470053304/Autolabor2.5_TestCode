# AutoLabor 2.5 开发指南

标签：ROS AutoLabor2.5

---

## **目标：以AutoLabor2.5为范例，学习基于ROS系统的机器人底盘设计方法**

注意：开始之前，请保证已安装Ubuntu16.04，并安装ROS Kinetic！！

## 1. 获取AutoLabor文档与资料
[AutoLabor2.5官网使用文档][1]   包括：
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

## 2. 熟悉ROS

如果没有ROS基础，可以先听下面的网课，并尝试调试网课自带的代码包
[ROS机器人操作系统入门-中国大学MOOC][2]
[课程讲义（不稳定，可能需要翻墙）][3]
[课程配套代码包-GitHub][4]


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

### **知识体系为：**

### ROS Basic
### ROS Perception
### ROS Navigation
### ROS Manipulation
参考来源：
* [ROS探索总结-古月居][5]
* [ROS机器人操作系统相关书籍、资料和学习路径][6]
* [ROS官方提供的书籍列表][7]
* [Programming Robots with ROS（E-book)][8]

## 3. 硬件设计

### 电机选型；主控板原理；PID控制；下位机代码编写；上下位机通讯，上位机设计

## 4. Locomotion

### 激光雷达的原理，型号，使用现状与方法 SLAM算法

## 5. 在ROS上完成建图仿真
[使用urdf建立ROS机器人Autolabor2.5机器人模型][9]

## 6. 实车建图
[autolabor2.5入门教程-SLAM导航][10]


  [1]: http://www.autolabor.com.cn/usedoc/autolabor2_5/radarVersion
  [2]: https://www.bilibili.com/video/av24585414?from=search&seid=3793999139419634004
  [3]: https://sychaichangkun.gitbooks.io/ros-tutorial-icourse163/content/
  [4]: https://github.com/sychaichangkun/ROS-Academy-for-Beginners
  [5]: http://www.guyuehome.com/column/ros-explore
  [6]: https://zhuanlan.zhihu.com/p/30391098
  [7]: http://wiki.ros.org/Books
  [8]: https://b-ok.cc/book/2577773/f02462
  [9]: https://blog.csdn.net/autolabor/article/details/85097679
  [10]: https://www.ncnynl.com/archives/201904/2995.html