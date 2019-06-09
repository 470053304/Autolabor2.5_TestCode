# ROS (PERCEPTION) 2019.6

标签（空格分隔）： 未分类

---
传感器是机器人用于感知周围世界的载体。作为机器人操作系统，ROS对很多种类的传感器（如摄像头，深度摄像头，激光雷达，IMU，里程计，超声红外传感器等）提供支持。
[ROS Sensors Wiki][1]
[ROS Perception GitHub][2]

Autolabor2.5小车上安装的是思岚科技的rplidar a1，本节以激光雷达为例。

[rplidar a1 下载与支持][3]，包括
> * ROS package
* SDK与固件
* 通讯协议


## 激光雷达原理

![此处输入图片的描述][4]

激光雷达是一种雷达系统，是一种主动传感器，所形成的数据是点云形式。其工作光谱段在红外到紫外之间，主要发射机、接收机、测量控制和电源组成。工作原理为：首先向被测目标发射一束激光，然后测量反射或散射信号到达发射机的时间、信号强弱程度和频率变化等参数，从而确定被测目标的距离、运动速度以及方位。除此之外，还可以测出大气中肉眼看不到的微粒的动态等情况。激光雷达的作用就是精确测量目标的位置（距离与角度）、形状（大小）及状态（速度、姿态），从而达到探测、识别、跟踪目标的目的。

从技术原理来看，激光雷达的类型主要有两种：旋转式激光雷达、固态激光雷达。

## 主要应用领域
激光技术从它的问世到现在，虽然时间不长，但是由于它有：高亮度性、高方向性、高单色性和高相干性等几个极有价值的特点，因而在国防军事、工农业生产、医学卫生和科学研究等方面都有广泛的应用。LiDAR技术在西方国家发展相对成熟，已经投入商业运行的激光雷达系统（主要指机载）主要有Optech（加拿大）、TopSys（法国）和Leica（美国）等公司的产品。

激光雷达的应用领域核心是扫地机器人、AVG小车、汽车自动驾驶、无人驾驶、空间测绘和无人机等领域。从目前全球激光雷达企业的下游应用领域分布来看，居多的仍然是智能汽车和机器人领域。

> 参考资料：
[激光雷达深度剖析][5]

## 基于Autolabor Simulation完成建图

### 栅格地图

![此处输入图片的描述][6]

ROS中的地图很好理解，就是一张普通的灰度图像，通常为pgm格式。这张图像上的黑色像素表示障碍物，白色像素表示可行区域，灰色是未探索的区域。

在SLAM建图的过程中，可以在RViz里看到一张地图被逐渐建立起来的过程，类似于一块块拼图被拼接成一张完整的地图。这张地图对于我们定位、路径规划都是不可缺少的信息。事实上，地图在ROS中是以Topic的形式维护和呈现的，这个Topic名称就叫做/map，它的消息类型是nav_msgs/OccupancyGrid

### Gmapping
Gmapping算法是目前基于激光雷达和里程计方案里面比较可靠和成熟的一个算法，它基于粒子滤波，采用RBPF的方法效果稳定，许多基于ROS的机器人都跑的是gmapping_slam。

> 更多：[基于粒子滤波的SLAM(GMapping)算法分析][7]

这个软件包位于ros-perception组织中的slam_gmapping仓库中。 其中的slam_gmapping是一个metapackage，它依赖了gmapping，而算法具体实现都在gmapping软件包中，该软件包中的slam_gmapping程序就是我们在ROS中运行的SLAM节点。

![][8]

### 仿真建图

[Autolabor Simulation GitHub][9]
依照教程完成下载和编译

该项目提供了许多编写好的launch file供使用者调用，他们展示了模拟器内各个组件不同的设置， 以及模拟器与其他ROS工具（例如Navigtation Stack，gmapping）配合的示例

**运行一个 autolabor_simulation_base 模拟，并且使用键盘控制机器人：**
```
# Please make sure you have sourced the devel/setup.bash file
roslaunch simulation_launch minimal_bringup.launch

# open a new terminal and source the devel/setup.bash file again
rosrun autolabor_simulation_base autolabor_teleop.py /autolabor_teleop/cmd_vel:=/cmd_vel
```
**完成建图：**
```
$ roslaunch simulation_launch lidar_sim.launch
$ rosrun autolabor_simulation_base autolabor_teleop.py /autolabor_teleop/cmd_vel:=/cmd_vel
$ roslaunch simulation_launch gmapping_navigation.launch
```
在rviz中：
> add robot model;
add LaserScan;(/scan)
add map;(/map)

用键盘操作小车即可看到小车在运动过程中完成建图
保存地图
``` 
$ sudo apt-get ros-kinetic-map-server #下载map_server包
$ rosrun map_server map_saver -f /tmp/my_map 
#将my_map保存在 /tmp 文件夹下
```


  [1]: http://wiki.ros.org/Sensors
  [2]: https://github.com/ros-perception
  [3]: http://www.slamtec.com/cn/Support#rplidar-a1
  [4]: http://www.eeworld.com.cn/uploadfile/2018/0314/1521031945212165.jpg
  [5]: https://blog.csdn.net/ppyang395942297111/article/details/79569148
  [6]: https://sychaichangkun.gitbooks.io/ros-tutorial-icourse163/content/pics/map.png
  [7]: https://blog.csdn.net/tiancailx/article/details/78590809
  [8]: https://sychaichangkun.gitbooks.io/ros-tutorial-icourse163/content/pics/gmapping.jpg
  [9]: https://github.com/gsc07/autolabor_simulation