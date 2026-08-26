

![img](https://pic3.zhimg.com/80/v2-16f8adca3758174cbe20599f99521b22_1440w.webp)

# GUI

GUI:图形用户界面吗，是指采用图形方式显示计算机操作用户界面

 GUI库：图形用户界面库，只需要调用GUI库的函数即可快速绘制出所需要的用户界面





# 优化LVGL运行效果的方法

- 提高芯片主频
- 增大SRAM容量、提高读写速度
- 增大图形缓冲区、使用双缓冲
- 减小需要刷新的总像素
- 提高图形数据的传输速度

优化运行下效果的关键就是：**缩短图像刷新所需要的时间**



# LVGL库文件介绍

![1702967282897](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1702967282897.png)





# LVGL移植的关键点





# LVGL移植整体流程

1. 确定输入、输出设备

例如：输入：触摸屏、鼠标、键盘以及编码器；输出：显示屏



2. 确定所需的可选功能

例如：屏幕上护具传输方式、系统、SRAM、内存管理算法



3. 准备LVGL库、例程

准备指定版本的LVGL库文件，还有支持所需功能的例程源码



4. 添加LVGL库到工程中

按需要裁剪、修改LVGL库文件，并添加到MDK工程中



5. 配置输入、输出设备

适配自己的输入和输出设备，添加所需功能



6. 提供心跳、测试

为LVGL提供时钟（时基），写测试代码检测移植是否成功





# LVGL对象

LVGL采用面向对象的编程思想，它的基本构造块是对象（实例），我们所说的所有的部件都是由一个一个对象构成的

一般的LVGL类定义了部件的抽象特点，其定义包含了数据的形式以及对数据的操作，部件（子类）比原本的类（称为父类或基类）要更加具体化，子类会继承父类的属性以及行为



在LVGL中， 所有的对象都在lv_obj_t这个结构体的基础上进行演变 ，所以我们就看到了各种不同的部件，就算是一样的部件，继承基础父类（基类）之后演变出来对象（实例）的形态或风格样式都不一样（就像狗有不一样的品种，不一样的品种就有不一样的体型、外观等等 、

![1703498763397](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1703498763397.png)



## LVGL基础对象（lv_obj）

screen（屏幕）是没有父类的一个类，我们可以将其看成为**基类**



一个LVGL的界面一般有三层的屏幕，这三个屏幕分为**用户层、顶层、系统层**

- 用户层：用于显示主要界面的层
- 顶层：用于特殊处理的层
- 系统层：权限最大的层，例如鼠标图标所在的层，就是系统层，这一层可以在任何时间都能移动，并且不受其他层影响

![1703514166135](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1703514166135.png)



## LVGL基础对象的大小

### 设置大小

- 设置基础对象大小的函数为：

```
lv_obj_set_width(obj, new_width);

:obj > 要设置的部件对象
:new_width > 部件对象要设置宽度的大小
```

- 设置高度

```
lv_obj_set_height(obj, new_height);

:obj > 要设置的部件对象
:new_height > 部件对象要设置高度的大小
```

- 同时设置宽度、高度

```
lv_obj_set_size(obj, new_width, new_height);

:obj > 要设置的部件对象
:new_width > 部件对象要设置的宽度
:new_height > 部件对象要设置的高度
```



### 获取大小

- 获取对象的宽度：

```
lv_obj_get_width(obj);

:obj > 要获取宽度的对象
```



- 获取高度：

```
lv_obj_get_height(obj);

:obj > 要获取高度的对象
```





## 基础对象的位置

### LVGL屏幕的原点

LVGL屏幕的坐标与我们熟悉的坐标系不一样，LVGL的坐标系是“LCD坐标系”，它的原点位置与直角坐标系不一样

![1703516375817](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1703516375817.png)

其相当于平面直角坐标系中的第四象限

当确定了坐标系类型后我们就可以确定原点，确定了原点我们就可以设置、确定LVGL部件（对象）的位置

![1703516540424](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1703516540424.png)

### 设置对象的坐标位置

- 设置x轴坐标位置：

```
lv_obj_set_x(obj, new_x);

:obj > 要设置位置的对象
:new_x > 对象在平面坐标的x轴位置
```



- 设置y轴坐标位置：

```
lv_obj_set_y(obj, new_y);

:obj > 要设置位置的对象部件
:new_y > 对象在平面坐标的y轴位置
```



- 同时设置x、y坐标位置：

```
lv_obj_set_pos(obj, new_x, new_y);

:obj > 要设置位置的对象部件
:new_X > 对象在平面坐标的x轴位置
:new_y > 对象在平面坐标的y轴位置
```



### 设置对象对齐

- 参考父对象对齐：

```
lv_obj_set_align(obj, LV_ALIGN_...);

:obj > 要进行对齐的操作的对象部件
：LV_ALIGN_... > 要如何对齐的枚举类型变量，具有的对齐方式如下
```

![1703519786229](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1703519786229.png)

具体的这些操作具体的位置参考如下：

![1703519831469](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1703519831469.png)



- 参考父对象对其后再设置坐标位置

```
lv_obj_align(obj, LV_ALIGN_..., x, y);

:obj > 要进行对齐操作的对象部件
:LV_ALIGN_... > 要进行对齐的枚举类型变量，具体的对齐方式如上
:x > 在对齐过后需要偏移的x轴的位置
:y > 在对齐过后需要偏移的y轴的位置
```



- 参照另一个对象（无父子关系）对齐后设置坐标位置

```
lv_obj_align_to(obj_to_align, obj_reference, LV_ALIGN..., x, y);
:obj_to_align > 要进行对齐操作的对象
:obj_reference > 进行对齐操作的参考的对象
:LV_ALIGN_... > 要进行对齐的枚举类型变量，具体的对齐方式如上
:x > 进行对齐操作过后需要偏移的x轴位置
:y > 进行对齐操作过后需要偏移的y轴位置
```



### 获取对象位置

- 获取x轴坐标位置

```
lv_obj_get_x(obj);

:obj > 要获取坐标的对象

```



- 获取y轴坐标位置

```
lv_obj_get_y(obj);

:obj > 要获取坐标的对象	
```





## 基础对象的盒子模型

对于一个基础界面来说，我们可以将将其看作一个盒子，这个盒子的窗口大小是固定的，但盒子的大小可以说是无限大的

而这个大盒子里面的部件，我们又可以想象成一个个的小盒子

![1703554941525](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1703554941525.png)

像上面的，整个蓝色框框起来的是我们的基类窗口，然后我们可以将这个窗口看作一个盒子，这个盒子里面又装了红色框中的窗口对象，我们将这个窗口对象又看作一个盒子，这个盒子里面又能装下一个盒子对象	



#### LVGL对象的盒子模型

LVGL遵循CSS的border-box模型。对象的盒子由以下部分构成：

![img](https://img-blog.csdnimg.cn/bdcc3c23acf045d6b479a7b46867db0b.png)

这里的黄色部分就是基类盒子的实际大小，

灰色部分就是轮廓部分



具体的参数有：

- 边界（bounding) :元素的宽度/高度围起来的区域（整个盒子）
- 边框（border）:边框有大小与颜色等属性（相当于盒子的边缘厚度以及颜色）
- 填充（padding）：对象两侧与其子对象之间的空间（盒子的填充物），使对象处于盒子中的某个指定地方，相当于月饼盒子中的隔开月饼的填充物
- 内容（content）：通过边框与填充设置过后的对象窗口，可以理解成用于实际存放内容的窗口
- 轮廓（outline）：LVGL中没有外边距的概念（盒子与盒子之间的距离），取而代之的使轮廓（outline）。它使绘制与元素（盒子）周围的一条线，它不占据空间，位于边框边缘的外围，可起到突出元素（盒子）的作用， 当鼠标点击或使用Tab键让一个选项或者一个图片获得焦点的时候，这个元素就会多了一个轮廓框围绕，当然我们也可以将其理解成外边距，将这个视作两个对象之间相隔的距离



#### 设置盒子模型参数

```
lv_obj_set_style_border_width(obj, )

```





## LVGL的基础对象样式

**样式**：用名称保存下来的一组修饰对象的参数，这参数可以使修饰对象有各种各样的不同的样子

对对象进行样式优化的作用是：优化用户体验



样式存储在lv_style_t变量中。样式变量应该是**静态**、**全局**或**动态分配**的。它们不能是函数中的局部变量，因为当函数执行完毕过后，局部变量会被销毁 



#### 设置样式属性

`注：`在设置样式属性之前需要先初始化一个样式对象

初始化代码：

```
static lv_style_t style_obj;   // 实例化样式对象,这个对象应该是静态、全局、或是动态分配的
lv_style_init(&style_obj); 	   // 样式对象初始化
```



当我们初始化好一个样式过后就可以设置它的样式属性了，接口函数是这样的：



```
lv_style_set_<property_name>(&style, <value>)

:&style > 要设置样式的样式对象的地址
:value > 要设置的样式的参数属性
```

示例：

```
lv_style_set_bg_color(&style_obj,lv_color_hex(0x00000));    // 设置背景色
lv_style_set_bg_opa(&style_obj, LV_OPA_50);    // 设置背景透明度

```

 

#### 添加样式到对应的对象			  	

样式本身并不会直接发挥作用。只有将其分配给对象使用才能生效。对应添加和移除函数

对象添加样式：

```
lv_obj_add_style(obj, &style, <selector>)

:obj > 要设置样式的窗口对象
:&style > 要使用的已经初始化并设置属性的样式对象
:selector > 样式对应的Parts或State，可以通过或运算设置多个Parts或State
```

对象移除样式：

```
void lv_obj_remove_style(struct _lv_obj_t * obj, lv_style_t * style, lv_style_selector_t selector);

:obj > 要设置样式的窗口对象
:*style > 窗口对象要使用的样式对象指针
:selector > 样式要作用的Parts或State，可以使用或运算设置多个Parts或State
```



#### LVGL对象的状态（State）

窗口对象所处的状态可以是以下的状态：

```
enum {
    LV_STATE_DEFAULT     =  0x0000,    //正常，释放状态
    LV_STATE_CHECKED     =  0x0001,    //切换或检查状态
    LV_STATE_FOCUSED     =  0x0002,    //通过键盘或编码器聚焦或通过触摸板/鼠标点击
    LV_STATE_FOCUS_KEY   =  0x0004,    //通过键盘或编码器聚焦，但不通过触摸板/鼠标聚焦
    LV_STATE_EDITED      =  0x0008,    //由编码器编辑
    LV_STATE_HOVERED     =  0x0010,    //鼠标悬停（现在不支持）
    LV_STATE_PRESSED     =  0x0020,    //被按下
    LV_STATE_SCROLLED    =  0x0040,    //正在滚动
    LV_STATE_DISABLED    =  0x0080,    //禁用状态
 
    LV_STATE_USER_1      =  0x1000,    //自定义状态
    LV_STATE_USER_2      =  0x2000,    //自定义状态
    LV_STATE_USER_3      =  0x4000,    //自定义状态
    LV_STATE_USER_4      =  0x8000,    //自定义状态
 
    LV_STATE_ANY = 0xFFFF,    /**< Special value can be used in some functions to target all states*/
};
```

可以通过<u>或运算</u>组合状态。另外，状态是有优先级的，**高位的优先级更高**，即LV_STATE_CHECKED的优先级高于LV_STATE_DEFAULT。



#### LVGL对象的部分（Parts）

对象可以分为多个Parts，例如一个Slider包含三个部分：背景、指标、旋钮。一个对象可以包含的部分有：

```
enum {
    LV_PART_MAIN         = 0x000000,   /**类似矩形的背景*/
    LV_PART_SCROLLBAR    = 0x010000,   /**滚动条*/
    LV_PART_INDICATOR    = 0x020000,   /**指标，例如用于滑块、条、开关或复选框的勾选框*/
    LV_PART_KNOB         = 0x030000,   /**旋钮*/
    LV_PART_SELECTED     = 0x040000,   /**表示当前选择的选项或部分*/
    LV_PART_ITEMS        = 0x050000,   /**如果小部件具有多个相似元素（例如表格单元格）*/
    LV_PART_TICKS        = 0x060000,   /**刻度上的刻度，例如对于图表或仪表*/
    LV_PART_CURSOR       = 0x070000,   /**标记一个特定的地方，例如文本区域或图表的光标*/
    LV_PART_CUSTOM_FIRST = 0x080000,   /**可以从这里添加自定义部件*/
    LV_PART_ANY          = 0x0F0000,   /**针对所有的Parts*/
};
```

`注意：`

**一个对象可以使用多个样式给它的部件**

**并且一个样式可以给多个对象使用**



#### 本地样式

除了普通的样式外，对象还可以存储本地样式。

本地样式与普通样式类似，但是它不能在其他对象之间共享

本地样式的接口函数：

```
lv_obj_set_style_<property_name>(obj, <value>, <selector>);

:obj > 要设置样式的窗口对象
:value > 设置样式的属性参数
:selector > 样式要作用的Parts或State，可以使用或运算设置多个Parts或State
```

例如:

```
 lv_obj_set_style_bg_color(obj, lv_color_hex(0xffff), 0); // 设置背景颜色
 lv_obj_set_style_bg_opa(obj, LV_OPA_50, 0);  // 设置背景透明度
 lv_style_set_...
  

```



`注意：`本地样式的优先级比普通样式高



#### 样式继承 

> 某些属性（通常与文本相关）可以从父对象的样式继承。

例如：

![1703582653934](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1703582653934.png)

上面的代码先设置了一个样式对象，这个样式对象要求字体变成橙色

而在下面我们为obj这个窗口对象创建了一个文本成员，然后将obj这个对象设置为当被按下时，将应用样式对象中的样式

但由于label这个对象的父类是obj，因此这个对象将会继承父类obj中的文本样式，因此在按下窗口对象的时候，label这个对象中的文本也将转为橙色



## 基础对象的事件

事件就是当发生某件特定的事情的时候，所要呈现的效果

简单来说时间其实就是用户与界面进行交互，当用户触发了某个特定的条件时，就使用指定的接口进行处理



#### 添加事件

```
lv_obj_add_event_cb(obj, event_cb, event_code, user_data);

:obj > 事件要绑定的窗口对象
:event_cb > 当事件触发的时候所要使用的回调处理函数
:event_code > 事件如何触发，事件类型
:user_data > 用户数据
```



事件类型有5个大类：

- 输入设备事件（input device events）
- 绘图事件（Drawing events）
- 其他事件（Other events)
- 特殊事件（Special events)
- 自定义事件（Custom events)

`注意`：在定义回调函数的时候，需要在定义回调函数的时候传入lv_event_t \* e这个参数，使得回调函数能够**接收到触发事件的相关信息**，例如事件类型、目标对象、触发对象等



### 父对象与子对象之间的关系

![1703733211678](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1703733211678.png)



# LVGL标签部件

在LVGL中，标签部件主要用于文本显示，例如标题、提示信息等

标签的组成部分：

- 主体部分（LV_PART_MAIN）
- 滚动条（LV_PART_SCROLLBAR）
- 选中的文本（LV_PART_SELECTED）



## 创建标签部件

```
lv_obj_t * label = lv_label_create(parent);

:parent > 要以哪个对象作为父对象，如果设置了某个对象，则标签将为父对象的指定部件
```



## 设置标签文本的三种方法

1. 直接设置文本，存储文本的内存动态分配：

```
lv_label_set_text(label, content);

:label > 要设置文本的标签对象
:content > 要给对象设置的文本内容（使用双引号括起）
```

例:![1703734370021](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1703734370021.png)





2. 文本不存储在动态内存中，而是在指定的缓冲区中（**慎用**）：

```
lv_label_set_text_static(label, content);

:label > 要设置文本的标签对象
:content > 要给对象设置的文本内容（使用双引号引起）
```

例：![1703734388389](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1703734388389.png)

`注意`：这种方法存储的文本不是动态分配的，其只是存储在缓冲区中，当需要使用这个文本的时候，将会去指定的缓冲区中寻找，这**种方法的内存占用相对较小，但如果缓冲区的内容被更改或者是被释放，那么这时从缓冲区获得的数据将会是不可靠的。**并且如果当缓冲区是只读的话，如果使用这种方法来写入，缓冲区就可能发生崩溃



3. 格式化显示文本， 类似printf:

```
lv_label_set_text_fmt(label, content, fmt);

:label > 要设置文本的标签对象
:content > 要给对象设置的文本对象（使用双括号引起，并且可以使用格式化方法）
:fmt > 要进行格式化的内容	
```

例：![1703734401966](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1703734401966.png)



## 设置文本的样式

### 1.设置文本样式

- 背景颜色

    - ```
        lv_obj_set_style_bg_color(label, lv_color_hex(0xFFF), STATE);
        
        :label > 要设置背景颜色的标签对象
        :lv_color_hex(0xXXX) > 要设置的背景颜色
        :STATE > 要触发将标签的背景颜色设置为背景色的方式
        ```

        

    `注意`： 默认情况下，标签的背景颜色是全透明的，因此我们在需要设置标签背景的时候应该先将背景透明度设置一下，范围值为0-255，**越大的值越不透明**，当然也可以使用<u>LV\_OPA\_XXX</u>这个枚举对象



- 字体大小

    - ```
        lv_obj_set_style_text_font(label, &lv_font_montserrat_xx, LV_STATE_xxx);
        
        :label > 要设置字体大小的标签对象
        :lv_font_montserrat_xx > 
        :LV_STATE_xxx > 要触发将字体设置为指定大小的方式
        
        ```

        

