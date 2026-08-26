Mujoco仿真都是环绕着 `mjModel` 和 `mjData` 两个结构体展开的

# mjModel



`mjModel` 就是仿真环境中所有不变、静态的实体

# mjData

`mjData` 则就像是机器人的 <u>状态记录仪</u> 或者说是 <u>运行时数据</u> ，例如：机器人的每个关节的角度、速度、受力	



mjModel 和 mjData 一般不是由用户直接分配，在mujoco中一般是使用相应的 API 函数进行读取xml模型文件的方式去分配和初始化，



# Python

在python中的mujoco包中，`mujoco.viewer` 模块中提供了一个**交互式GUI查看器**，该查看器主要有三种不同的使用场景：**托管查看器**、**独立应用程序**与**被动查看器**



## 托管查看器







