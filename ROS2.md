# ROS2与ROS1的区别

1. 架构的颠覆：

    * Ros1架构下，所有节点都需要使用Master进行管理，一旦Master崩溃，则所有节点都无法使用
    * Ros2架构下，通讯使用了基于DDS的Discovery机制，不再使用master节点机制，

    ![image-20250406181217766](E:\Markdown\markdown\ROS2.assets\image-20250406181217766.png)

2. API的重新设计：

    * ROS2重新设计了用户API，但其使用方法与ROS1相似

3. 编译系统的升级：

    * ROS1使用了rosbuild、catkin进行管理项目
    * ROS2使用了升级版的ament、colcon