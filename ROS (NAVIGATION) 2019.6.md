# ROS (NAVIGATION) 2019.6

标签（空格分隔）： 未分类

---
## 建图，定位与路径规划

机器人研究的问题包含许许多多的领域，我们常见的几个研究的问题包括：建图(Mapping)、定位(Localization)和路径规划（Path Planning），如果机器人带有机械臂，那么运动规划（Motion Planning）也是重要的一个环节。而同步定位与建图（SLAM）问题位于定位和建图的交集部分。
SLAM需要机器人在未知的环境中逐步建立起地图，然后根据地区确定自身位置，从而进一步定位。

![此处输入图片的描述][1]

## Navigation Stack
Navigation Stack是一个ROS的metapackage，里面包含了ROS在路径规划、定位、地图、异常行为恢复等方面的package，其中运行的算法都堪称经典。Navigation Stack的主要作用就是路径规划，通常是输入各传感器的数据，输出速度。一般我们的ROS都预装了Navigation。

[ros-planning/navigation GitHub][2]

![此处输入图片的描述][3]

上图中位于导航功能正中心的是move_base节点，可以理解为一个强大的路径规划器，在实际的导航任务中，你只需要启动这一个node，并且给他提供数据，就可以规划出路径和速度。 move_base之所以能做到路径规划，是因为它包含了很多的插件，像图中的白色圆圈global_planner、local_planner、global_costmap、local_costmap、recovery_behaviors。这些插件用于负责一些更细微的任务：全局规划、局部规划、全局地图、局部地图、恢复行为。而每一个插件其实也都是一个package，放在Navigation Stack里。

## move_base
move_base算得上是Navigation中的核心节点，之所以称之为核心，是因为它在导航的任务中处于支配地位，其他的一些package都是它的插件。

![此处输入图片的描述][4]

* base_local_planner: 
实现了**Trajectory Rollout**和**DWA**两种局部规划算法
* dwa_local_planner: 
实现了DWA局部规划算法，可以看作是base_local_planner的改进版本
* parrot_planner: 
实现了较简单的全局规划算法
* navfn: 
实现了**Dijkstra**和**A***全局规划算法
* global_planner:
重新实现了Dijkstra和A*全局规划算法,可以看作navfn的改进版

> * [DWA算法分析][5]
> * [ROS源码解读(一)--局部路径规划][6]
> * [最短路径问题---Dijkstra算法详解][7]
> * [A星算法详解][8]

## costmap

在实际的导航任务中，光有一张地图是不够的，机器人需要能动态的把障碍物加入，或者清楚已经不存在的障碍物，有些时候还要在地图上标出危险区域，为路径规划提供更有用的信息。

因为导航的需要，所以出现了代价地图。你可以将代价地图理解为，在/map之上新加的另外几层地图，不仅包含了原始地图信息，还加入了其他辅助信息。

代价地图有以下特点：

* 代价地图有两张，一张是local_costmap，一张是global_costmap，分别用于局部路径规划器和全局路径规划器，而这两个costmap都默认并且只能选择costmap_2d作为插件。
* 无论是local_costmap还是global_costmap，都可以配置他们的Layer，可以选择多个层次。costmap的Layer包括以下几种：
> * Static Map Layer：静态地图层，通常都是SLAM建立完成的静态地图。
> * Obstacle Map Layer：障碍地图层，用于动态的记录传感器感知到的障碍物信息。
> * Inflation Layer：膨胀层，在以上两层地图上进行膨胀（向外扩张），以避免机器人的外壳会撞上障碍物。
> * Other Layers：还可以通过插件的形式自己实现costmap，目前已有Social Costmap Layer、Range Sensor Layer等开源插件。

## AMCL
Adaptive Mentcarto Localization(AMCL)，蒙特卡洛自适应定位是一种很常用的定位算法，它通过比较检测到的障碍物和已知地图来进行定位。

> 更多：[机器人粒子滤波定位（蒙特卡罗定位）][9]

AMCL上的通信架构如上图所示，与之前SLAM的框架很像，最主要的区别是/map作为了输入，而不是输出，因为AMCL算法只负责定位，而不管建图。 

![此处输入图片的描述][10]

## 使用Autolabor2.5完成路径规划与导航仿真





  [1]: https://sychaichangkun.gitbooks.io/ros-tutorial-icourse163/content/pics/slam.png
  [2]: https://github.com/ros-planning/navigation
  [3]: https://sychaichangkun.gitbooks.io/ros-tutorial-icourse163/content/pics/navigation.png
  [4]: https://sychaichangkun.gitbooks.io/ros-tutorial-icourse163/content/pics/move_base.jpg
  [5]: https://blog.csdn.net/u013158492/article/details/50512900
  [6]: https://blog.csdn.net/xmy306538517/article/details/78772066
  [7]: https://blog.csdn.net/qq_35644234/article/details/60870719
  [8]: https://blog.csdn.net/hitwhylz/article/details/23089415
  [9]: https://www.cnblogs.com/21207-iHome/p/5237701.html
  [10]: https://sychaichangkun.gitbooks.io/ros-tutorial-icourse163/content/pics/amcl.JPG
  [11]: http://moorerobots.com/blog/post/6