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

[ROS机器人操作系统入门-中国大学MOOC][2]
掌握知识点包括：
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

## 3. 硬件设计

### 电机选型；主控板原理；PID控制；下位机代码编写；上下位机通讯，上位机设计

## 4. Locomotion

### 激光雷达的原理，型号，使用现状与方法 SLAM算法

## 5. 在ROS上完成建图仿真
[使用urdf建立ROS机器人Autolabor2.5机器人模型][3]

## 6. 实车建图
[autolabor2.5入门教程-SLAM导航][4]


  [1]: http://www.autolabor.com.cn/usedoc/autolabor2_5/radarVersion
  [2]: https://www.bilibili.com/video/av24585414?from=search&seid=3793999139419634004
  [3]: https://blog.csdn.net/autolabor/article/details/85097679
  [4]: https://www.ncnynl.com/archives/201904/2995.html