# ROS (BASIC) 2019.6

标签（空格分隔）： ROS BASIC

---

新手教程：
[Tutorials][1]
[rospy][2]
[roscpp][3]

## 三个级别：计算图级、文件系统级、社区级
* 计算图是ROS处理数据的一种点对点的网络形式。程序运行时，所有进程以及他们所进行的数据处理，将会通过一种点对点的网络形式表现出来。这一级主要包括几个重要概念：节点（node）、消息（message）、主题（topic）、服务（service）
* ROS文件系统级指的是在硬盘上面查看的ROS源代码的组织形式。ROS中有无数的节点、消息、服务、工具和库文件，需要有效的结构去管理这些代码。在ROS的文件系统级，有以下几个重要概念：包（package）、堆（stack）
* ROS的社区级概念是ROS网络上进行代码发布的一种表现形式。

## ROS文件系统
* ROS对CMake进行了扩展，于是便有了Catkin编译系统。Catkin操作更加简化且工作效率更高，可移植性更好，而且支持交叉编译和更加合理的功能包分配。
* 一个Catkin的软件包（package）必须要包括两个文件：
**package.xml:** 包括了package的描述信息
name, description, version, maintainer(s), license
opt. authors, url's, dependencies, plugins, etc...
**CMakeLists.txt:** 
构建package所需的CMake文件
调用Catkin的函数/宏
解析package.xml
找到其他依赖的catkin软件包
将本软件包添加到环境变量
* 编译流程
```
$ cd ~/catkin_ws #回到工作空间,catkin_make必须在工作空间下执行
$ catkin_make    #开始编译
$ source ~/catkin_ws/devel/setup.bash #刷新坏境
```
## catkin 工作空间
```
$ mkdir -p ~/catkin_ws/src　　
$ cd ~/catkin_ws/
$ catkin_make #初始化工作空间
```
* catkin工作空间的结构包括了src、build、devel三个路径，在有些编译选项下也可能包括其他。但这三个文件夹是catkin编译系统默认的。它们的具体作用如下：
* src/: ROS的catkin软件包（源代码包）
* build/: catkin（CMake）的缓存信息和中间文件
* devel/: 生成的目标文件（包括头文件，动态链接库，静态链接库，可执行文件等）、环境变量
后两个路径由catkin系统自动生成、管理，我们日常的开发一般不会去涉及，而主要用到的是src文件夹，我们写的ROS程序、网上下载的ROS源代码包都存放在这里。在编译时，catkin编译系统会递归的查找和编译src/下的每一个源代码包。
## package
ROS中的package的定义更加具体，它不仅是Linux上的软件包，更是catkin编译的基本单元。

定义package的是CMakeLists.txt和package.xml，这两个文件是package中必不可少的。catkin编译系统在编译前，首先就要解析这两个文件。这两个文件就定义了一个package。
|文件名|描述|
| :----:  | :----:  |
|CMakeLists.txt| 定义package的包名、依赖、源文件、目标文件等编译规则，是package不可少的成分|
|package.xml|描述package的包名、版本号、作者、依赖等信息，是package不可少的成分|
|src/|存放ROS的源代码，包括C++的源码和(.cpp)以及Python的module(.py)|
|include/|存放C++源码对应的头文件
|scripts/|存放可执行脚本，例如shell脚本(.sh)、Python脚本(.py)
|msg/| 存放自定义格式的消息(.msg)
|srv/|存放自定义格式的服务(.srv)
|models/|存放机器人或仿真场景的3D模型(.sda, .stl, .dae等)
|urdf/| 存放机器人的模型描述(.urdf或.xacro)
|launch/|存放launch文件(.launch或.xml)


* launch文件一般以.launch或.xml结尾，它对ROS需要运行程序进行了打包，通过一句命令来启动。一般launch文件中会指定要启动哪些package下的哪些可执行程序，指定以什么参数启动，以及一些管理控制的命令。launch文件通常放在软件包的launch/路径中中。
* ROS程序中有可能有一些自定义的消息/服务/动作文件，为程序的发者所设计的数据结构，这类的文件以.msg,.srv,.action结尾，通常放在package的msg/,srv/,action/路径下。
* urdf/xacro文件是机器人模型的描述文件，以.urdf或.xacro结尾。它定义了机器人的连杆和关节的信息，以及它们之间的位置、角度等信息，通过urdf文件可以将机器人的物理连接信息表示出来。并在可视化调试和仿真中显示。
* yaml文件一般存储了ROS需要加载的参数信息，一些属性的配置。通常在launch文件或程序中读取.yaml文件，把参数加载到参数服务器上。通常我们会把yaml文件存放在param/路径下。
* dae或stl文件是3D模型文件，机器人的urdf或仿真环境通常会引用这类文件，它们描述了机器人的三维模型。相比urdf文件简单定义的性状，dae/stl文件可以定义复杂的模型，可以直接从solidworks或其他建模软件导出机器人装配模型，从而显示出更加精确的外形。
* rviz文件本质上是固定格式的文本文件，其中存储了RViz窗口的配置（显示哪些控件、视角、参数）。通常rviz文件不需要我们去手动修改，而是直接在RViz工具里保存，下次运行时直接读取。
```
$ rospack help
$ rospack list
$ rosdep install --from-paths src --ignore-src --rosdistro=kinetic -y #安装工作空间中src路径下所有package的依赖项（由pacakge.xml文件指定）
```

## Metapackage
ROS里常见的Metapacakge有：
|名称|描述|链接|
|:-:|:-:|:-:|
|navigation|导航相关的功能包集|https://github.com/ros-planning/navigation
|moveit|运动规划相关的（主要是机械臂）功能包集|https://github.com/ros-planning/moveit
|image_pipeline|图像获取、处理相关的功能包集|https://github.com/ros-perception/image_common|
|vision_opencv|ROS与OpenCV交互的功能包集|https://github.com/ros-perception/vision_opencv

## 通信架构
### Topic 主题
ROS中的通信方式中，topic是常用的一种。对于实时性、周期性的消息，使用topic来传输是最佳的选择。topic是一种点对点的单向通信方式，这里的“点”指的是node，也就是说node之间可以通过topic方式来传递信息。topic要经历下面几步的初始化过程：首先，publisher节点和subscriber节点都要到节点管理器进行注册，然后publisher会发布topic，subscriber在master的指挥下会订阅该topic，从而建立起sub-pub之间的通信。注意整个过程是单向的。

那么怎么样来理解“异步”这个概念呢？在node1每发布一次消息之后，就会继续执行下一个动作，至于消息是什么状态、被怎样处理，它不需要了解；而对于node2图像处理程序，它只管接收和处理/camera_rgb上的消息，至于是谁发来的，它不会关心。所以node1、node2两者都是各司其责，不存在协同工作，我们称这样的通信方式是异步的。


```
# 常用命令
$ rostopic list
$ rostopic info topic_name #属性
$ rostopic echo topic_name #内容
$ rostopic type topic_name #类型

$ rosmsg list
$ rosmsg show msg_name
```

### Service 服务
当一些节点只是临时而非周期性的需要某些数据，如果用topic通信方式时就会消耗大量不必要的系统资源，造成系统的低效率高功耗。这种情况下，就需要有另外一种请求-查询式的通信模型——service(服务)。

Service通信是双向的，它不仅可以发送消息，同时还会有反馈。所以service包括两部分，一部分是请求方（Clinet），另一部分是应答方/服务提供方（Server）。这时请求方（Client）就会发送一个request，要等待server处理，反馈回一个reply，这样通过类似“请求-应答”的机制完成整个服务通信。

Service是同步通信方式，所谓同步就是说，此时Node A发布请求后会在原地等待reply，直到Node B处理完了请求并且完成了reply，Node A才会继续执行。Node A等待过程中，是处于阻塞状态的成通信。这样的通信模型没有频繁的消息传递，没有冲突与高系统资源的占用，只有接受请求才执行服务，简单而且高效。

```
# 常用命令
$ rosservice list
$ rosservice info #打印服务信息
$ rosservice type #打印服务类型
$ rosservice args #打印服务参数

$ rossrv list
$ rossrv show
$ rossrv package #列出包中的服务
```
### Parameter Service 参数服务器
参数服务器也可以说是特殊的“通信方式”。特殊点在于参数服务器是节点存储参数的地方、用于配置参数，全局共享参数。参数服务器使用互联网传输，在节点管理器中运行，实现整个通信过程。参数服务器，作为ROS中另外一种数据传输方式，有别于topic和service，它更加的静态。参数服务器维护着一个数据字典，字典里存储着各种参数和配置。

参数服务器的维护方式非常的简单灵活，总的来讲有三种方式：

* 命令行维护
* launch文件内读写
* node源码


### Actionlib 动作库
Actionlib是ROS中一个很重要的库，类似service通信机制，actionlib也是一种请求响应机制的通信方式，actionlib主要弥补了service通信的一个不足，就是当机器人执行一个长时间的任务时，假如利用service通信方式，那么publisher会很长时间接受不到反馈的reply，致使通信受阻。当service通信不能很好的完成任务时候，actionlib则可以比较适合实现长时间的通信过程，actionlib通信过程可以随时被查看过程进度，也可以终止请求，这样的一个特性，使得它在一些特别的机制中拥有很高的效率。

Action的工作原理是client-server模式，也是一个双向的通信模式。通信双方在ROS Action Protocol下通过消息进行数据的交流通信。client和server为用户提供一个简单的API来请求目标（在客户端）或通过函数调用和回调来执行目标（在服务器端）。

利用动作库进行请求响应，动作的内容格式应包含三个部分，目标、反馈、结果。

## gazebo
[gazebo入门教程][4]
[gazebo-ROS-Wiki][5]
## rviz
[rviz-ROS-Wiki][6]
## rqt
### rqt_graph
rqt_graph是来显示通信架构，也就是我们上一章所讲的内容节点、主题等等，当前有哪些Node和topic在运行，消息的流向是怎样，都能通过这个语句显示出来。此命令由于能显示系统的全貌，所以非常的常用。
### rqt_plot
rqt_plot将一些参数，尤其是动态参数以曲线的形式绘制出来。当我们在开发时查看机器人的原始数据，我们就能利用rqt_plot将这些原始数据用曲线绘制出来，非常的直观，利于我们分析数据。

## rosbag
rosbag是一个这是一套用于记录和回放ROS主题的工具。它旨在提高性能，并避免消息的反序列化和重新排序。rosbag package提供了命令行工具和代码API，可以用C++或者python来编写包。而且rosbag命令行工具和代码API是稳定的，始终保持向后的兼容性。

## rosbridge
Rosbridge是一个用在ROS系统和其他系统之间的一个功能包,就像是它的名字一样,起到一个"桥梁"的作用,使得ros系统和其他系统能够进行交互.Rosbridge为非ROS程序提供了一个JSON API,有许多与Rosbridge进行交互的前端，包括一个用于Web浏览器交互的WebSocket服务器。Rosbridge_suite是一个包含Rosbridge的元程序包，用于Rosbridge的各种前端程序包（如WebSocket程序包）和帮助程序包。

Rosbridge主要包含两部分内容:协议(Potocol)和实现(Implementation)


  [1]: http://www.ros.org/wiki/ROS/Tutorials
  [2]: http://www.ros.org/wiki/rospy_tutorials
  [3]: http://www.ros.org/wiki/roscpp/Tutorials
  [4]: https://blog.csdn.net/weixin_41045354/article/details/84881498
  [5]: http://wiki.ros.org/gazebo
  [6]: http://wiki.ros.org/rviz