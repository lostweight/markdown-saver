





# Isaac Sim的工作流

Isaac Sim一共有三种的工作方式：

## GUI交互

我们在仿真平台上进行创建Prim、世界、场景等操作基本都是GUI操作，主要就是低代码的在仿真平台上进行世界的构建、场景的搭建、机器人的组装、连接传感器。



## 扩展（extension）

扩展时基于Omniverse Kit的子集，Isaac Sim中使用的工具都安装在extension manager中，可以在不同的应用程序中使用它们，在菜单中的Isaac example，加载USD并引入脚本控制，也属于扩展的一种。

并且通常我们的脚本设计的样式为：

脚本程序的仿真类程序实现步骤：

1. 导入相应需要使用的节点、对象、功能包
2. 创建仿真对象，当然也可以使用task对象，并在主仿真对象中使用这个task对象
3. 创建的仿真对象中，程序的大概步骤分为：
   * 定义初始化设置
   * 定义初始化场景的函数，可执行的任务为：初始化场景、获取数据等等
   * reset函数，这个函数一般需要定义为当按下reset按键进行充值的时候所需要执行的操作
   * 如果是使用了task命令，则需要在task命令中设置为：
     * 设置场景的加载操作
     * 设置执行任务是所需要的功能操作，task多数是设置与定义
       最后还是需要在BaseSample类中定义执行仿真任务的具体任务，

具体的代码可以参考

```python
from isaacsim.examples.interactive.base_sample import BaseSample
from isaacsim.robot.manipulators.examples.franka.tasks import PickPlace
from isaacsim.robot.wheeled_robots.robots import WheeledRobot
from isaacsim.core.utils.nucleus import get_assets_root_path
from isaacsim.robot.wheeled_robots.controllers.wheel_base_pose_controller import WheelBasePoseController
from isaacsim.robot.manipulators.examples.franka.controllers import PickPlaceController
from isaacsim.robot.wheeled_robots.controllers.differential_controller import DifferentialController
from isaacsim.core.api.tasks import BaseTask
from isaacsim.core.utils.types import ArticulationAction
import numpy as np


class RobotsPlaying(BaseTask):
    def __init__(self, name):
        super().__init__(name=name, offset=None)
        # Jetbot的目标位置
        self._jetbot_goal_position = np.array([1.3, 0.3, 0])
        # 任务阶段标记：0-导航，1-后退，2-抓取
        self._task_event = 0
        # 初始化抓取任务（Franka机械臂）
        self._pick_place_task = PickPlace(
            cube_initial_position=np.array([0.1, 0.3, 0.05]),  # 立方体初始位置
            target_position=np.array([0.7, -0.3, 0.0515 / 2.0])  # 目标放置位置
        )
        return

    def set_up_scene(self, scene):
        super().set_up_scene(scene)
        # 设置抓取任务的场景（地面、Franka、立方体）
        self._pick_place_task.set_up_scene(scene)
        # 加载Jetbot模型
        assets_root_path = get_assets_root_path()
        jetbot_asset_path = assets_root_path + "/Isaac/Robots/Jetbot/jetbot.usd"
        # 添加Jetbot到场景
        self._jetbot = scene.add(
            WheeledRobot(
                prim_path="/World/Fancy_Jetbot",  # USD路径
                name="fancy_jetbot",              # 名称
                wheel_dof_names=["left_wheel_joint", "right_wheel_joint"],  # 轮子关节
                create_robot=True,                # 创建机器人
                usd_path=jetbot_asset_path,       # 模型路径
                position=np.array([0, 0.3, 0])    # 初始位置
            )
        )
        # 获取Franka机械臂并设置位置
        pick_place_params = self._pick_place_task.get_params()
        self._franka = scene.get_object(pick_place_params["robot_name"]["value"])
        self._franka.set_world_pose(position=np.array([1.0, 0, 0]))  # 当前位置
        self._franka.set_default_state(position=np.array([1.0, 0, 0]))  # 默认位置
        return

    def get_observations(self):
        # 获取Jetbot位姿
        current_jetbot_position, current_jetbot_orientation = self._jetbot.get_world_pose()
        # 合并任务观察数据（包括子任务数据）
        observations = {
            "task_event": self._task_event,  # 当前任务阶段
            self._jetbot.name: {
                "position": current_jetbot_position,      # 位置
                "orientation": current_jetbot_orientation,  # 方向
                "goal_position": self._jetbot_goal_position  # 目标位置
            }
        }
        observations.update(self._pick_place_task.get_observations())  # 添加子任务数据
        return observations

    def get_params(self):
        # 获取任务参数（包括子任务参数）
        pick_place_params = self._pick_place_task.get_params()
        params_representation = pick_place_params
        params_representation["jetbot_name"] = {"value": self._jetbot.name, "modifiable": False}
        params_representation["franka_name"] = pick_place_params["robot_name"]
        return params_representation

    def pre_step(self, control_index, simulation_time):
        # 任务阶段0：Jetbot导航到目标
        if self._task_event == 0:
            current_jetbot_position, _ = self._jetbot.get_world_pose()
            if np.mean(np.abs(current_jetbot_position[:2] - self._jetbot_goal_position[:2])) < 0.04:
                self._task_event += 1  # 进入阶段1
                self._cube_arrive_step_index = control_index  # 记录到达时间步
        # 任务阶段1：Jetbot后退200步
        elif self._task_event == 1:
            if control_index - self._cube_arrive_step_index == 200:
                self._task_event += 1  # 进入阶段2
        return

    def post_reset(self):
        # 重置时打开Franka夹爪并重置任务阶段
        self._franka.gripper.set_joint_positions(self._franka.gripper.joint_opened_positions)
        self._task_event = 0
        return


class HelloWorld(BaseSample):
    def __init__(self) -> None:
        super().__init__()
        return

    def setup_scene(self):
        world = self.get_world()
        # 添加任务到世界
        world.add_task(RobotsPlaying(name="awesome_task"))
        return

    async def setup_post_load(self):
        self._world = self.get_world()
        # 获取任务参数和对象
        task_params = self._world.get_task("awesome_task").get_params()
        self._franka = self._world.scene.get_object(task_params["franka_name"]["value"])
        self._jetbot = self._world.scene.get_object(task_params["jetbot_name"]["value"])
        self._cube_name = task_params["cube_name"]["value"]
        # 初始化控制器
        self._franka_controller = PickPlaceController(
            name="pick_place_controller",  # Franka抓取控制器
            gripper=self._franka.gripper,
            robot_articulation=self._franka
        )
        self._jetbot_controller = WheelBasePoseController(
            name="cool_controller",  # Jetbot导航控制器
            open_loop_wheel_controller=DifferentialController(
                name="simple_control",
                wheel_radius=0.03,  # 轮子半径
                wheel_base=0.1125   # 轮距
            )
        )
        # 添加物理回调
        self._world.add_physics_callback("sim_step", callback_fn=self.physics_step)
        await self._world.play_async()  # 启动仿真
        return

    async def setup_post_reset(self):
        # 重置控制器
        self._franka_controller.reset()
        self._jetbot_controller.reset()
        await self._world.play_async()  # 重启仿真
        return

    def physics_step(self, step_size):
        current_observations = self._world.get_observations()
        # 阶段0：Jetbot导航
        if current_observations["task_event"] == 0:
            self._jetbot.apply_wheel_actions(
                self._jetbot_controller.forward(
                    start_position=current_observations[self._jetbot.name]["position"],
                    start_orientation=current_observations[self._jetbot.name]["orientation"],
                    goal_position=current_observations[self._jetbot.name]["goal_position"]
                )
            )
        # 阶段1：Jetbot后退
        elif current_observations["task_event"] == 1:
            self._jetbot.apply_wheel_actions(ArticulationAction(joint_velocities=[-8, -8]))
        # 阶段2：Jetbot停止，Franka抓取
        elif current_observations["task_event"] == 2:
            self._jetbot.apply_wheel_actions(ArticulationAction(joint_velocities=[0.0, 0.0]))
            # Franka执行抓取动作
            actions = self._franka_controller.forward(
                picking_position=current_observations[self._cube_name]["position"],
                placing_position=current_observations[self._cube_name]["target_position"],
                current_joint_positions=current_observations[self._franka.name]["joint_positions"]
            )
            self._franka.apply_action(actions)
        # 抓取完成后暂停仿真
        if self._franka_controller.is_done():
            self._world.pause()
        return
```

上面的代码中就是一个扩展Isaac Sim的脚本文件，在脚本文件中我们定义了两个类，分别是**BaseSample**以及**BaseTask**的子类，在这两个子类中我们能够实现基本的场景、机械臂、小车、夹取方块的加载以及任务的执行逻辑，其中BaseTask子类主要用于加载场景以及机器人实例，而BaseSample则确定了大概的仿真程序的执行逻辑流程

在编写完上面的脚本文件过后，可以直接启动Isaac Sim仿真程序，并在Isaac Sim的选项栏中的Window→Examples→Robotics Examples打开机器人的控制样例程序，<img src="D:\Soft\Typora\markdown_data\Isaac_Sim学习记录.assets\image-20250421151537780.png" alt="image-20250421151537780" style="zoom:33%;" />

然后我们就能在下面的Robotics Examples窗口栏中的GENERAL选项中加载HelloWorld样例程序（注意：脚本程序需要在容器Isaac-Sim文件管理器中extension_examples脚本文件夹中的hello_world/hello_world.py中修改），最后在Robotics Examples窗口栏中执行load场景，并进行仿真

![image-20250421151926253](D:\Soft\Typora\markdown_data\Isaac_Sim学习记录.assets\image-20250421151926253.png)



## 独立应用程序

独立应用程序完全不依赖Isaac Sim程序的启动，我们可以在Isaac Sim仿真程序完全没有运行的条件下执行我们想要的仿真结果，这程序进行仿真的特点是完全使用Python脚本启动Isaac Sim仿真程序，并且所有的渲染步以及时间步也都是通过代码控制的。

具体的实现步骤：

我们可以在Isaac-Sim容器的course-content/scripts文件夹中创建独立的应用程序文件，通过这个文件我们能够通过Vscode这种IDE直接编辑应用程序以及通过下面的方式来运行调试仿真应用程序：

<img src="D:\Soft\Typora\markdown_data\Isaac_Sim学习记录.assets\image-20250421152518518.png" alt="image-20250421152518518" style="zoom:45%;" />

而具体的程序文件的实现步骤应该为：

> 

> 1. 创建Simulaition仿真实例用于启动Isaac Sim仿真模拟器（默认无头模式：即在开启仿真器的时候不自动将渲染的仿真画面传回到屏幕上进行显示，节省了渲染资源），并建立渲染画面传输途径

> 2. 创建世界、以及默认的实体地面Prim，并加载机器人实体实例/机器人描述USD文件到世界的场景中

> 3. 实例化机器人/机械臂的控制器

> 4. 对仿真的任务的具体仿真逻辑，其中包括：

* 世界的场景渲染更新
* 机器人具体控制器的时候用逻辑
* 世界物理步进控制

> 5. 仿真完毕过后跳出仿真逻辑，并关闭仿真渲染以及仿真软件

具体的实现样例程序如下：

```python
from isaacsim import SimulationApp
import argparse
import sys

import carb

# 配置仿真应用参数
CONFIG = {
    "width": 1280,            # 渲染窗口宽度
    "height": 720,            # 渲染窗口高度
    "window_width": 1920,     # 应用窗口宽度
    "window_height": 1080,    # 应用窗口高度
    "headless": True,         # 无头模式（不显示图形界面）
    "hide_ui": False,         # 显示UI界面
    "renderer": "RaytracedLighting",  # 使用光线追踪渲染器
    "display_options": 3286,  # 显示选项（默认显示网格）
}

# 启动Omniverse仿真应用
kit = SimulationApp(launch_config=CONFIG)

from isaacsim.core.utils.extensions import enable_extension

# 设置Livestream相关参数
kit.set_setting("/app/window/drawMouse", True)  # 在流媒体中显示鼠标光标

# 启用WebRTC Livestream扩展（支持浏览器实时查看）
enable_extension("omni.kit.livestream.webrtc")

from isaacsim.core.api.objects import DynamicCuboid                             # 加载动态Cube类
from isaacsim.core.utils.stage import add_reference_to_stage
from isaacsim.robot.manipulators import SingleManipulator                       # 加载机械臂类，该类可以创建一个含有简单关节且具有一个夹爪的机械臂
from isaacsim.robot.manipulators.examples.franka.controllers.pick_place_controller import PickPlaceController   # 加载
from isaacsim.robot.manipulators.grippers import ParallelGripper                # 加载夹爪类
from isaacsim.storage.native import get_assets_root_path

import numpy as np
from isaacsim.core.api import World

my_world = World(stage_units_in_meters=1.0, physics_dt=1.0 / 120.0, rendering_dt=1.0 / 60.0) # 创建世界
my_world.initialize_physics()                                                   # 初始化物理仿真模拟
print(f"物理时间步长: {my_world.get_physics_dt()} 秒")  
print(f"渲染时间步长: {my_world.get_rendering_dt()} 秒")

# 添加默认地面
ground_plane = my_world.scene.add_default_ground_plane()                        # 在World世界中的场景类中添加默认的地面
# 输出地面路径
print(f"地平面的路径是: {ground_plane.prim_path}")

from isaacsim.core.api.objects import DynamicCuboid

# 添加立方体，并返回一个XFormPrim的对象，即Prim对象
cube = my_world.scene.add(                                                      # 在World世界的场景中添加一个立方体
    DynamicCuboid(
        name="cube",
        position=np.array([0.3, 0.3, 0.3]),                                     # 初始位置
        prim_path="/World/Cube",                                                # 在World关系图中的关系
        scale=np.array([0.0515, 0.0515, 0.0515]),                               # 缩放大小
        size=1.0,
        color=np.array([0, 0, 1]),
    )
)
# 输出物体路径
print(f"物体的路径是: {cube.prim_path}")

# 获取Isaac Sim 官方资产地址
from isaacsim.storage.native import get_assets_root_path
assets_root_path = get_assets_root_path()           # 获取isaac sim官方资产的根路径
print("assets_root_path:" + assets_root_path)

# 加载机械臂usd模型至场景"/World/Franka"路径
from isaacsim.core.utils.stage import add_reference_to_stage
asset_path = assets_root_path + "/Isaac/Robots/Franka/franka_alt_fingers.usd"
add_reference_to_stage(usd_path=asset_path, prim_path="/World/Franka")
print("机械臂模型加载成功!")

# 配置平行夹爪
from isaacsim.robot.manipulators.grippers import ParallelGripper

gripper = ParallelGripper(
    end_effector_prim_path="/World/Franka/panda_rightfinger",  # 夹爪末端效应器路径
    joint_prim_names=["panda_finger_joint1", "panda_finger_joint2"],  # 夹爪关节名称
    joint_opened_positions=np.array([0.05, 0.05]),  # 夹爪张开时关节位置（此处表示夹爪张开时间隙为 5cm）
    joint_closed_positions=np.array([0.0, 0.0]),    # 夹爪闭合时关节位置（此处表示夹爪闭合时间隙为 0cm）
    action_deltas=np.array([0.01, 0.01])            # 每次移动的步长夹爪增量为 1cm
)



my_franka = my_world.scene.add(
    SingleManipulator(
        prim_path="/World/Franka",  # 机械臂Prim路径
        name="my_franka", # 机械臂名称
        end_effector_prim_name="panda_rightfinger", #机械臂末端执行器Prim名称
        gripper=gripper # 夹爪对象
    )
)

my_franka.gripper.set_default_state(my_franka.gripper.joint_opened_positions)

from isaacsim.robot.manipulators.examples.franka.controllers.pick_place_controller import PickPlaceController

# 初始化夹取和放置控制器
my_controller = PickPlaceController(
    name="pick_place_controller", # 控制器名称
    gripper=my_franka.gripper, # 夹爪
    robot_articulation=my_franka # 关节系统
)

# 获取机械臂控制器
articulation_controller = my_franka.get_articulation_controller()

# 定义一个标识，用于判断是否需要重置仿真场景
reset_needed = False
# 停止仿真，准备进入主循环
my_world.stop()

# 当仿真引擎处于运行状态时，循环持续
while kit.is_running():
    # 每帧推进仿真时间，同时渲染更新场景
    my_world.step(render=True)

    # 如果场景已停止，并且尚未重置
    if my_world.is_stopped() and not reset_needed:
        # 将重置标志置为 True，下一帧进行重置
        reset_needed = True
    # 当仿真正在运行时
    if my_world.is_playing():
        # 如果需要重置场景
        if reset_needed:       
            # 重置仿真世界
            my_world.reset() 
            # 重置控制器状态
            my_controller.reset() 
            # 重置完成，标记为 False
            reset_needed = False

        # 获取当前仿真环境的观测数据
        observations = my_world.get_observations()

        # 根据当前状态和目标位置，计算下一步动作
        actions = my_controller.forward(
            # 获取物体抓取点
            picking_position=cube.get_local_pose()[0],  
            # 放置位置
            placing_position=np.array([-0.3, -0.3, 0.0515 / 2.0]), 
            # 当前关节位置
            current_joint_positions=my_franka.get_joint_positions(),  
            # 末端偏移量
            end_effector_offset=np.array([0, 0.005, 0]), 
        )

        # 将计算好的动作应用到机械臂仿真中
        articulation_controller.apply_action(actions)
    # 更新仿真引擎状态（包括渲染、逻辑更新等）
    kit.update()
```

编写完毕过后保存好，就能通过上面的调试工具直接运行，当出现了“Streaming server started”即表示Isaac Sim启动成功，这个时候我们就能通过isaacsim-webrtc-streaming-client渲染图形化程序进行查看仿真程序的仿真结果





# 学习问题：

### 什么叫做工作流

工作流其实就是指为了完成特定任务或业务流程而设置的一系列步骤的自动化或者结构化执行顺序，它定义了谁（who）在什么时间（when）做了什么事情（What），并确保任务按照预定的逻辑以及规则高效、无差错地运行

工作流的组成要素：

* 步骤：任务的具体操作
* 规则：决定流程如何运转
* 参与者：执行步骤的人、程序、系统或者服务
* 输入与输出：每个步骤的输入数据以及输出结果



### 我们在概念中学习到整体的仿真架构，但是为什么脚本文件中的操作Prim对象不是在Stage中进行操作的呢？而是在Scene中操作的呢？

因为Stage其实就像是一个管理者，它一般都是隐居于幕后虽然在python脚本中，并没有使用到Stage对象，但是Stage在Isaac Sim中还是非常重要的，它负责管理场景中的所有Prim对象，它作为一个容器，存储了场景中的所有对象、对象的层级结构、属性以及动画等信息

尽管我们并不需要操控Stage，但是我们主要操作的XFormPrim对象在创建的时候就已经封装了Stage的底层细节，以至于我们可以完全不用关心Stage的内部实现细节





SingleRigidPrim：高层的封装的用于处理刚体Prim的属性与特性





### 怎么样实现将一个对象a嵌入到另一个对象b中，并以对象b作为上级呢？

我们可以通过将实例化的对象a作为参数传入到另一个对象b的实例函数中去，并且在这样对象b保存这个对象a到自己的内部，并且可以使用@property装饰器将对象a的名字作为父对象b的属性来进行访问，并且@property装饰器装饰的函数最终返回存储了传入对象a的属性值即可









步进如此，当按下load按钮的时候还会启动协程setup_post_load函数并运行其中的内容

（并且这些setup_post_load、setup_scene函数都是还是抽象方法，这些函数是必须要在子类中进行定义的）

load过程中还会将task通过add_physics_callback添加预步进操作





### 为什么task对象又会与observations有关系，为什么能从task对象中获取observations呢？

这是因为如下图：World.get_observations()函数传入的参数是相应的task_name最后获取的依旧是task对象中定义个get_observations函数的内容，因此就能直接获取对应task中的observation观察参数，默认的task_name传入的参数是None，那么就会获取所有task的observation观察值

<img src="D:\Soft\Typora\markdown_data\Isaac_Sim学习记录.assets\image-20250421114612294.png" alt="image-20250421114612294" style="zoom:67%;" />





### task到底在底层中是怎么执行的，为什么task那么重要

当我们按下load按键的时候，BaseSample对象将会被创建，并且他的异步程序将会自动的创建一个世界，并进行初始化

然后当我们使用self._world.add_task()函数的时候，将会将task对象存储到task表中

同时在创建世界的同时还会自动生成一个场景，因此我们能直接加载场景，并在场景对象中添加所需要的Prim对象、

并且在还会运行BaseSample类中的load_world_async函数的内容

![image-20250418172939739](D:\Soft\Typora\markdown_data\Isaac_Sim学习记录.assets\image-20250418172939739.png)

当world实例化过后，执行reset()函数的时候，将会自动将self._current_tasks字典中的所有的task任务都自动执行task实例的set_up_scene()函数，以此来实现task任务的自动执行

在BaseSample对象中的当按下load按钮进行场景的加载时将会自动执行BaseSample对象中的load_world_async()函数，并自动执行BaseSample中定义的setup_scene()函数吗，然后进行仿真图像的初始化，在初始化的同时进行task的set_up_scene函数的执行，并暂停仿真图象的渲染，然后获取task任务表，然后执行setup_post_load()函数





官方文档中提到：

[Core [omni.isaac.core\] — isaac_sim 4.2.0-rc.17 documentation](https://docs.omniverse.nvidia.com/py/isaacsim/source/extensions/omni.isaac.core/docs/index.html?highlight=basetask#omni.isaac.core.tasks.BaseTask)

BaseTask类提供了一种途径，去建立一个task在场景中，并且模块化的添加一个对象到舞台中，同时得到所需要的行为层观察数据



我们要找的是task为什么需要存在

task到底传入到scene中的时候到底做了什么

执行了场景的设置、创建等操作

task执行就是通过add_task函数添加task，然后加载到self._current_task字典中，然后开始执行task类中的set_up_scene()函数中的内容并进行动态的修改场景





合成数据

数据孪生，通过Isaac Sim来创建真实的场景，然后进行产生数据









### 怎样让一个物体拥有刚性，机器人跟它碰撞后效果如何？这个效果背后是如何产生的？

答：使得物体的Attribute Name中的type转为刚体类型，并且需要具有碰撞网络，在进行仿真的时候，而为了模拟机器人的碰撞之间的交互，Isaac Sim使用了碰撞器（Colider）的概念，碰撞器用于定义物体的碰撞形状和边界的组件，它通常与刚体并包含碰撞网络的属性一起使用，碰撞器可以是各种形状，以适应Prim对象的具体形状

要使得机器人产生碰撞效果：我们就需要在Prim的物理引擎中启动Collision Enable(启动碰撞)，当启动该选项的时候，物体的碰撞器则能够与其他的碰撞器发生碰撞

而碰撞器会根据碰偏移参数、碰撞效果的进行进一步的碰撞参数、形变参数等具体碰撞参数的计算，并进一步将这种效果渲染出来

下图中描述了碰撞偏移以及静止偏移两种参数：

* 碰撞偏移：从碰撞几何体表面起开始生成接触的距离，如果接触偏移值越大，那么物体会在彼此靠近时会提前检测到碰撞，即如果过大，将会使得物体并没有相互碰撞到就会立刻发生弹性偏移
* 静止偏移：物体在碰撞后静止时的偏移距离。该值影响碰撞后的物体间距

![image-20250421111348535](D:\Soft\Typora\markdown_data\Isaac_Sim学习记录.assets\image-20250421111348535.png)



### 怎样让机器人拥有移动的能力？这个移动能力背后的原理是什么？

答：需要使用到如关节控制器Articulation关节控制器、自定义差速控制器、底层转子控制器或者Isaac Sim底盘控制API提供给机器人实例控制器对象，同时apply_aciton函数来接收关节控制器的关节速度、差速控制器传出的前进速度以及角速度、底层轮子控制器传出的数据来进行移动

而差速控制器首先在程序中是先实例化预先设置好机器人的轮子的具体尺寸以及轮距等参数，并对后面传入的具体的期望速度，进行后台的转速算法计算，进而控制底盘的电机速度控制



### 轮式机器人在仿真场景运动时，摩擦力是如何产生的？

答：摩檫力是通过世界节点的参数，通过物理求解器进行现实物理仿真计算的，具体点来说就是通过Prim实例的材质属性的具体参数进行计算的，这里的<u>材质</u>是预先设置碰撞网络、材料的摩擦系数等参数，而这些材料通常是先存储到<u>looks组</u>中的，looks组相当于一个独立的机器人组成部件的所有使用材料的总和（可以理解成一个机器人所用材质的字典）

字典中有不同的外表材质，这些材质，后面的机器人组成部件的Prim的材质属性就会从这个字典中获取的，即Prim的材质属性与Looks组中的材质元素之间是有链表关系的





### 通过Python API 运行Isaac Sim应用，怎样能让它通过Isaac Sim WebRTC Streaming Client 进行访问？背后的原理是什么

具体代码：

```python
import argparse

from isaacsim import SimulationApp

parser = argparse.ArgumentParser()
parser.add_argument("--test", default=False, action="store_true", help="Run in test mode")
args, unknown = parser.parse_known_args()

from isaacsim import SimulationApp

# 调整后的配置
CONFIG = {
    "width": 1280,
    "height": 720,
    "window_width": 1920,
    "window_height": 1080,
    "headless": True,
    "hide_ui": False,  # Show the GUI
    "renderer": "RaytracedLighting",
    "display_options": 3286,  # Set display options to show default grid
}

simulation_app = SimulationApp(launch_config=CONFIG)

from isaacsim.core.utils.extensions import enable_extension

# 开启鼠标键盘输入
simulation_app.set_setting("/app/window/drawMouse", True)

# 开启WebRTC连接
enable_extension("omni.kit.livestream.webrtc")

import carb
import numpy as np
from isaacsim.core.api import World
from isaacsim.robot.wheeled_robots.controllers.differential_controller import DifferentialController
from isaacsim.robot.wheeled_robots.robots import WheeledRobot
from isaacsim.storage.native import get_assets_root_path
```

其中Simulation实例就是仿真软件本身，当实例化完成其实就已经启动的仿真软件以及仿真引擎

而enable_extension()函数则是建立了与仿真软件的渲染传输通道，通过这个通道我们能够在Client中看到实时的渲染画面，并进一步的控制Isaac Sim仿真软件



### 完成机械臂、轮式机器人任务开发，常见Python API 有哪些？这些 API的作用分别是什么？

答：

> 控制机械执行指定操作isaacsim.robot.manipulators.examples.franka.Franka.get_object(object_name).apply_action(actions)

>  创建世界：isaacsim.core.api.World()
> 为世界添加任务：isaacsim.core.api.World().add_task(task_object())
> 给世界的场景添加Prim：isaacsim.core.api.World.scene.add()

> 获取世界中的某个Prim：BaseSample.get_world.scene.get_object(Prim_name)
> 设置世界在仿真过程中要执行的回调函数：BaseSample.get_world.add_physics_callback("sim_step", callback_fn)
> 获取世界观察的数据：BaseSample.get_world().get_observations()
> 启动仿真：BaseSample.get_world().play_async()
> 暂停仿真：BaseSample.get_world().pause()

> Cube对象实例：isaacsim.core.api.objects.DynamicCuboid
> 机械臂对象实例：isaacsim.robot.manipulators.examples.franka.Franka()
> 轮式机器人对象实例：isaacsim.robot.wheel_robots.WheeledRobot(prim_path:str, name:str, wheel_dof_names:List<str>, create_robot:bool, usd_path:str)

> 实例化机械臂抓取、放置控制器：isaacsim.robot.manipulators.examples.franka.controllers.PickPlaceController
> 轮式机器人控制器：isaacsim.core.api.controllers.BaseController
> 关节控制器：isaacsim.core.utils.types.ArticulationAction(joint_velocities)
> 控制器基类：isaacsim.core.api.controllers.BaseController



### 参考课程的案例，实现Jetbot 机器人导航任务的**独立**Python 脚本如何编写？

> 答：要实现Jetbot机器人的导航任务可以通过一下步骤来实现：

> 1. 创建Simulaition仿真实例用于启动Isaac Sim仿真模拟器（默认无头模式：即在开启仿真器的时候不自动将渲染的仿真画面传回到屏幕上进行显示，节省了渲染资源），并建立渲染画面传输途径

> 2. 创建世界、以及默认的实体地面Prim，并加载机器人实体实例/机器人描述USD文件到世界的场景中

> 3. 实例化机器人/机械臂的控制器

> 4. 对仿真的任务的具体仿真逻辑，其中包括：

* 世界的场景渲染更新
* 机器人具体控制器的时候用逻辑
* 世界物理步进控制

> 5. 仿真完毕过后跳出仿真逻辑，并关闭仿真渲染以及仿真软件

​	而如果不是独立的python程序，而是使用

> 1. 建立HelloWorld实例

> 2. 编写实例程序的初始化场景函数，在该函数中首先我们需要进行加载世界、地面实例、机器人实例到场景中

> 3. 编写实例程序在点击加载按钮进行加载场景时的操作函数，在该函数中，我们可以将世界、机器人对象、以及后续对机器人的操作的控制器进行加载以及初始化

> 4. 编写对机器人进行操作时的物理回调函数，这个物理回调函数是当程序进行仿真的时候出现时间不仅的时候会自动的回调执行，即每步进一次就返回来执行一次这个函数
>    在这个函数中，我们可以定义机器人传感器数据获取、机器人执行操作的指令，进而实现对机器人控制信息的获取并且最终传入到控制器中





### 一个依靠Isaac Sim的程序应该怎么设计：

如果要实现一个完整的仿真脚本程序可以有一个怎么样的顺序来编写脚本代码？
脚本程序的仿真类程序实现步骤：
1. 导入相应需要使用的节点、对象、功能包
2. 创建仿真对象，当然也可以使用task对象，并在主仿真对象中使用这个task对象
3. 创建的仿真对象中，程序的大概步骤分为：
	* 定义初始化设置
	* 定义初始化场景的函数，可执行的任务为：初始化场景、获取数据等等
	* reset函数，这个函数一般需要定义为当按下reset按键进行充值的时候所需要执行的操作
	* 如果是使用了task命令，则需要在task命令中设置为：
		* 设置场景的加载操作
		* 设置执行任务是所需要的功能操作，task多数是设置与定义
		最后还是需要在BaseSample类中定义执行仿真任务的具体任务，





