

![1700277749779](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1700277749779.png)





# PCB基本结构

## 1. 铜层

PCB的铜层一般都是以两层的倍数作为层数的

![1701352474604](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1701352474604.png)





## 2.阻焊 

PCB板上会覆上一层油漆、这个油漆就叫做**阻焊层**，阻焊层的作用就是保护线路， 把我们的铜线保护好，让其不受空气的氧化，如果阻焊层失效，那么就会导致PCB板的线路的氧化，进而可能失效，同时他还会将除了线路以及线路不需要焊接的地方覆盖起来，只留下焊盘，剩下的都覆盖起来，可以使得焊锡无法焊到板子上，因此这层油漆就叫阻焊层



## 3.丝印层

丝印层是在阻焊层之上的一层，丝印层其实就是在电路板上印上了字，一般情况下，这些字被称之为**位号**，他表示了**元器件的焊接位置**以及使用的**元器件简称符号**



## 4.PCB的本质

PCB板的顶层结构其实就是一副二值图形，表示的是黑色的是镂空的，红色的地方则就是不透光的

![1701353101371](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1701353101371.png)

有了这副图像，当你将这张图像发给生产厂，生产厂就会做出这个胶片出来，通常这个发送的文件就叫做**GERBER文件**（光绘文件），当PCB每一层都有这样的文件的时候，生产厂就会生产一张这样的胶片出来，生产出一张如下图一样的胶片出来

![1701353266502](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1701353266502.png)

有了胶片过后，生产厂就会开始制作PCB板，其制作的原理就如下图所示

![1701353321868](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1701353321868.png)

其中底层蓝色的就是我们的电路板，这个电路板表面是铜层，它的上面没有任何东西，只有一层**光敏胶**

然后我们使用一个紫外光源，然后在紫外光源的下方放上我们的胶片，然后通过一个镜头给胶片**成像**



### 显影

成像聚焦到光敏胶上，这个紫外光照到光敏胶上之后，光敏胶就会变性，变性过后我们就再使用丙烯之类的邮寄溶液进行清洗，这时没有被照射到的那部分光敏胶就会被洗掉，而曝光的光敏胶则保留



### 蚀刻

未经过曝光的干膜被显影液去除过后将会露出铜面，使用盐酸混合型药水将这部分露出的铜面溶解腐蚀掉，就得到了所需要的线路



### 退膜

将保护铜面的已经曝光的干膜用氢氧化钠溶液剥掉，露出线路图形



## 5.制作电路板时必须要满足的基础常规工艺指标

![1701354197844](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1701354197844.png)



## 6.元件

元件是需要我们画出来的，其次画一个元件还需要有以下的元素

1. 首先元件是放在元件库里的，叫做PCBLIB（PCB引脚库 ），在这个库中，每个元件都有其自己的名称
2. 其次每个元件都会有pad（引脚 ）每个pad都会有自己的pad号
3. 除了pad之外，元件还会有一个丝印的外框，这个丝印的外框还是很重要的，如果再画电路般的时候不画上，那么在画电路的时候，有可能芯片与芯片之间在空间上会发生干涉，这会导致芯片元器件焊接不上电路板



## 7.布局布线

**布局**：布局就是元器件与元器件之间的摆放位置的关系，器件并不是随意摆放的，一般而言器件的摆放位置一般是由两个因素确定的

1. 由前后板的连接关系确定的
2. 由信号的走向来确定的

**布线**：布线其实就是指元器件之间的铜线连接





## 8.叠层设计

![1701355164850](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1701355164850.png)

叠层设计一般用在6层板以上，例如上图所显示的就是一个典型的6层板，其中

第一层：信号层  （最佳信号层）

第二层：地层（一般是不分割的一整个地层）

第三层：信号层 （最佳信号层）

第四层：信号层 （次信号层）

第五层：电源层（电源层也是一般不分割的）

第六层：信号层（次信号层）





### 四层板设计

第一层：信号层

第二层：地层

第三层：电源层

第四层：信号层





## 9.原理图

走线连接的限定是由原理图限定的，整个PCB使用的元件也是由原理图限定的



### 原理图的基本要素

1. 元器件
2. 连线
3. 网名（连线网络的名称 ）

当两个元器件要连接到一起的时候，如果是较为复杂的元器件，我们就不能直接将其直接连接，反而可以通过标签的形式将其连接起来，其中**每个元件之间连接的那个引脚应该使用同一个标签名**表示两个元器件通过这两个引脚进行连接







# PCB的各层

![1710065066590](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710065066590.png)

## 1.机械层

机械层是定义整个PCB板的外观，其并不具有电气属性，因此我们可以在这一层中放心的勾画外形，机械尺寸以及放置文本等工作



## 2.信号层

![1710065180635](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710065180635.png)

信号层包含两层：顶层、中间层与底层，各层之间可通过盲孔、通孔和埋孔实现相互连接

![1710065269057](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710065269057.png)

​		

### 顶层

称之为元件层，主要用于放置元器件

![1710065346464](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710065346464.png)

当然对于双层板和多层板可以用来布置导线或覆铜



### 中间层

中间层最多可以有30层，在多层板中通常用于布置信号线，**注意**这里面不包含电源线与地线

### 底层

底层信号层也称焊接层，主要用于布线和焊接，对于双层板或多层板还可以用于放置元器件



## 3.内置电源层

通常简称内电层，仅在多层板中出现

![1710065578867](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710065578867.png) 同样的内电层与内电层、内电层与信号层之间可通过盲孔、通孔、埋孔进行连接



## 4.丝印层

丝印层定义顶层和底层的丝印字符，也就是在阻焊层之上印上的一些文字字符，比如元件名称，元件符号、元件管脚等信息，方便后面的电路焊接与差错等等



## 5.阻焊层

指的是需要使用油墨的层，该层不沾锡，它可以防止在焊接时相邻的焊接点的多余焊锡导致PCB短路，同时阻焊层还能将铜模导线覆盖住，防止其在空气中氧化











# PCB的基本设计流程

![1701356200299](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1701356200299.png)





![1705909302117](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1705909302117.png)

# PCB工程

一个完整的工程应该包含元件库文件、原理图文件、PCB库文件、网络表文件、PCB文件、生产文件

![1701586041359](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1701586041359.png)

 





# 元件符号

![1701586951060](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1701586951060.png)

原理图符号是元件在原理图上的表现形式，主要由**元件边框**、**管脚**（包括管教序号和管脚名称）、元件名称及元件说明组成，通过防止的管教来建立电器连接关系





# 原理图标注

![1701693610245](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1701693610245.png)



**更新原理图编号**：工具—》标注—》原理图标注

同样的也可以使用快捷键**taa**来打开原理图标注的页面，要更改所有的原理图编号需要将标号列的锁定勾选取消才能够更新对那个的编号

![1701693013653](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1701693013653.png)



如果想要对原理图中的某个部分重新编号，那么可以先选中要重新编号的部分，然后使用快捷键**TAA**，然后将标注范围更改位以下的选项，然后重复上面的步骤即可

![1701693446940](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1701693446940.png)





# 原理图查找元器件

由于大面积的原理图无法直接定位某个元器件的位号、网络标签所在的位置，我们可以通过跳转以及查找功能来实现定位查找

**查找快捷键**：ctrl+f

**跳转快捷键**：jc





## 批量放置

由于一些IC的管脚很多，如果我们一个个来放置的话将会相当的耗费时间，因此我们可以使用批量放置管教功能，

功能地址：**编辑（E）—》阵列式粘贴（Y）**或使用快捷键**E—》Y**

**功能使用方式：**

1. 选定对应列的第一个引脚

2. 使用快捷键EY使用阵列式粘贴功能

3. 指定对象数量（要批量放置多少个引脚）

4. ​        主增量（指定引脚的**管脚号Designator**的增量）

5. ​        次增量（指定引脚的**引脚名Name**的增量）

6. 设置间距，其中**正数的序号从下往上**

    ​						   **负数的序号从上往下**

    





## 对齐

管脚太多一个个的去排序或者是调整位置将会相当的耗费时间，因此我们可以使用软件的自动对齐功能直接调整每个管脚的位置

**功能使用方式：**

1. 选定要对齐的管脚或元器件
2. 使用快捷键a调出对齐选择栏

![1705975560389](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1705975560389.png)

3. 选择指定的对齐方式











# PCB设计流程

## 建立工程文件











## PCB建库

我们通常首先都是先建立PCB库，这是因为PCB库的数量比原理图库的数量会少得多



以下是PCB建库的具体流程：

### 元件起名

![1710064875691](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710064875691.png)

打开PCB库，并创建一个新的PCB元件

### 放置引脚

#### 焊盘防止

在设计所有东西前，我们都应该首先防止PAD（焊盘）

![1710066101291](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710066101291.png)



#### 焊盘大小设置

在放置前我们可以通过**TAB键**来设置其属性

通过选择layer中的焊盘所在的层就可更换其样式，

![1710066401022](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710066401022.png)

同时我们在下面的（x/y）选项中可以设置其指定的物理大小

![1710066417622](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710066417622.png)

同时焊盘的长度，是根据焊接需求来定义的，例如这里我们元件的引脚长度为2mm，我们可以将焊盘设置为1mm，使得引脚外有0.5mm，而引脚阴处有0.5mm，这样可以方便我们焊接，同时还能增加元件的机械强度，

然后在上面第二张图片中的Designator中设置焊盘编号即可



#### 焊盘横向间距

同时由于焊盘间也有间距，因此我们就可以使用吸附格功能了

我们可以右键，选择下图中的选项

![1710067103975](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710067103975.png)

具体22版本可选择选项：视图->栅格->设置全局捕捉山歌栅格![1710070739191](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710070739191.png)



#### 焊盘纵向间距

1. 选中所有需要调整的焊盘
2. 选择下面的选项

![1710070891135](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710070891135.png)

调出下图选项，我们选择select选项，并将其更改成same选项，这样我们在更改间距的时候就能批量选择我们刚才选定的4个焊盘进行更改了

![1710070963284](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710070963284.png)

确定过后，就会有一个批量修改窗口弹出，同时我们还能看到窗口的下面显示，

![1710071108454](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710071108454.png)

则证明我们完成了批量选择，现在可以对这4个焊盘进行横间距进行调整了

然后对Properties标签中的x/y处设置即可	

![1710072109421](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710072109421.png)



设置完过后可使用**R+M键**或**ctrl+M键**来测量是否准确

![1710072224022](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710072224022.png)

测量完毕后使用CLear删除测量标线

![1710072249162](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710072249162.png)





#### 设置原点中心

![1710072304943](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710072304943.png)

选中上图的选项过后，中心点就会自动设置到芯片的正中心



### 放置丝印

首先在放置丝印前，我们需要将所在的层切换到Top Overlay层

#### 设置吸附栅格大小

使用CTRL+G键调出设置吸附栅格窗口

![1710072522139](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710072522139.png)



#### 放置丝印

更改过后，我们就可放置丝印了，直接选择 放置->线条 选项 

![1710072735075](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710072735075.png)

然后绘制一个图形，这时我们可以直接画，由于栅格的存在，我们画出来的每一格就是栅格的大小，因此我们画一格即为上面需要设置的0.15，



#### 设置第一脚标识

由于我们的芯片不容易看出1脚，因此可以设置丝印来标识指定的1脚，我们可以直接将鼠标放到丝印的1脚附近的角点处，鼠标出现下图的标识后即可拖动丝印角进行调整

![1710072920724](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710072920724.png)



当然我们还有别的表示方法：

##### 引脚圆丝印

我们可以直接在1脚的旁边放上一个圆丝印，这也可以帮助我们判断

![1710073058136](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710073058136.png)



##### 更改焊盘形状

当然我们还可以直接将焊盘的属性改成round，圆角属性，这样也能直接看出1脚在什么地方

![1710073202869](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710073202869.png)

最后效果：

![1710073226754](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710073226754.png)



### 检查

最后我们还是需要使用快捷键ctrl+M来检查丝印的大小

![1710073312350](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710073312350.png)



### 放置3D外框

先将吸附栅格重新更改大小为1.5mm

并且更换所在层至机械层

#### 1.放置3D体

![1710073705067](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710073705067.png)

然后在画出所需大小的方框

![1710073749467](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710073749467.png)

然后双击选中设置3d体属性，将Overall Height（总高）设置为指定需要的高度

![1710073860979](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710073860979.png)



然后我们就可以使用3键来切换3d视角，然后使用shift+右键就可以拖动查看3d视角了

[拖动失败原因](https://blog.csdn.net/cw_huang/article/details/123658315)

![1710074649893](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710074649893.png)

 



## 原理图库

### 元件起名

首先选择添加元器件，然后在弹出的窗口中输入元件的名称

![1710075470839](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710075470839.png)



### 放置引脚

创建好过后我们可以先放置一个矩形

![1710075536416](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710075536416.png)



然后开始放置引脚

![1710075563520](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710075563520.png)

 放置引脚过后给引脚设置其信息

![1710076569393](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710076569393.png)



### 指定封装

设置好引脚以及矩形大小过后，我们就可以设置其指定的PCB封装了，其实封装就是我们刚才绘制的PCB

双击SCH Library中对应要设置的原理元件![1710076659283](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710076659283.png)

然后设置对应的信息属性

![1710076677402](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710076677402.png)

最后添加封装

![1710076710709](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710076710709.png)

然后在弹出的窗口中输入刚才我们设计的PCB元件的名字即可

![1710076807596](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710076807596.png)



## 原理图绘制

### 添加元器件

进入刚才我们设置好的原理图库，选择指定的器件，然后选择放置

![1710077014232](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710077014232.png)



当然我们还有另一种方法来选择我们的原理图元件

在原理图页中的右上脚的Components就可以直接访问原理图库



### 连接元器件

#### 连线

使用快捷键ctrl+w即可放置线，也可以从 放置->线选项来放置线

![1710087335968](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710087335968.png)

#### 网名

我们可以给每条连线定义一个线的标签

![1710117210827](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710117210827.png)



#### 示意标识符

有时我们的线之间有特别的联系，因此我们就可以使用到标识来给连线进行说明

![1710117362402](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710117362402.png)





### 元器件编号

大致的原理画好过后，我们就可以给Designator为例如U?、C?等等，这种标号方式能使用批量编号来给所有的元器件进行编号

![1710117660044](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710117660044.png)

打开原理图标注界面过后就可以进行自动标注编号了

![1710117717023](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710117717023.png)

我们直接选择“更新更改列表”，然后我们就可以看到上面的建议更新列表中的建议值列就有了标号，不再是C?、U?，我们而是U1、C1等等，然后我们就可以选择“接收更改创建eco”

![1710117862925](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710117862925.png)

![1710117883247](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710117883247.png)

来到这一步过后，我们就可以选择执行改变，然后就可以自动进行编号了







### 检查原理图

[如何检查错误](https://blog.csdn.net/m0_63181118/article/details/126317140)

![img](https://img-blog.csdnimg.cn/93c5eff3cc334efbbf3c4a58a705d131.png)

我们在做好连线，标号等工作过后，我们就可以进行检查原理图是否有问题，具体可使用上图中的选项给原理图进行编译

![1710118099929](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710118099929.png)

如果有问题就会出现如上图中的Error报错

如果没有问题就不会出现上面的Messages弹框

如果有错误我们就可以根据上面的弹框中的报错进行更改







## 网表传递

在将原理图转换成PCB前，我们有必要去看一看网络与器件的连接表

![1710118801589](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710118801589.png)

### 器件

#### 编号与封装

![1710119039618](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710119039618.png)

打开过后我们就可以看到有一个列表形式的文本信息，这个就是**元器件的标号（Designator）**、使用的**（parameters）封装**、以及**（comment）属性标注**







### 网络

![1710119378282](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710119378282.png)

当到了网络的时候，我们的网表的格式就变成了括号的形式





#### 包含引脚

具体的含义就是，例如上图中，

VCC_5V的电源线连接上了J_485的第1引脚、

​					 J_USB的第1引脚、

​					 U1的第七引脚、

​					 U2的第8引脚

具体由原理图转换成PCB时，这些引脚就会按照网络表的内容进行连接

具体的实际原理图的连接格式应该是这样的、

![1710120280441](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710120280441.png)

#### 网名

如果我们没有使用网络标签给网络连线进行标识的话，我们的网表就会自动给我们分配网名例如：

下图的原理图

![1710120513498](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710120513498.png)

![1710120481386](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710120481386.png)

由于这根线并没有进行网络标识，因此我们的网表便自动分配了名为NetC5_1的网名



### 模型与属性

#### 器件模型

#### 网路属性

#### 其他信息





## PCB绘制流程

### 导入原理图

首先选择设计中的"Update PCB Document+PCB文件名"

![1710121101449](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710121101449.png)

然后我们会弹出下图的表格。

![1710121258263](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710121258263.png)

表格中的的“打勾的器件”都将会添加到“受影响文档”中，然后我们将所有都选中，然后我们就可以“执行变更”

执行变更完毕后必须要检查“检测”与“完成”项的状态是否是正确的

![1710121386805](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710121386805.png)

如果遇到错误的话，可以查看Message查看错误信息，并根据错误信息进行修改调整 	



如果没有问题，我们选择“关闭”选项，然后我们的PCB图的右下脚就会出现我们的PCB图了

![1710121628411](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710121628411.png)





但是我们的PCB图中有绿色一般都是表示错误，我们将其放大，就能看到具体如下图 

![1710121796456](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710121796456.png)

![1710122013747](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710122013747.png)

具体的错误将会标注出来，比如我们上面的提示的错图就是引脚键的间距小于0.254mm

### 建立规则

pcb的规则的建立是根据PCB电路板的制作的参数来定义的

例如：板厚、走线宽度、钻孔内外径、走线间距、铜厚、丝印字符

具体的规则选项，我们可以选择“设计”->“规则”选项

![1710123736458](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710123736458.png)

然后将PCB电路板的参数设置到规则弹窗中

其中我们这里设置上面提到的参数

具体包括：Electrical（电气属性）->Clearance(线距)

我们将线距的最小线间距设置为0.1mm	![1710124000103](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710124000103.png)

而上面的表中，我们可以根据行标签或列标签进行设置两个部件之间的间距

其中具体包含的部件有：

Track（线）、SMD_Pad(贴片引脚)、TH_Through_Hole（通孔）、Via(过孔)等等

例如上图中的Track（线）到Track是0.1mm

​	

#### 根据加工厂的设计极限



#### 根据个人的绘图习惯

​	

当然我们在设置好一次规则过后，并不是过后的每一次都需要重新进行设置的，我们也可以保存规则

![1710124795240](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710124795240.png)

我们可以选择规则设置面板中的Design Rules中的“Export Rules”，然后将规则配置保存下来，那么下次我们画电路板的时候就能直接直接使用上图中的“Import Rules"选项来加载保存下来的规则配置文件

#### 层叠管理器

而如果我们想要增加层数，我么也可以使用“设计”->“层叠管理器”进行添加或管理层

其中：

Top_Overlay:为顶层丝印层

Top_Solder:顶层阻焊层

Top_Layer:顶层信号层

Dielectric：电介质层

Bottom_Layer:底层信号层

等

如果需要增加层，使用add选项即可

![1710126789120](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710126789120.png)



### 器件布局

器件的布局应该按照信号的流向进行设计

![1710129806686](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710129806686.png)

### 布线

布线是具有一定规则的，一般来说，**布线会先布模拟信号线以及高速信号线**，这是因为模拟信号线会比较容易受到干扰，高速信号线不仅容易受到干扰，还容易干扰到其他的信号线，因此在布线的时候应该首先考虑这两根线，这两根线应该设计得尽可能短

#### 连线

我们选择“放置”->“走线”选项，进行走线，并且在走线的过程中，我们可以使用tab键来进行线的属性设置

![1710130520398](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710130520398.png)

连线应该遵循先快后慢的原则，即先将快速信号线全都布置好，然后再去走慢一点的信号线

#### 覆铜

一般来说我们对电源进行布线时都会选择铺铜的方式，这样每个VCC引脚都能直接的连接到电源的同时，在底层做地层，能使得我们整个PCB的布线变得清晰，且铺铜的电阻很小，能起到很好的供电效果

选择“放置”->“铺铜”选项，选择过后使用Tab键来调出铺铜属性窗口进行设置属性

![1710130753289](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710130753289.png)

例如：给铜皮设置其名字，需要与之连接的网络，铜皮所处位置，死铜（没有连接任何器件的铜）如何处理



### PCB规则检查

使用“工具”->“设计规则检查”（Design Rule Check）

![1710163063005](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710163063005.png)

然后在这个界面中我们选择运行检查![1710163077136](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710163077136.png)



然后可能就有超级多的错误

![1710163184021](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710163184021.png)

这上面的错误其实就是我们规则制定的错误

我们一一来解决它：

1. Silk to Silk（Clearance=0.xxxmm）:

该选项处于“Manufacturing”中的

![1710163267373](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710163267373.png)

![1710163479815](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710163479815.png)

该项的含义为：丝印字符与字符，还有位号与芯片外框之间的距离太近，我们同样将其改小，实际上这同样不影响使用







2. Silk To Silk Mask（Clearance=0.xxxmm）

![1710163378950](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710163378950.png)

其含义为丝印与焊盘之间的距离太近，我们可以将其设置小一点，当然这其实并不影响电路板的正常使用，只不过是丝印会模糊



3. Minimum Solder Mask Sliver(Gap=0.xxxmm)

 ![1710163664487](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710163664487.png)

焊盘与焊盘之间的阻焊绿油的粗细，如果定义过大也会报错







### 裁剪板框

我们首先将移动到Keep-Out Layer层

然后“放置”->“线”，给铜的边缘画上，这时候一定会出现报错

我们进行重新铺铜，报错就会消失

![1710164230404](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710164230404.png)



**注意：**只要对电路板的电气、铜层有任何的修改的话，就必须进行规则检测（Design Rule Check）一次，确保没有任何问题



最后我们对板进行裁剪：



我们使用快捷键“L”调出层可视窗口，然后将所有的层都隐藏，仅仅留下刚才我们画线的Keep-Out Layer层

![屏幕截图 2024-03-11 214104](C:\Users\R\Pictures\Screenshots\屏幕截图 2024-03-11 214104.png)

然后框选所有

![1710164536922](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710164536922.png)

最后选择“设计”->“板子形状”->“按照选择对象定义”来进行更改，就可以更改完毕。

![1710164670945](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1710164670945.png)