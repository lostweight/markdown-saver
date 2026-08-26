[ROS简介-从零开始讲解ROS（适合超零基础阅读）-CSDN博客](https://blog.csdn.net/qq_25267657/article/details/84316111)

[ROS课程文档](http://www.autolabor.com.cn/book/ROSTutorials/)





# ROS概念

ROS是适用于机器人的开源元操作系统，其集成了大量的工具、库、协议，提供类似OS所提供的功能，简化对机器人的控制

并且ROS还提供了在多台计算机上（分布式）获取，构建，编写和运行代码的工具和库，相当于机器人框架

ROS的设计者将ROS表述为

“ROS = Plumbing(通讯) + Tools + Capabilities（功能） + Ecosystem（生态）”

> Plumbing（通讯）： 不同的模块进行数据交换
>
> Tools（工具）：ros为我们提供仿真的功能，模拟出一个真实的机器人，能够节省很多功夫、
>
> Capabilities（功能）：ros中具有很多开源的功能程序，我们可以直接找到这些功能包并直接复用
>
> Ecosystem（生态）：





# ROS文件系统

ROS文件系统是在磁盘上呈现的ROS源码文件结构，其结构大致如下图所示:

![img](![img](http://www.autolabor.com.cn/book/ROSTutorials/assets/%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F.jpg)

WorkSpace --- 自定义的工作空间

    |--- build:编译空间，用于存放CMake和catkin的缓存信息、配置信息和其他中间文件。
    
    |--- devel:开发空间，用于存放编译后生成的目标文件，包括头文件、动态&静态链接库、可执行文件等。
    
    |--- src: 源码
    
        |-- package：功能包(ROS基本单元)包含多个节点、库与配置文件，包名所有字母小写，只能由字母、数字与下划线组成
    
            |-- CMakeLists.txt 配置编译规则，比如源文件、依赖项、目标文件
    
            |-- package.xml 包信息，比如:包名、版本、作者、依赖项...(以前版本是 manifest.xml)
    
            |-- scripts 存储python文件和脚本文件
    
            |-- src 存储C++源文件
    
            |-- include 头文件
    
            |-- msg 消息通信格式文件
    
            |-- srv 服务通信格式文件
    
            |-- action 动作格式文件
    
            |-- launch 可一次性运行多个节点 
    
            |-- config 配置信息
    
        |-- CMakeLists.txt: 编译的基本配置







## ROS文件系统的相关命令

### 增

```
catkin_create_pkg + + 自定义包名 +（使用的依赖包）
```

### 

### 删

```
sudo apt purge xxx ==== 删除某个功能包
```



### 改

```
rosed + 包名 + 文件名 ==== 修改功能包文件
```



### 查

```
rospack list ==== 列出所有的功能包
rospack find 包名 ==== 查找某个功能包是否存在，如果存在则返回功能包的安装路径
roscd 包名 ==== 进入某个功能包的文件路径
rosls 包名 ==== 列出某个包下的文件
apt search xxx ==== 搜索某个功能包
```



### 执行

#### roscore

**roscore ===** 是 ROS 的系统先决条件节点和程序的集合， 必须运行 roscore 才能使 ROS 节点进行通信。

roscore 将启动:

- ros master
- ros 参数服务器
- rosout 日志节点

用法:

```
roscore
Copy
```

或(指定端口号)

```
roscore -p xxxx
Copy
```



#### rosrun

**rosrun 包名 可执行文件名** === 运行指定的ROS节点

**比如:**`

```ros
rosrun turtlesim turtlesim_node
```



#### roslaunch

**roslaunch 包名 launch文件名** === 执行某个包下的 launch 文件



















# roscore节点管理器

roscore是节点和程序的集合，这些节点和程序是基于ROS系统所必需的，于是我们需要一个管理器来作为所有的节点与程序的集合地，通过这个集合地我们能更好的控制节点以及程序

![在这里插入图片描述](.\ROS.assets\a2e06982c219680192bb44104d738715.png)

**注意**：

只有运行了roscore过后才能是的ROS节点进行通讯，而如果我们使用的是roslaunch命令来运行机器人，当检测到roscore尚未运行的，将会自动启动roscore（除非我们使用--wait参数）

roscore这个命令会启动：

> ​	ROS Master（即ros系统中用于通信的主机/主节点）
>
> ​	ROS Parameter Server （ros参数服务器）
>
> ​	rosout logging node (输出日志节点)



# ros参数服务器

参数服务器是节点管理器的一部分，其允许系统将数据或者配置信息保存在关键位置，所有的节点都可以获取这些数据来配置、改变自己的状态

参数我们可以认为是节点系统中的全局变量，我们可以将这个参数服务器想象成一张多人共享表格，其通讯模型如下：

![在这里插入图片描述](D:\markdown\ROS.assets\72be9aca63c6ce89c3150da235db17d2.png)

核心元素为：

> ROS Master （管理者）: 必须首先运行，负责管理节点之间的消息通讯中的连接信息
>
> Talker（参数设置者）：想参数服务器写入参数（以键值对的方式存储，包括参数名与参数值），ROS Master将参数保存到参数列表中
>
> Listener（参数调用者）：Listener从参数服务器中读取参数，通过参数名称来进行查询

我们以更简单的方式来理解他：

1. ROS Master可以将其想象成多人共享表格的管理者，专门盯着给工作人员（节点）通讯许可等连接信息
2. Talker通过管理者（ROS Master）获得通信权限过后在共享表格中写入数据
3. Listener通过所需要获取的数据名称来获取所需的数据















# ROS实现流程

ROS中的程序即便使用不同的编程语言，实现流程也大致类似，以当前HelloWorld程序为例，实现流程大致如下：

1. **先创建一个工作空间；**
2. **再创建一个功能包；**
3. **编辑源文件；**
4. **编辑配置文件；**
5. **编译并执行。**





## 创建工作空间并初始化

```
mkdir -p 自定义空间名称/src
cd 自定义空间名称
catkin_make						// 编译
```





## 创建功能包

```
cd src
catkin_create_pkg 功能包名称 功能包依赖包
示例：catkin_create_pkg helloworld roscpp(C++实现的ros库) rospy(python实现的ros库) std_msgs(标准消息库)
```







# helloworld

在完成上面两步的通用步骤过后，我们就能正式进行节点程序的编写了

每个程序包我们都可以使用一下的步骤进行构建

## 1.进入 ros 包的 src 目录编辑源文件

具体程序如下：

```C++
//1.包含ros的头文件
#include "ros/ros.h"

//2.编写main函数
int main(int argc, char *argv[])
{
	//3.初始化ros节点
	ros::init(argc, argv, "hello_node");
	
	//4.输出日志
	ROS_INFO("hello world!");
	
	return 0;
}
```







## 2.编辑 ros 包下的 Cmakelist.txt文件

编写完毕过后，我们需要编辑ros包下的CMakeLists.txt文件

```cmake
add_executable(步骤3的源文件名 src/步骤3的源文件名.cpp)
target_link_libraries(步骤3的源文件名 ${catkin_LIBRARIES})
```





## 3.进入工作空间目录并编译

```cmake
cd 自定义空间名称
catkin_make
```

执行完这一步过后，我们的工作空间中就会出现build、devel文件夹，





## 4.修改环境变量

```
source 自定义空间文件夹/devel/setup.bash
```

但是这种方法具有局限性，因为这种方法是局部修改环境变量，无法在全局的窗口下运行

因此我们可以使用下面的全局修改方法：

```
echo "source ~/工作空间/devel/setup.bash" >> ~/.bashrc
```





## 5.执行功能包

```
rosrun 功能包名称 功能包最后生成的可执行文件的名称
```









# launch文件

需求：一个程序中可能需要启动多个节点，为了能够快速的启动多个节点我们可以使用launch文件

实现：

>1.在需要使用launch文件的功能包中新建launch文件夹
>
>2.在该launch文件夹中新建launch文件
>
>3.编辑launch文件
>
>```
><launch>
>	<!-- 添加需要被执行的节点 -->
>	<node pkg="需要使用的功能包名" type="需要执行的节点" name="执行的节点的别名"> 
>				<!-- 若有日志需要是输出则可以再加入一个属性output="screen" -->
></launch>
>```
>
>4.运行launch文件：
>
>```
>roslaunch 包名 launch文件名
>```
>
>5.运行结果：一次性启动了多个节点】









# ROS架构

立足于不同的角度，对ROS架构的描述也是不同的，一般我们可以从设计者、维护者、系统架构与自身架构四个角度来描述ROS架构



## 1.设计者

ROS设计者将ROS表述为：

ROS**设计者**将ROS表述为“ROS = Plumbing + Tools + Capabilities + Ecosystem”

- Plumbing: **通讯机制(实现ROS不同节点之间的交互)**
- Tools :**工具软件包(ROS中的开发和调试工具)**
- Capabilities :机器人高层技能(ROS中某些功能的集合，比如:导航)
- Ecosystem:机器人生态系统(跨地域、跨软件与硬件的ROS联盟)





## 2.维护者

立足**维护者**的角度: ROS 架构可划分为两大部分

- mainI（基本架构）：核心部分，主要由Willow Garage 和一些开发者设计、提供以及维护。它提供了一些分布式计算的基本工具，以及整个ROS的核心部分的程序编写。
- universe（扩展功能）：全球范围的代码，有不同国家的ROS社区组织开发和维护。一种是库的代码，如OpenCV、PCL等；库的上一层是从功能角度提供的代码，如人脸识别，他们调用下层的库；最上层的代码是应用级的代码，让机器人完成某一确定的功能。





## 3.系统架构

立足系统架构: ROS 可以划分为三层

- OS 层，也即经典意义的操作系统

    ROS 只是元操作系统，需要依托真正意义的操作系统，目前兼容性最好的是 Linux 的 Ubuntu，Mac、Windows 也支持 ROS 的较新版本

- 中间层

    是 ROS 封装的关于机器人开发的中间件，比如:

    - 基于 TCP/UDP 继续封装的 TCPROS/UDPROS 通信系统
    - 用于进程间通信 Nodelet，为数据的实时性传输提供支持
    - 另外，还提供了大量的机器人开发实现库，如：数据类型定义、坐标变换、运动控制....

- 应用层

    功能包，以及功能包内的节点，比如: master、turtlesim的控制与运动节点...立足系统架构: ROS 可以划分为三层

    - OS 层，也即经典意义的操作系统

        ROS 只是元操作系统，需要依托真正意义的操作系统，目前兼容性最好的是 Linux 的 Ubuntu，Mac、Windows 也支持 ROS 的较新版本

    - 中间层

        是 ROS 封装的关于机器人开发的中间件，比如:

        - 基于 TCP/UDP 继续封装的 TCPROS/UDPROS 通信系统
        - 用于进程间通信 Nodelet，为数据的实时性传输提供支持
        - 另外，还提供了大量的机器人开发实现库，如：数据类型定义、坐标变换、运动控制....

    - 应用层

        功能包，以及功能包内的节点，比如: master、turtlesim的控制与运动节点...





## 4.自身结构

就 ROS 自身实现而言: 也可以划分为三层

- 文件系统

    ROS文件系统级指的是在硬盘上面查看的ROS源代码的组织形式

- 计算图

    ROS 分布式系统中不同进程需要进行数据交互，计算图可以以点对点的网络形式表现数据交互过程，计算图中的重要概念: 节点(Node)、消息(message)、通信机制_主题(topic)、通信机制_服务(service)

- 开源社区

    ROS的社区级概念是ROS网络上进行代码发布的一种表现形式















# ROS通信机制

在ROS中每一个功能点都是一个单独的进程，每一个进程都是独立运行的。更确切的讲，**ROS是进程（也称为*Nodes*****）的分布式框架。** 因为这些进程甚至还可分布于不同主机，不同主机协同工作，从而分散计算压力。不过随之也有一个问题: 不同的进程是如何通信的？也即不同进程间如何实现数据交换的？在此我们就需要介绍一下ROS中的通信机制了。

ROS 中的基本通信机制主要有如下三种实现策略:

- 话题通信(发布订阅模式)
- 服务通信(请求响应模式)
- 参数服务器(参数共享模式)





## 话题通讯

话题通信是ROS中使用频率最高的一种通信模式，话题通信是基于**发布订阅**模式的，也即:一个节点发布消息，另一个节点订阅该消息。话题通信的应用场景也极其广泛，比如下面一个常见场景:

> 机器人在执行导航功能，使用的传感器是激光雷达，机器人会采集激光雷达感知到的信息并计算，然后生成运动控制信息驱动机器人底盘运动。

像雷达、摄像头、GPS.... 等等一些传感器数据的采集，也都是使用了话题通信，换言之，话题通信适用于不断更新的数据传输相关的应用场景。



### **概念**

以发布订阅的方式实现不同节点之间数据交互的通信模式。



### **作用**

用于不断更新的、少逻辑处理的数据传输场景。





## 服务通信

服务通信包括了服务端与客户端交互的过程，并且该通信方式是基于**请求响应的模式**，这种模式是一种应答机制，它还是一种双向同步数据传输模式，它具有两部分的通信数据类型，一种用于请求，一种用用于应答，他的通信方式与网络通信模式Tcp/ip模式类似，服务端会提前开启，只有当客户端请求访问的时候，服务端才会返回数据。







## 参数服务器

参数服务器就很有意思了，它相当于一张共享表格，这张共享表格可以被任何节点更改，也能让任何节点读取，例如：微信的共享表格，用户能够在表格中填写数据，当然也能通过共享表格获取数据





### 理论模型

话题通信实现模型是比较复杂的，该模型如下图所示,该模型中涉及到三个角色:

- ROS Master (管理者)
- Talker (发布者)
- Listener (订阅者)

ROS Master 负责保管 Talker 和 Listener 注册的信息，并匹配话题相同的 Talker 与 Listener，帮助 Talker 与 Listener 建立连接，连接建立后，Talker 可以发布消息，且发布的消息会被 Listener 订阅。

![img](http://www.autolabor.com.cn/book/ROSTutorials/assets/01%E8%AF%9D%E9%A2%98%E9%80%9A%E4%BF%A1%E6%A8%A1%E5%9E%8B.jpg)

[模型解释]([038话题通信_理论模型_Chapter2-ROS通信机制_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Ci4y1L7ZZ/?p=40&spm_id_from=pageDriver&vd_source=b6ec906023fa46a5d781f4c754d9bf34))

整个流程由以下步骤实现:

#### 0.Talker注册

Talker启动后，会通过RPC在 ROS Master 中注册自身信息，其中包含所发布消息的话题名称。ROS Master 会将节点的注册信息加入到注册表中。



#### 1.Listener注册

Listener启动后，也会通过RPC在 ROS Master 中注册自身信息，包含需要订阅消息的话题名。ROS Master 会将节点的注册信息加入到注册表中。



#### 2.ROS Master实现信息匹配

ROS Master 会根据注册表中的信息匹配Talker 和 Listener，并通过 RPC 向 Listener 发送 Talker 的 RPC 地址信息。



#### 3.Listener向Talker发送请求

Listener 根据接收到的 RPC 地址，通过 RPC 向 Talker 发送连接请求，传输订阅的话题名称、消息类型以及通信协议(TCP/UDP)。



#### 4.Talker确认请求

Talker 接收到 Listener 的请求后，也是通过 RPC 向 Listener 确认连接信息，并发送自身的 TCP 地址信息。



#### 5.Listener与Talker件里连接

Listener 根据步骤4 返回的消息使用 TCP 与 Talker 建立网络连接。



#### 6.Talker向Listener发送消息

连接建立后，Talker 开始向 Listener 发布消息。

> 注意1:上述实现流程中，前五步使用的 RPC协议，最后两步使用的是 TCP 协议
>
> 注意2: Talker 与 Listener 的启动无先后顺序要求
>
> 注意3: Talker 与 Listener 都可以有多个
>
> 注意4: Talker 与 Listener 连接建立后，不再需要 ROS Master。也即，即便关闭ROS Master，Talker 与 Listern 照常通信。





### **案例**

向底盘发送运动指令

```C++
#include <ros/ros.h>
#include <geometry_msgs/Twist.h>

int main(int argc, 	char * argv[])
{
    ros::init_node(argc, argv, "val_node");	 // 初始化节点
    ros::NodeHandle nh;						// 设置句柄，相当于手机，用于发送数据
    ros::Publisher vel_put_node = nh.advertise<geometry_msgs::Twist>("/cmd_vel", 10);	// 实例化手机，并告诉ros服务器指定要发送数据的话题以及发布的话题的数组大小
    
    geometry_msgs::Twist vel_msg;
    
    vel_msg.linear.x = 0.5;					// 向前走0.5个栅格距离
    vel_msg.linear.y = 0;
    vel_msg.linear.z = 0;
    vel_msg.angular.x = 0;
    vel_msg.angular.y = 0;
    vel_msg.angular.z = 0.2					// 向左转动0.2 
    
    ros::Rate r(30);						// 设置频率
    while (1)
    {
        vel.pub.publish(vel_msg);			// 发送话题数据到/cmd_vel中
        r.sleep();
    }
        
    return 0;
}
```

```python
import rospy
from geometry_msgs.msg import Twist

if __name__ == "__main__":
	rospy.init_node("vel_node")				# 初始化节点
	
	vel_pub = rospy.Publisher("cmd_vel", Twist, queue_size=10)
	# c++与python的发布节点的区别在于，C++需要使用句柄这种指针的方式进行发送数据
	# 而python能直接实例化发布者对象进行发送数据，但其本质上差不多
	
	vel_msg = Twist()
	vel_msg.linear.x = 0.1
	rate = rospy.Rate(30)

	while not rospy.is_shutdown():
		vel_pub.publish(vel_msg)
		rate.sleep()
```





## action服务

ROS中有一个名为**actionlib**的功能包，它实现了action的通信机制

而**action是一种类似于Service的问答通信机制，不同之处在于action带有连续的反馈，可以当需要action服务端做某事的时候，就能通过action的客户端向action服务端发送action命令，使得action服务端开始工作并持续向action客户端发送工作的进度信息**

![img](E:\Markdown\markdown\ROS.assets\v2-6e37962e65b5b1681d10d8e130225b17_1440w.jpg)

Client和Server之间通过actionlib定义的“action protocol”来进行通信。这种通信协议基于ROS的话题机制实现，为用户提供如下图所示的Client和Server的接口

![img](E:\Markdown\markdown\ROS.assets\v2-59d846511585d0b75b5ea41670907862_1440w.jpg)

Client向Server端发布任务目标以及在必要的时候取消任务，Server会向Client发布当前的状态、实时反馈和任务执行的最终结果。

> (1) goal：Client向Server发送任务目标
>
> （2）cancel：请求取消任务
>
> （3）status：服务端在接收到action命令开始执行任务时，自动通知Client当前的工作状态
>
> （4）feedback：周期反馈任务的工作监控数据
>
> （5）result：向Client发送任务的执行结果，通常是在Action Server完成任务或者无法完成任务时进行发布，并且只会发布一次



### action通信的实现方式

action通信服务一般可以用于自主坐标导航的任务中，其具体的工作流程图如下图所示：

<img src="E:\Markdown\markdown\ROS.assets\image-20250418064719470.png" alt="image-20250418064719470" style="zoom:40%;" />

通过action的通信方式，最终能够让用户自己建立程序，并在程序中创建一个aciton Client，并设置好目标点的Linear坐标以及欧拉角的姿态坐标最后发送给move_base自主导航模块，导航模块最终会通过各种全局规划器、局部规划器、以及应急机制等等方法进行自主导航，并将导航过程中每一时刻需要的底盘运动指令通过/cmd_vel话题发送给底盘，进而驱动底盘运动









# Node节点

节点即功能，或者说是进程，这些进程实现机器人运行过程中的某部分的功能，比如采集数据、计算数据等等

我们也可以将其（节点）看成一个真实的人，每个人负责机器人控制的某部分工作，所有人一起合作，机器人就能正常运行了

通常一个机器人系统就是很多个节点独立运行，**同时联合相互合作**，如同下图，在下图中，整个计算机系统是通过许多的节点相互联系组合而成的，其中每个节点只负责执行其中一个简单的功能，

<img src="E:\Markdown\markdown\ROS.assets\image-20250415155156008.png" alt="image-20250415155156008" style="zoom:50%;" />





# Package包

简单点理解Package包其实就是节点的包装袋子，每个袋子里面包含若干个节点功能



# 激光雷达工作原理



<img src=E:\Markdown\markdown\ROS.assets\52623ee4012eb7c246f37dd416af322e.jpeg style="zoom:50%;" />

通过发送端发出光信号，当光信号到达障碍物并反弹回接收端，计算其时间以及光速，最后通过计算得到具体的距离

然后再调整指定的角度，再继续进行上面的操作，然后不断的重复上面的两个步骤就能实时地扫描周围障碍物的分布情况

于是在rviz中就能看到具体的障碍物分布图

<img src="E:\Markdown\markdown\ROS.assets\image-20250415122641877.png" alt="image-20250415122641877" style="zoom:50%;" />

激光雷达的数据类型





# Terminator 常用快捷键

**第一部份：关于在同一个标签内的操作**

```
Alt+Up                          //移动到上面的终端
Alt+Down                        //移动到下面的终端
Alt+Left                        //移动到左边的终端
Alt+Right                       //移动到右边的终端
Ctrl+Shift+O                    //水平分割终端
Ctrl+Shift+E                    //垂直分割终端
Ctrl+Shift+Right                //在垂直分割的终端中将分割条向右移动
Ctrl+Shift+Left                 //在垂直分割的终端中将分割条向左移动
Ctrl+Shift+Up                   //在水平分割的终端中将分割条向上移动
Ctrl+Shift+Down                 //在水平分割的终端中将分割条向下移动
Ctrl+Shift+S                    //隐藏/显示滚动条
Ctrl+Shift+F                    //搜索
Ctrl+Shift+C                    //复制选中的内容到剪贴板
Ctrl+Shift+V                    //粘贴剪贴板的内容到此处
Ctrl+Shift+W                    //关闭当前终端
Ctrl+Shift+Q                    //退出当前窗口，当前窗口的所有终端都将被关闭
Ctrl+Shift+X                    //最大化显示当前终端
Ctrl+Shift+Z                    //最大化显示当前终端并使字体放大
Ctrl+Shift+N or Ctrl+Tab        //移动到下一个终端
Ctrl+Shift+P or Ctrl+Shift+Tab  //Crtl+Shift+Tab 移动到之前的一个终端
Copy
```

**第二部份：有关各个标签之间的操作**

```
F11                             //全屏开关
Ctrl+Shift+T                    //打开一个新的标签
Ctrl+PageDown                   //移动到下一个标签
Ctrl+PageUp                     //移动到上一个标签
Ctrl+Shift+PageDown             //将当前标签与其后一个标签交换位置
Ctrl+Shift+PageUp               //将当前标签与其前一个标签交换位置
Ctrl+Plus (+)                   //增大字体
Ctrl+Minus (-)                  //减小字体
Ctrl+Zero (0)                   //恢复字体到原始大小
Ctrl+Shift+R                    //重置终端状态
Ctrl+Shift+G                    //重置终端状态并clear屏幕
Super+g                         //绑定所有的终端，以便向一个输入能够输入到所有的终端
Super+Shift+G                   //解除绑定
Super+t                         //绑定当前标签的所有终端，向一个终端输入的内容会自动输入到其他终端
Super+Shift+T                   //解除绑定
Ctrl+Shift+I                    //打开一个窗口，新窗口与原来的窗口使用同一个进程
Super+i                         //打开一个新窗口，新窗口与原来的窗口使用不同的进程
```











# Navigation导航系统

![image-20250413161001373](E:\Markdown\markdown\ROS.assets\image-20250413161001373.png)

该系统与日程生活使用地图进行导航的流程相类似，例如

* map_server下载地图数据

* 同时输入目的地

* 使用global_planner（全局规划器）进行全局路线规划

* 开始前往，并使用local_planner（局部规划器）根据自身的观察（雷达、amcl\<自适应蒙特卡洛定位算法\>、odom\<里程计>等传感器）进行生成局部的代价地图，使得其辅助路线规划并进行路线决策，并将运动信号发送给运动神经（底盘）

* 当遇到临时障碍物阻挡规划的路线，则会思考，并使用局部规划器进行避障决策，若无法避障，则回进入应急机制（恢复行为：保险重置、旋转消除、激进重置、旋转清除）

* 底盘根据发送过来的运动信号开始移动

    

## map_server

* 描述：机器人导航地图数据节点

* 使用话题：/map → nav_msgs::OccupancyGrid（占据栅格地图）

* 数据类型的具体参数：

    * OccupancyGrid.header：时间戳和坐标id
    * OccupancyGrid.info：地图的参数信息
    * OccupancyGrid.data：地图的具体数据数组，将地图的具体数值通过数组进行存储，并最后通过改变数组的形状即可获得原地图的具体样貌，其中障碍物占据值取值位0-100，未知区域则取值-1

    

    发布地图节点的具体操作步骤：

    1. 构建map_pkg功能包，且依赖项中需要包含nav_msgs数据类型
    2. 在map_pkg创建发布数据节点
    3. 发布话题/map，消息类型nav_msgs::OccupanyGrid
    4. 实例化数据类型，并给数据对象赋值
    5. 将地图的数据发送到话题/map中
    6. 编译







# 问题

## **当ROS__INFO 终端输出有中文时，会出现乱码**

解决办法：在函数开头加入下面代码的任意一句

```cpp
setlocale(LC_CTYPE, "zh_CN.utf8");
setlocale(LC_ALL, "");
```