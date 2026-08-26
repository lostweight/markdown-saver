# 安装与启动isaac-Sim

启动isaac Sim容器需要两台电脑，一台是服务器，另一台是访问机

下面的操作需要在isaac Sim的镜像运行为基础

确认服务器端安装完毕docker的镜像并启动进项后，就可以使用访问机电脑来运行isaac-Sim的仿真界面平台

具体在访问机所使用运行平带命令：

```
chmod 777 ./isaacsim-webrtc-streaming-client-1.0.6-linux-x64.AppImage   # 第一次运行必须执行的
./isaacsim-webrtc-streaming-client-1.0.6-linux-x64.AppImage 
```

<img src="E:\Markdown\markdown\Nvidia_issac_sim.assets\image-20250416104727487.png" alt="image-20250416104727487" style="zoom:50%;" />

# 图形化界面与工作流介绍

**工作流**是什么：<u>在Isaac Sim仿真平台中，工作流是指一系列任务的执行步骤树</u>

Isaac Sim是用于设计、调试、训练以及部署机器人智能体任务的仿真平台，它提供了两种工作流方式（即通过不同的执行方式来进行仿真控制，每种方式都有它具体的使用方式，比如图形话界面就能直接通过界面来仿真，而python脚本则是使用代码的方式）：

1. 图形化界面：Isaac Sim通过图形化的方式将仿真场景进行渲染，可视化界面中提供了参数设置面板、构建任务逻辑的低代码工具，我们可以通过可视化界面设计与构建机器人、场景以及任务。不仅如此，我们还能在训练任务以及训练后的模型部署的过程中直接使用图形化界面将效果渲染出来，直观的查看效果
2. 独立的Python脚本：该工作流通过Python脚本的方式设计issac-Sim启动流程以及任务逻辑

## 图形化界面介绍

以下是Isaac Sim的图形化界面，我们可以简单对界面各个部分进行分类：

| 编号 | 部件名称   | 部件作用                   |
| ---- | ---------- | -------------------------- |
| 1    | 菜单栏     | 软件功能入口               |
| 2    | 视图窗口   | 3D场景实时渲染显示区域     |
| 3    | 工具栏     | 快捷操作工具集             |
| 4    | 文件浏览器 | 容器文件管理系统           |
| 5    | USD场景树  | 场景层级结构可视化         |
| 6    | 属性面板   | 当前选中Prim的详细参数配置 |



### 菜单栏

Isaac-Sim菜单栏由八部分组成：

#### 1. Create

创建各种仿真对象的菜单，比如我们可以在场景中Create一个立方体

#### 2. Windows

用于打开/隐藏Isaac_Sim的图形化界面的部分窗口，图形化界面就是由这些窗口组成的

#### 3. Tools

仿真工作流过程中使用的工具，可以通过该栏打开某部分的工具栏

#### 4. Utilities

#### 5. Layouts

用于调整Isaac_Sim的可视化界面的展示布局，通过该栏的Visual Scripting选项就能进行调整可视化界面的展示布局，当然也能通过`CTRL+6`来使用调整功能，若要回到默认的布局则可以使用`CTRL+1`切换回来

#### 6. Help

提供Isaac_Sim相关的帮助文档机器示例，可以通过该选项来查看示例

### 文件浏览器

文件浏览器顾名思义，往往存放着isaac sim的核心启动文件以及官方提供的自残文件，我们能通过该文件浏览器在服务器中找到我们需要的文件，并加载到场景中



### USD场景树

在Isaac-Sim中，所有渲染的物品都是**OpenUSD**格式（可简称为USD），这一格式通过组合式架构来管理物品中的层级、关联关系，





### 属性面板 

属性面板用于现实所选的Prim的属性内容，这对于查看、调试物品属性十分有帮助

其中Prim（基本图元）是构成虚拟场景的基本构建块、可以理解成Prim就是场景中的一个对象或者实体，可以代表为模型、灯光、相机、物理属性等等，可以理解成Prim就是Isaac-Sim中的一块积木，通过这个积木能够搭建出一个机器人、机械臂或者是一个场景

而属性面板则能查看这些积木的属性，包括大小、颜色等等的参数



# Isaac-Sim仿真入门



Isaac-Sim这类仿真器的目的就是为了对现实的场景进行物理仿真，按照**仿真的基础构建**（物理场景、角色、环境）到**仿真核心过程**（运动、交互），再到**仿真优化与数据处理**（计算参数设置、数据记录处理），最后到**仿真支持与效率提升**（物理引擎、初始化边界条件、脚本自动化）的逻辑顺序，通常情况下需要包含以下的十个方面的内容

#### 1. 物理空间

物理空间是所有仿真的基础，犹如现实世界，*所有东西都要基于物理空间为基础*，它定义了整个模拟环境的空间布局和基本的物理特性，它为其他的物体提供了支撑以及参照，地面上的物体构成了具体的模拟对象，它们的物理属性（如质量、材质等）以及空间位置决定了仿真的初始状态和后续的相互作用



#### 2. 角色以及物体

人、机器人、小车等角色是仿真中的主要活动对象，它们具有各自独特的运动方式以及行为模式。角色的物理模型与控制逻辑则直接影响着仿真的真实性与实用性。我们必须要通过精准地设置以及调整，以实现符合实际状况的运动效果



#### 3. 环境

包含视觉和物理环境，如特定的光照、物理空间地形等等，通过环境的不同，仿真会更加地接近现实，同时还会对角色以及物体的运动产生间接性的影响，例如在雨天的摩檫力会变小等状况，我们可以通过不同的环境来仿真具体的角色在各种环境条件下的实用性



#### 4. 角色或者物体相互间的交互

碰撞是角色与物体之间最常见的交互方式之一，同时会包括各种物理力学，支持力，传感器交互等等的协作

准确的碰撞检测以及合理的碰撞响应机制是保证仿真真实性的重要环节，当角色或物体发生碰撞的时候，会使得角色或环境产生不同的效果



#### 5. 初始条件与边界条件

初始条件包含：角色的初始位置、速度

边界条件包括：仿真空间的限制



#### 6. 仿真过程的数据记录与处理

在仿真过程中，记录数据是分析和评估仿真结果二端基础，通过这些数据的处理以及分析，可以更加深入了解仿真过程中存在的问题，并以此来优化模型以及参数



#### 7. 物理引擎

物理引擎支持所有仿真背后的物理动力学的支撑



#### 8. 仿真过程计算与性能相关的参数

有些参数对于优化仿真过程、提高计算效率和保证结果的准确至关重要，例如时间步长的设置决定了仿真的精细程度和计算速度，较小的时间步长可以提高精度，但是会提升计算量



#### 9. 脚本与自动化

脚本与自动化程序能够提高仿真的效率





## 物理动力学相关工具

在我们的例子中，物理引擎只所以能够遵循物理动力学的相关规律，因此便需要物理引擎的核心物理求解器和约束解释器

#### 物理求解器

在仿真过程中，物理求解器被用于执行物理模拟的计算，以确定场景中的物体的运动、碰撞以及相互作用等的物理行为

其具体的作用包括：

* 计算物体运动
* 处理碰撞检测与响应
* 模拟关节以及关节约束
* 支持复杂的物理模拟
* 保证模拟的稳定性和准确性



#### 约束求解器

约束求解器用于实现机器人在运行过程中的各种约束条件，包括：机器人的关节角度限制、速度限制、加速度限制、运动限制、环境障碍物限制等等约束条件

物理求解器与约束求解器之间有什么区别：

**约束求解器**主要的工作就是通过各种算法和技术来处理约束条件，确保机器人满足约束条件，确保机器人的在各种约束条件下依旧正常工作运行，其主要应用在角色的姿态控制、工程设计规范等等

**物理求解器**则主要工作是执行物理模拟的计算，通过这些计算来是的每个刚体在力、扭矩作用下的加速度、速度、位置以及摩擦等物理力学的影响以确定场景中的运动、碰撞、相互影响等的物理行为	



## 仿真相关概念

### USD通用概念

prim就是基本的场景积木

### 物理场景

物理场景是比物理空间更大的一个概念，其包含了所有物理空间以及所有参与物理模拟的角色、物体、环境等元素的一个集合。它定义了整个仿真的物理环境，如重力、物理求解器参数等。一个场景中可以有多个刚体和关节物体相互作用。

### 角色

#### 刚体

物理场景是比物理空间更大的一个概念，其包含了所有物理空间以及所有参与物理模拟的角色、物体、环境等元素的一个集合。它定义了整个仿真的物理环境，如重力、物理求解器参数等。一个场景中可以有多个刚体和关节物体相互作用。



# 问题

而isaac Sim容器连接并启动为什么需要两台电脑，我们就不能只在一台电脑上运行嘛？

当然可以



### 学习问题：

#### ！怎样让一个物体拥有刚性，机器人跟它碰撞后效果如何？这个效果背后是如何产生的？

答：使得物体的Attribute Name中的type转为刚体类型，并且需要具有碰撞网络，

怎样让机器人拥有移动的能力？这个移动能力背后的原理是什么？
答：需要使用到如关节控制器Articulation关节控制器、自定义差速控制器、底层转子控制器或者Isaac Sim底盘控制API提供给机器人实例控制器对象，同时apply_aciton函数来接收关节控制器的关节速度、差速控制器传出的前进速度以及角速度、底层轮子控制器传出的数据来进行移动

#### ！轮式机器人在仿真场景运动时，摩擦力是如何产生的？

答：摩檫力是通过世界节点的参数，通过物理求解器进行现实物理仿真计算的

！通过Python API 运行Isaac Sim应用，怎样能让它通过Isaac Sim WebRTC Streaming Client 进行访问？背后的原理是什么

#### 完成机械臂、轮式机器人任务开发，常见Python API 有哪些？这些 API的作用分别是什么？

答：
控制机械执行指定操作isaacsim.robot.manipulators.examples.franka.Franka.get_object(object_name).apply_action(actions)

创建世界：isaacsim.core.api.World()
为世界添加任务：isaacsim.core.api.World().add_task(task_object())
给世界的场景添加Prim：isaacsim.core.api.World.scene.add()

获取世界中的某个Prim：BaseSample.get_world.scene.get_object(Prim_name)
设置世界在仿真过程中要执行的回调函数：BaseSample.get_world.add_physics_callback("sim_step", callback_fn)
获取世界观察的数据：BaseSample.get_world().get_observations()
启动仿真：BaseSample.get_world().play_async()
暂停仿真：BaseSample.get_world().pause()


Cube对象实例：isaacsim.core.api.objects.DynamicCuboid
机械臂对象实例：isaacsim.robot.manipulators.examples.franka.Franka()
轮式机器人对象实例：isaacsim.robot.wheel_robots.WheeledRobot(prim_path:str, name:str, wheel_dof_names:List<str>, create_robot:bool, usd_path:str)

实例化机械臂抓取、放置控制器：isaacsim.robot.manipulators.examples.franka.controllers.PickPlaceController
轮式机器人控制器：isaacsim.core.api.controllers.BaseController
关节控制器：isaacsim.core.utils.types.ArticulationAction(joint_velocities)
控制器基类：isaacsim.core.api.controllers.BaseController



#### 参考课程的案例，实现Jetbot 机器人导航任务的独立Python 脚本如何编写？

答：要实现Jetbot机器人的导航任务可以通过一下步骤来实现：

	1. 建立HelloWorld实例
	2. 编写实例程序的初始化场景函数，在该函数中首先我们需要进行加载世界、地面实例、机器人实例到场景中
	3. 编写实例程序在点击加载按钮进行加载场景时的操作函数，在该函数中，我们可以将世界、机器人对象、以及后续对机器人的操作的控制器进行加载以及初始化
	4. 编写对机器人进行操作时的物理回调函数，这个物理回调函数是当程序进行仿真的时候出现时间不仅的时候会自动的回调执行，即每步进一次就返回来执行一次这个函数
	在这个函数中，我们可以定义机器人传感器数据获取、机器人执行操作的指令，进而实现对机器人控制信息的获取并且最终传入到控制器中








    class FrankaPlaying(BaseTask):                  # 
        def __init__(self, name):
            super().__init__(name=name, offset=None)
            self._goal_position = np.array([-0.3, -0.3, 0.0515 / 2.0])
            self._task_achieved = False
            return
        
    def set_up_scene(self, scene):              # 初始化场景
        super().set_up_scene(scene)
        scene.add_default_ground_plane()        # 添加地面
        self._cube = scene.add(
            DynamicCuboid(
                prim_path="/World/random_cube",
                name="fancy_cube",
                position=np.array([0.3, 0.3, 0.3]),
                scale=np.array([0.0515, 0.0515, 0.0515]),
                color=np.array([0, 0, 1.0])
            )
        )
        self._franka = scene.add(
            Franka(
                prim_path="/World/Fancy_Franka",
                name="fancy_franka"
            )
        )
    
    def get_observations(self):
        cube_position, _ = self._cube.get_world_pose()
        current_joint_positions = self._franka.get_joint_positions()
        observations = {
            self._franka.name:{"joint_positions": current_joint_positions},
            self._cube.name:{
                "position": cube_position,
                "goal_position": self._goal_position
            }
        }
        return observations
    
    def pre_step(self, control_index, simulation_time):
        cube_position, _ = self._cube.get_world_pose()
        if not self._task_achieved and np.mean(np.abs(self._goal_position - cube_position)) < 0.02:
            self._cube.get_applied_visual_material().set_color(color=np.array([0, 0, 1.0]))
            self._task_achieved = True
        return  
    
    def post_reset(self):
        self._franka.gripper.set_joint_positions(self._franka.gripper.joint_opened_positions)
        self._cube.get_applied_visual_material().set_color(color=np.array([0, 1.0, 0]))
        self._task_achieved = False
        return


当然我们还可以不进行自定义task，直接通过官方封装的Franka的夹取、放置任务，并通过PickPlace的封装task类来进行加载机器人控制task类，来直接实现机械臂的抓取、放置任务









常用的API
