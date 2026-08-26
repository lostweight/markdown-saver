[TOC]

#### 数学函数

![1677388648079](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677388648079.png)



——————————————————————————————————

![1677388705517](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677388705517.png)

***



#### 向量的方向

**行向量**：按行方向分布的向量称为行向量：x = [1 2 3 4] （同一行元素以逗号或空格分隔）

**列向量**：按列方向分布的向量称为列向量：c = [1;2;3;4]   (同一列元素以分号分隔)

<u>行向量与列向量之间可通过**转置**进行转换：x = x'</u>

<u>行向量与列向量在操作上和运算上一样，唯一区别在于显示上</u>



![1677372562274](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677372562274.png)



***



#### 向量的运算

![1677372712047](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677372712047.png)



![1677372727975](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677372727975.png)



***



#### 矩阵的创建

##### *普通矩阵的创建：*

![1677373119382](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677373119382.png)



——————————————————————————————————



##### 特殊的矩阵创建

c  = ones(m,n) 产生一个m行n列的元素全为1的矩阵

b = zeros(m,n) 产生一个m行n列的元素全为0的矩阵

a = []                  产生一个空矩阵，空矩阵的大小为0

d = eye(m,n) 	产生一个m行n列，对角线为1，其余为0的矩阵

![1677373593406](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677373593406.png)

*<u>如果eye函数所要生成的矩阵为m=n大小的矩阵，则可以只存在一个值</u>*

即：

eye（m）：产生一个m行m列大小的矩阵，对角线为1，其余为0



————————————————————————————————



##### 矩阵的元素操作



![1677374040049](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677374040049.png)



![1677374071550](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677374071550.png)

<u>*注：*</u>两个维度如果要合并必须要至少行数或者列数中一个相等的才可以合并，如果两个矩阵维度不一致，则无法合并 



***



#### 矩阵的运算

![1677375359986](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677375359986.png)

——————————————————————————————————

###### 矩阵的乘法

<u>两个矩阵相乘时，矩阵维度可以不同，但A的列数必须要等于B的行数才可以相乘</u>

A * B = C (**c的行数**与**A的行数**相同，**c的列数**与**B的列数**相同)

![1677375246823](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677375246823.png)





###### 方阵的行列式





***





#### 关系

![1677375790355](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677375790355.png)

​	

![1677375968819](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677375968819.png)

为非零且为正的数为true，为0则为false，负数既不是true也不是false



***



#### 控制流结构

![1677376686580](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677376686580.png)



————————————————————————————————————



##### 循环结构 - for循环

![1677376735530](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677376735530.png)



—————————————————————————————————————

##### 循环结构 - while循环结构

![1677384412065](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677384412065.png)



—————————————————————————————————————



##### 分支结构 - if/else/end分支

![1677385050416](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677385050416.png)





***



#### 作图

##### 二维作图	

###### plot（）

![1677386801801](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677386801801.png)

​	

向量x与向量y大小必须相同否则会发生错误

而如果想在同一坐标系中绘制多条线，那么x必须使用



————————————————————————————————————



###### ezplot（）

![1677389395450](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677389395450.png)

 

—————————————————————————————————————

​	

###### fplot()

![1677389624744](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677389624744.png)

@（x）表示声明一个自变量x



—————————————————————————————————————



##### 三维作图

###### 一条曲线（plot3）

三维空间的画图函数（有别于plot）

![1677390910622](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677390910622.png)

其中x,y,z必须时维度相同的向量



——————————————————————————————————



###### 多条曲线

![1677391539778](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677391539778.png)



————————————————————————————————————



###### 空间曲面

*surf（）*

![1677391723636](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677391723636.png)



*mesh（）*

对网格曲面填充

![1677391851823](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677391851823.png)



*isosurface（）*影视曲面函数

meshgrid用于根据x，y来生成矩阵

![1677391940648](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677391940648.png)

函数调用含义：

x，y，z所张成的长方体的网格内要满足p = v所有的点的集合



***



##### 特殊图形

###### 极坐标图

![1677392426358](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677392426358.png)



例：

![1677392471091](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677392471091.png)

 

——————————————————————————————————



###### 散点图

![1677392546469](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677392546469.png)

​	



###### 等值线图

![1677392736199](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677392736199.png)	

单位阵  eye(3)





***





### Matlib数据导入与导出

##### 1.简单文本文件读取（只包含数值，且以逗号或者空格进行分隔）

![1677907658082](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677907658082.png)



——————————————————————————————————————————————



##### 2.按指定分隔符读取数据文件

![1677908697287](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677908697287.png)





——————————————————————————————————————————



##### 3.按指定格式读取数据文件

格式：M = fscanf（fileID,formatSpec,sizeM）;

fileID: 指文件名称句柄，需要使用fopen命令获取

formatSpec：指读取数据的分隔格式

sizeM：指读取的数据赋给M时的大小为多少行多少列

![1677909182154](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677909182154.png)

例：

![1677911644283](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677911644283.png)

（**注意，这里读取的顺序是按行读取，存储的时候是按列存储**）

按行读取，所以格式为一行的格式

###### format的格式列表

![1677912439186](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677912439186.png)





***



#### 数据拟合

形象的说，拟合就是把平面上一系列的点，用一条光滑的曲线连接起来。因为这条曲线有无数种可能，从而有各种拟合方法。拟合的曲线一般可以用函数表示，根据这个函数的不同有不同的拟合名字。





***





## 数列的极限

### 极限xx

定义：

对于**数列{xn}**， 如果当n无限增大时，其**<u>通项Xn将无限接近</u>一个确定的<u>常数A</u>**，则称**A是数列{Xn}的极限**或者称数列收敛于A

记作：

![1678373821611](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1678373821611.png)

![1678373952828](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1678373952828.png)



### 函数的极限

由于对不同的n，数列中有不同的Un与之对应，这就决定了一个标量函数 Un = f（n），定义域为0至正无穷

也可以说，**函数是定义在在正整数集中的特殊函数**

![1678494488804](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1678494488804.png)



因此数列的极限理论对函数来说同样适用

![1678494846559](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1678494846559.png)





函数的极限：指x趋近于正无穷的时候，f(x)趋近于a这个值，并且任给一个任意数那么，以这个任意数为半径的邻域中，总能找到一个X，并且X之后的x都完全在邻域之中。

![1678603199075](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1678603199075.png)





当函数的左半领域趋向于0的时候函数无限趋近于-1，那么就称函数的左极限为-1

当函数的右半领域趋向于0的时候函数无限趋近于1，那么就称函数的右极限为1



![1678495148907](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1678495148907.png)

#### 函数极限的充要条件

![1678503531073](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1678503531073.png)



f（x）趋向于指定值的极限值：

f(x)在x0的**去心**邻域内有定义（在x0处可以没有定义），如果存在常数A



#### 极限的四则运算法则

![1678503808067](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1678503808067.png)

​	

#### 重要的极限 

n为一个数组，他的**f（n）的值**（即Y的值）**随着n的值越来越大**，**向一条直线无限的接近**，那么就说**f（n）为这个数列的<u>极限</u>**

![1678579683224](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1678579683224.png)





![1678580293197](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1678580293197.png)

​	

————————————————————————————————



#### 增量

![1678582714340](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1678582714340.png)

![1678582766266](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1678582766266.png)

![1678610698156](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1678610698156.png)

![1678610856737](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1678610856737.png)





——————————————————————————————————



#### 无穷大与无穷小

![1678842578041](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1678842578041.png)







——————————————————————————————————



#### 连续

![1678583033505](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1678583033505.png)

 

![1678583559034](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1678583559034.png)	



——————————————————————————————————



### 导数

导数指的是一个函数他在趋于一个x0时，f（x）到f（x0）的增量比上x到x0的增量等于一个常数那么这个常数就是这个函数的导数

当这个常数为零时（即增量y与增量x，当增量x趋近于0时，这两个增量的比值存在），这个导数点被称为驻点

**导数的几何意义**：

指函数在某一点处变化的快慢，是一种变化率

![1678584590798](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1678584590798.png)	



#### 导数的运算	

![1678607440770](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1678607440770.png)

![1678607609785](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1678607609785.png)

![1678894629249](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1678894629249.png)





#### 函数的凹凸性（一阶导数的变化率（二阶导数））

当函数的二阶导数大于0时，为凹曲线

当函数的二阶导数小于0时，为凸曲线

![1678895403062](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1678895403062.png)

![1678895517723](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1678895517723.png)



**如果二阶导数大于0则为凹函数，如果二阶导数小于0则为凸函数**

![1679273762422](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679273762422.png)

**函数的单调性例题**

![1679199557760](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679199557760.png)

![1679200249970](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679200249970.png)

![1679273172960](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679273172960.png)



————————————————————————————————————



#### 函数的极值

![1678895557345](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1678895557345.png)

![1678895794190](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1678895794190.png)



————————————————————————————————————————



#### 微分中值定理	

##### 拉格朗日定理、罗尔定理

![1679187792438](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679187792438.png)





——————————————————————————————————



### 微分的定义

**微分的几何意义**：

是指函数在某一点处（趋近于无穷小）的变化量，是一种变化的量

![1679021741823](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679021741823.png)



——————————————————————

### 微分的近似公式

#### 微分的四则运算

![1679070822053](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679070822053.png)



![1679186872012](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679186872012.png)

![1679021893566](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679021893566.png)

![1679021952313](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679021952313.png)

例： 

![1679144696644](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679144696644.png)

![1679185541952](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679185541952.png)



——————————————————————



#### 洛必达法则 	

![1679191387331](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679191387331.png)



例：

**0比0型**

![1679192061727](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679192061727.png)

![1679192507588](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679192507588.png)

![1679192740335](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679192740335.png)

**无穷比无穷型**

![1679193183009](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679193183009.png)

![1679194051001](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679194051001.png)



- **洛必达法则只有当为0比0型、无穷比无穷型时才进行使用**
- **不要一味地去求导，要与<u>重要极限</u>，以及<u>等价无穷小替换</u>结合使用**

![1679194769023](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679194769023.png)



##### 等价无穷小

![1679195044805](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679195044805.png)

等价无穷小只有乘除的时候可以替换x，加减的时候x无法进行替换

![1679195573910](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679195573910.png)

如果洛必达法则计算出来的结果为没有极限，则需要使用其他方法进行求极限 	

![1679198282122](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679198282122.png)

1. 如果将趋向数带入式子中得到的**0比0型**或**无穷比无穷型，**那么首先就可以考虑洛必达法则
2. 如果将趋向数代入到式子中的到的是其他型的，比如：<u>0*无穷，0^0，1^无穷，无穷^0</u>等形式的话，需要先将式子转化成**0比0型**或者**无穷比无穷型，**例如：0*无穷 =  无穷/0分之1 或者 0/无穷分之1 ，然后再进行使用洛必达法则
3. 如果再使用了一次洛必达法则进行求导后再将趋向数带入到式子中去时，如果式子还是0比0型、无穷比无穷型时，就再对式子进行一次求导并对式子进行化简，同时尽量使用两个重要极限以及等价无穷小进行对式子的替换



————————————————————————————————————

 

#### 牛顿迭代法解方程

牛顿迭代法使用的是微分的近似公式3

![1679022474558](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679022474558.png)

牛顿迭代法：将不是线性的转为线性的来进行求根

![1679067700514](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679067700514.png)





——————————————————————————————



## 微积分

求导与求积分为两个不相同的概念

**求导**：已知一个函数，求其导函数，

（注：导数是指函数在某一点处的变化的快慢，是一种变化率）

**求积分**：已知一个导数，求原本的函数

![1679310890436](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679310890436.png)

#### 1.不定积分

不定积分就是指这个导数的全体原函数

![1679312765808](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679312765808.png)

![1679412931886](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679412931886.png)

![1679412993987](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679412993987.png)

![1679413046313](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679413046313.png) 



**基本求积分方法**

![1679413239131](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679413239131.png)

![1679413453568](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679413453568.png)





例题：

![1679311495323](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679311495323.png)

![1679313200320](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679313200320.png)

![1679314050344](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679314050344.png)



**基本积分公式**

![1679315173338](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679315173338.png)





**例题2：**

二倍角公式： 	![1679317658991](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679317658991.png)





##### 第一换元微分法（凑） 

将dx前面相乘的某一项凑到d的里面去（求原函数），即d里面的是这一项的原函数，**朝里拿求原函数**

![1679316930379](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679316930379.png)

![1679317956827](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679317956827.png)



**积分法**

![1679326291139](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679326291139.png)

![1679398452674](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679398452674.png)

![1679400054260](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679400054260.png)

![1679400867624](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679400867624.png)

**<u>积化和差公式</u>**

![img](https://bkimg.cdn.bcebos.com/formula/f5356cb9abb471a3189311c7b42d24c3.svg)

![img](https://bkimg.cdn.bcebos.com/formula/07792690a852ebba3ef29681e3ffb867.svg)

![img](https://bkimg.cdn.bcebos.com/formula/539fcb085f84c6bb61d3c3b318053ab2.svg)

![img](https://bkimg.cdn.bcebos.com/formula/92e1a87e1e8ca4649a1a6605b2badb9b.svg)

![1679404546756](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679404546756.png)





##### 第二换元公式（把内的项往外拿，并且对这个项求导）



例题：

![1679742126153](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679742126153.png)

![1679839764423](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679839764423.png)





##### 分布积分法

![1679924800721](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679924800721.png)

![1679928472929](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679928472929.png)

![1679928575757](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679928575757.png)

![1679930014619](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679930014619.png)

![1679930709506](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1679930709506.png)