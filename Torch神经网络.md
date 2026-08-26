# Torch神经网络



## 一.基本概念

**基本模型**：

![1677324513193](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677324513193.png)







首先，我们导入`torch`。请注意，虽然它被称为PyTorch，但是代码中使用`torch`而不是`pytorch`。

```
import torch
```

![Copy to clipboard](https://raw.githubusercontent.com/choldgraf/sphinx-copybutton/master/sphinx_copybutton/_static/copy-button.svg)

**张量**表示一个由**数值组成的数组**，这个数组可能有多个维度。 **具有一个轴的张量**对应数学上的***向量***（vector）； **具有两个轴的张量**对应数学上的***矩阵***（matrix）； 具有两个轴以上的张量没有特殊的数学名称。



————————————————————————————————————————————

#### 样本

数据集中的一个样本对应的就是一个实体的特征与标签的集合

#### 特征值

即样本中实体的特征量



例如：一堆水果中，有苹果，香蕉，橙子

​		其中**这堆水果**就是**数据集**

​		其中**水果的味道，形状**就是数据的**特征**

​		**水果的名称**就是最终的**标签**



———————————————————————————————————————————



#### 张量、数组与列表的区别

##### 1.list和ndarray

==最大的区别在于在内存中存储方式不同==

**相同：**

- 列表（list）与数组（ndarray）类似，是具有相同类型的多元素构成的整体
- list和array都可以根据索引、切片来取其中的元素

**区别：**

- **数组在内存中是连续的**，数组里的元素都是同一类，所以一旦确定了一个数组，它的内存就确定了，因此不能向列表一样通过.append()追加。**列表中保存的是数据存放的地址**，简单地说就是指针并非数据，所以可以存储不同的类型，由于地址不用连续，所以可通过.append()把元素的地址追加进去，由于每个元素都需要一个地址，因此增加了堆内存和cpu的开支
- 列表不能对整体进行数值运算，因为列表是由多个元素组成的有序组合，每个元素都是独立的，具有自己的数值。但是数组能对整体进行数值运算
- 数组底层使用c语言编写，运算速度快，并且具有强大的运算能力



##### 2.ndarray和tensor

==最大区别在于值是否可以改变（数据运行的设备）==

**相同：**

- tensor内部的数据类型为ndarray类型
    **区别：**

- tensor可以有加速器内存（如GPU）支持，既可以在CPU上运行也可以在GPU上运行。ndarray只能在CPU上运行。
- ndarray在CPU上运行，因此可以改变其数值。tensor的值可以驻留在GPU上加速，GPU不具有改变元素值的能力，因此tensor的值不可以改变。
  



———————————————————————————————————————————



### arange创建张量

```python
x = torch.arange(12)
x

>>>
tensor([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11])
```

使用arange创建一个**行向量x**，**默认创建为整数**，也可以指定类型为浮点数，张量中的值都称为张量中的**元素**。



———————————————————————————————————————————

### shape属性访问张量的形状

```python
x.shape

>>>
torch.Size([12])
```



——————————————————————————————————————————

### numel（）获取张量的元素总数

```python
import torch
a = torch.arange(12)
a = a.reshape(3,4)
print(a.shape)
print(a.numel())

>>>
torch.Size([3, 4])
12
```



——————————————————————————————————————————

### reshape函数，改变张量形状

**改变**张量的**形状**，张量的**元素以及大小不变**

```python
import torch
a = torch.arange(12)
a = a.reshape(3,4)
print(a.shape)


>>>
torch.Size([3, 4])
```

不一定要手动指定每个维度来改变形状

如果我们的目标形状为（高度，宽度），那么在知道宽度后，高度自然会被计算出来。

```python
import torch
a = torch.arange(12)
a = a.reshape(3,-1)
print(a.shape)
print(a.numel())

>>>
torch.Size([3, 4])
12
```



——————————————————————————————————————————

### torch.zero()函数创建全零张量

例：创建形状（size）为（2，3，4）的张量

```python
import torch
a = torch.zeros((2,3,4))
print(a)

>>>
tensor([[[0., 0., 0., 0.],
         [0., 0., 0., 0.],
         [0., 0., 0., 0.]],

        [[0., 0., 0., 0.],
         [0., 0., 0., 0.],
         [0., 0., 0., 0.]]])

```



——————————————————————————————————————————

### torch.ones()函数创建全一张量

```python
import torch
a = torch.ones((3,3,4))
print(a)

>>>
tensor([[[1., 1., 1., 1.],
         [1., 1., 1., 1.],
         [1., 1., 1., 1.]],

        [[1., 1., 1., 1.],
         [1., 1., 1., 1.],
         [1., 1., 1., 1.]],

        [[1., 1., 1., 1.],
         [1., 1., 1., 1.],
         [1., 1., 1., 1.]]])

```



——————————————————————————————————————————

### torch.randn(size)函数创建随机张量

我们可以通过这个函数来创建一个张量，其中的每个元素都从均值为0、标准 差为1的**标准高斯分布（正太分布）**中**随机采样**

```python
import torch
a = torch.randn(3,4)
print(a)

>>>
tensor([[ 1.7085, -0.8961,  1.7966, -0.4379],
        [-0.2799, -0.2751,  0.9366, -0.8937],
        [-1.6790, -0.5384, -1.5153, -0.0057]])
```



——————————————————————————————————————————

#### torch.cuda.get_device_properties(num)

该函数用于获取可用GPU的具体信息，num是指定查看第num个设备



——————————————————————————————————————————

### 爱因斯坦求和约定

**爱因斯坦求和约定**是一种标记的约定，又称为爱因斯坦**标记法**，这种略去求和号的办法，使得许多坐标公式的书写变得异常简洁，直接来说，**爱因斯坦求和约定就是省去求和公式中的求和符号**

其基本约定是，当两个变量具有相同的角标，且一上一下时，则遍历求和。此时这样的指标也称为“哑指标”。在这种情况下，求和号可以省略

我们先看一个例子

```
a = torch.rand(2,3)
b = torch.rand(3,4)
c = torch.einsum("ik,kj->ij", [a, b])
# 等价操作 torch.mm(a, b)
```

其中需要关注einsum的第一个参数 “ ik,kj->ij ”，该字符串（下文以equation表示）表示了输入和输出张量的维度。**equation中的箭头左边表示`输入张量`**，以逗号分割每个输入张量，箭头右边则表示输出张量，表示维度的字符只能是26个英文字母

而einsum的第二个参数表示实际的输入张量列表，其数量要与equation中的输入数量对应，同时对应每个张量的子equation的字符个数要与张量的真实维度对应，比如"ik,kj->ij" 表示输入和输出张量都是两维的。



equation 中的字符也可以理解为索引，就是输出张量的某个位置的值，是怎么从输入张量中得到的，比如上面矩阵乘法的**输出 c 的某个点 c[i, j] 的值是通过 a[i, k] 和 b[k, j] 沿着 k 这个维度做内积**得到的。



接着介绍两个基本概念，自由索引（***Free indices***）和求和索引（***Summation indices***）：

- 自由索引，出现在箭头右边的索引，比如上面的例子就是 i 和 j；
- 求和索引，只出现在箭头左边的索引，表示中间计算结果需要这个维度上求和之后才能得到输出，比如上面的例子就是 k；

接着是介绍三条基本规则：

- 规则一，equation 箭头左边，在不同输入之间重复出现的索引表示，把输入张量沿着该维度做乘法操作，比如还是以上面矩阵乘法为例， "ik,kj->ij"，k 在输入中重复出现，所以就是把 a 和 b 沿着 k 这个维度作相乘操作；
- 规则二，只出现在 equation 箭头左边的索引，表示中间计算结果需要在这个维度上求和，也就是上面提到的求和索引；
- 规则三，equation 箭头右边的索引顺序可以是任意的，比如上面的 "ik,kj->ij" 如果写成 "ik,kj->ji"，那么就是返回输出结果的转置，用户只需要定义好索引的顺序，转置操作会在 einsum 内部完成。

### **特殊规则**

特殊规则有两条：

- equation 可以不写包括箭头在内的右边部分，那么在这种情况下，输出张量的维度会根据默认规则推导。就是把输入中只出现一次的索引取出来，然后按字母表顺序排列，比如上面的矩阵乘法 "ik,kj->ij" 也可以简化为 "ik,kj"，根据默认规则，输出就是 "ij" 与原来一样；
- equation 中支持 "..." 省略号，用于表示用户并不关心的索引，比如只对一个高维张量的最后两维做转置可以这么写：

```python
a = torch.randn(2,3,5,7,9)
# i = 7, j = 9
b = torch.einsum('...ij->...ji', [a])
```



————————————————————————————————————

#### torch.einsum函数

在实现一些算法时，数学表达式已经求出来了，需要将之转换为代码实现，简单的一些还好，有时碰到例如矩阵转置、矩阵乘法、求迹、张量乘法、数组求和等等，若是以分别以transopse、sum、trace、tensordot等函数实现的话，不但复杂，还容易出错

现在，这些问题你统统可以一个函数搞定，没错，就是einsum，einsum函数就是根据上面的标记法实现的一种函数，可以根据给定的表达式进行运算，可以替代但不限于以下函数：

矩阵求迹：trace
求矩阵对角线：diag
张量（沿轴）求和：sum
张量转置：transopose
矩阵乘法：dot
张量乘法：tensordot
向量内积：inner
外积：outer

torch.einsum函数语法：

```
einsum(equation, *operands)
```

**equation：**是字符串表达式，operands是操作数

equation是字符串的表达式，operands是操作数，是一个元组参数，并不是只能有两个，所以只要是能够通过einsum标记法表示的**乘法**求和公式，都可以用一个einsum解决，下面以numpy举几个栗子：

```python3
# 沿轴计算张量元素之和：
c = a.sum(axis=0)
```

上面的以sum函数的实现代码，设 � 为三维张量，上面代码用公式来表达的话就是：

![1687938733703](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1687938733703.png)

换成einsum标记法：

![1687938744015](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1687938744015.png)

然后根据此式使用einsum函数实现等价功能：

```python3
c = np.einsum('ijk->jk', a)   
# 作用与 c = a.sum(axis=0) 一样
```

更进一步的，如果 **a** 不止是三维，可以将下标 **jk**换成省略号，以表示剩下的所有维度：

```python3
c = np.einsum('i...->...', a)
```

这种写法pytorch与tensorflow同样支持，如果不是很理解的话，可以查看其对应的公式：

![1687938775146](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1687938775146.png)

```python3
# 矩阵乘法
c = np.dot(a, b)
```

矩阵乘法的公式为：

![1687938789195](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1687938789195.png)

然后是einsum对应的实现：

```python3
c = np.einsum('ij,jk->ik', a, b)
```



最后再举一个张量乘法栗子：

```python3
# 张量乘法
c = np.tensordot(a, b, ([0, 1], [0, 1]))
```

如果 **a，b**是三维的，对应的公式为：

![1687938818711](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1687938818711.png)

对应的einsum实现：

```python3
c = np.einsum('ijk,ijl->kl', a, b)
```



——————————————————————————————————



#### 工厂函数

 python中一切皆为对象，如果当我们们在调用对象的时候在后面加上了()号的话，也就是说我们实例化或者说调用了这个函数或者是对象，如果我们的后面没有加上()号的话，那么我就将继承这个函数或对象，那么这时这个变量就相当于前面函数这个对象 ，当对这个变量使用()来调用的时候，就会自动使用前一个对象函数来生成或者处理结果

例：

首先这里定义了四个函数用于计算

![1687940180569](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1687940180569.png)

然后我们使用一个字典来封装这些函数对象

![1687940216211](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1687940216211.png)

最后使用一个工厂函数，根据不同的how参数来使用对应的函数对象

![1687940232030](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1687940232030.png)







##### 闭包

我们先看例子

**本地作用域在函数结束后就立即失效，而嵌套作用域在嵌套的函数返回后却仍然有效。**

```
def f1():
	x = 88
	def f2():
		print(x)
	return f2
action = f1()
action()

>>> 
88
```

这个例子非常重要，也很有意思，函数f1中定义了函数f2，f2引用了f1嵌套作用域内的变量x，并且f1将函数f2作为返回对象进行返回。最值得注意的是我们通过获取了返回的f2，虽然此时f1函数已经退出结束了，但是f2仍然记住了f1嵌套作用域内的变量名x。

上面这种语言现象称之为闭包：一个能记住嵌套作用域变量值的函数，尽管作用域已经不存在。

这里有一个应用就是工厂函数，工厂函数定义了一个外部的函数，这个函数简单的生成并返回一个内嵌的函数，仅仅是返回却不调用，因此通过调用这个工厂函数，可以得到的一个内嵌函数的引用，内嵌函数就是通过调用工厂函数时，运行内部的def语句而创建的。



————————————————————————————————————————



##### torch.Tensor.to方法

to方法用于执行张量数据类型或设备转换，返回具有指定设备或数据类型的张量

```python
tensor = torch.randn(2, 2)  # Initially dtype=float32, device=cpu
tensor.to(torch.float64)
>>>
tensor([[-0.5044,  0.0005],
        [ 0.3310, -0.0584]], dtype=torch.float64)

——————————————————————————————————————————————————

cuda0 = torch.device('cuda:0')
tensor.to(cuda0)
>>>
tensor([[-0.5044,  0.0005],
        [ 0.3310, -0.0584]], device='cuda:0')

——————————————————————————————————————————————————

tensor.to(cuda0, dtype=torch.float64)
>>>
tensor([[-0.5044,  0.0005],
        [ 0.3310, -0.0584]], dtype=torch.float64, device='cuda:0')

——————————————————————————————————————————————————

other = torch.randn((), dtype=torch.float64, device=cuda0)
tensor.to(other, non_blocking=True)
>>>
tensor([[-0.5044,  0.0005],
        [ 0.3310, -0.0584]], dtype=torch.float64, device='cuda:0')
```



————————————————————————————————————————



##### torch.transpose(input, dim0, dim1) → Tensor

返回一个张量，该张量是输入张量的转置版本，当输入了dim0和dim1的时候将会对张量的指定维度进行转置，

参数：

input：（张量）输入张量

dim0：（int）要转置的第一个维度

dim1：（int）要转置的第二个维度



————————————

###### 稠密矩阵

稠密矩阵与稀疏矩阵相反，若非0元素数占绝大多数的时候， 则称该矩阵的稠密矩阵



————————————

###### 稀疏矩阵

在矩阵中，若数值为0的元素数目远远多于非0元素的数目时，则称该矩阵为稀疏矩阵



稀疏矩阵的特性：

- 稀疏矩阵其非零元素的个数远远少于零元素的个数，而且这些0元素的分布也没有规律
- **稀疏因子是用于描述稀疏矩阵的非零元素的比例情况**。设一个n\*m的稀疏矩阵A中有**t个非零元素**，则稀疏因子δ的计算公式如下：δ=t / (m*n) (当这个值小于等于0.05时，可以认为是稀疏矩阵)



————————————————————————————————————————



##### 张量的存储区创建

在创建存储区之前，我们可以先认识几个特殊的定义

- **大小：**大小指的是张量的形状大小，一般用元组进行表示，一般格式为（行数， 列数）
- **偏移量：**偏移量指的是张量的第一个元素相对于存储区中对应的元素的索引位置
- **步长：**步长是指当索引在原张量的每个维度中增加1时在存储区中必须跳过的元素数量

![img](https://img-blog.csdnimg.cn/bb03f58efcff4221af194134965bd073.jpeg)









## 2.1运算符

按元素运算：将标准量运算符应用到张量中的每个元素中，对于将两个数组作为输入的函数，按元素运算将二元运算符应用于两个数组中的每对位置对应的元素，



在数学表示法中，我们将通过符号
$$
f：R  →R
$$
 来表示*一元*标量运算符（只接收一个输入）。 



这意味着该函数从任何实数（
$$
R
$$
）映射到另一个实数。



 同样，我们通过符号 
$$
f:R,R→R
$$
表示*二元*标量运算符，这意味着该函数接收两个输入，并产生一个输出。 



给定同一形状的任意两个向量**<u>u</u>**和<u>**v**</u>和二元运算符**f**， 我们可以得到向量。
$$
c = F(u,v)
$$


对于任意具有相同形状的张量， 常见的标准算术运算符（`+`、`-`、`*`、`/`和`**`）都可以被升级为按元素运算。 我们可以在同一形状的任意两个张量上调用按元素操作。



```python
x = torch.tensor([1.0, 2, 4, 8])
y = torch.tensor([2, 2, 2, 2])
x + y
x - y
x * y
x / y
x ** y  # **运算符是求幂运算

>>>
(tensor([ 3.,  4.,  6., 10.]),
 tensor([-1.,  0.,  2.,  6.]),
 tensor([ 2.,  4.,  8., 16.]),
 tensor([0.5000, 1.0000, 2.0000, 4.0000]),
 tensor([ 1.,  4., 16., 64.]))
```



—————————————————————————————————————————

### torch.exp(张量)输出以e为底做指数运算

```python
import torch
a = torch.Tensor([1,2,3,4,5])
print(a)
b = torch.exp(a)
print(b)

>>>
tensor([1., 2., 3., 4., 5.])
tensor([  2.7183,   7.3891,  20.0855,  54.5981, 148.4132])
```



————————————————————————————————————————————

### 广播机制

通常情况下，两个张量应该如同矩阵一样形状应该相同才能进行元素操作，但在某些特定情况下，即使形状不同，我们依旧可以通过调用*广播机制*来执行按元素操作

具体的工作方式如下：

1.通过适当复制元素来扩张一个或两个数组，以便在转换之后，两个张量具有相同的形状

2.对生成的数组执行按元素操作

多数情况下，我们将沿着数组中长度为1的轴进行广播，具体如下：

```python
import torch
a = torch.Tensor([1,2,3]).reshape((3,1))  # 两种reshape传入的方式得到的结果是等价的
b = torch.Tensor([4,5,6]).reshape(1,3)
print(a)
print(b)
print(a + b)

>>>
tensor([[1.],
        [2.],
        [3.]])
tensor([[4., 5., 6.]])
tensor([[5., 6., 7.],
        [6., 7., 8.],
        [7., 8., 9.]])
```

由于这两个矩阵形状不匹配，所以我们将两个矩阵广播为一个更大的3 x 2 的矩阵，

如上所示：矩阵A将**复制列**，矩阵B则**复制行**，然后按元素相加



————————————————————————————————————————————

### 索引与切片

与python中的数组一样， 张量中的元素可以通过索引访问

```python
import torch
a = torch.arange(12).reshape(3,4)
print(a)
print(a[-1])    # 索引最后一行
print(a[:,-1])  # 索引最后一列，这里的索引顺序为：[行索引，列索引]
a[1,1] = 33     # 修改矩阵中第二行第二列的元素的值
print(a)

>>>
tensor([[ 0,  1,  2,  3],
        [ 4,  5,  6,  7],
        [ 8,  9, 10, 11]])
tensor([ 8,  9, 10, 11])
tensor([ 3,  7, 11])
tensor([[ 0,  1,  2,  3],
        [ 4, 33,  6,  7],
        [ 8,  9, 10, 11]])
```



——————————————————————————————————————————————

### 内存问题

有时我们运行的一些操作可能会导致为新结果分配内存

如下例子

```python
import torch
a = torch.arange(4).reshape(2,2)
before = id(a)           # 通过python的id函数，我们可以看到当前的变量的内存id地址
a = a + 1
print(id(a) == before)

>>>
False
```

这种浪费内存的方式是不可取的，原因有两个：

1.首先，我们不想总是不必要地分配内存，在机器学习中，我们可能有数百兆的参数，并且在一秒内多次更新所以参数，通常情况下，我们希望原地执行这些更新

2.如果我们不原地更新，其他引用仍然会指向旧的内存位置，这样我们的某些代码可能会无意中引用旧的参数。



其实执行**原地操作**非常简单，我们可以使用**切片表示法**将操作的结果分配给先前分配的数组

```python
import torch
a = torch.arange(12).reshape(3,4)
b = a + 3
z = torch.zeros_like(b)
print("id(z): ",id(z))
z[:] = a + b            # 通过索引的方式实现原地操作
print("id(z): ",id(z))
z += b                  # 通过+=实现原地操作
print("id(z): ",id(z))

>>>
id(z):  2204998948800
id(z):  2204998948800
id(z):  2204998948800
```



——————————————————————————————————————————————

### 转换为其他python对象

```python
A = X.numpy()
B = torch.tensor(A)
type(A), type(B)

>>>
(tensor([3.5000]), 3.5, 3.5, 3)
```







## 2.2数据预处理

在python中常用的数据分析工具中，通常使用pandas软件包，pandas可以与张量兼容



——————————————————

### os.path.join()函数

用于路径拼接文件路径，可以传入多个路径

如果不存在以“/”开始的参数，则函数将会自动加上



——————————————————

### os.makedirs()函数

os.makedirs()方法用于递归创建目录（单层可使用os.mkdir）

参数说明
name：你想创建的目录名
mode：要为目录设置的权限数字模式，默认的模式为 0o777 (八进制)。
exist_ok：是否在目录存在时触发异常。如果exist_ok为False（默认值），则在目标目录已存在的情况下触发				FileExistsError异常；如果exist_ok为True，则在目标目录已存在的情况下不会触发FileExistsError异     				常



——————————————————————————————————————————————

### 读取数据集

```python
import os
os.makedirs(os.path.join('..', 'data'), exist_ok=True)
data_file = os.path.join('..', 'data', 'house_tiny.csv')
with open(data_file, 'w') as f:
    f.write('NumRooms,Alley,Price\n')  # 列名
    f.write('NA,Pave,127500\n')  # 每行表示一个数据样本
    f.write('2,NA,106000\n')
    f.write('4,NA,178100\n')
    f.write('NA,NA,140000\n')
```

要从创建的csv文件中加载原始数据集，我们导入pandas包并调用read_csv函数，该数据集有四行三列，其中每行描述了房间数量、巷子类型和房屋价格

```python
import pandas as pd

data = pd.read_csv(data_file)
print(data)

>>>
 NumRooms Alley   Price
0       NaN  Pave  127500
1       2.0   NaN  106000
2       4.0   NaN  178100
3       NaN   NaN  140000
```



——————————————————————————————————————————————

### 处理缺失值

“NaN”项代表缺失值，为了处理缺失的数据，典型的方法包括<u>*插值法*</u>和<u>*删除法*</u>

其中插值法用一个替代值弥补缺失值，而删除法则直接忽略缺失值



这里我们将通过插值法进行弥补缺失值

```python
import pandas as pd
import os
# 先将文件路径组合起来，然后使用os.makedirs函数进行递归创建文件夹，如果文件夹已经创建，则忽略报错
os.makedirs(os.path.join('.','数据文件库'), exist_ok = True)
data_file = os.path.join('.','数据文件库','house_price.csv')
with open(data_file,'w') as f:
    f.write('NumRooms,Alley,Price,country\n')  # 列名
    f.write('NA,Pave,127500,Germany\n')  # 每行表示一个数据样本
    f.write('2,NA,106000,NaN\n')
    f.write('4,NA,178100,China\n')
data = pd.read_csv(data_file)
print(data)
print(pd.get_dummies(data,dummy_na = True))
data = data.fillna(5)
print(data)

>>>
   NumRooms Alley   Price  country
0       NaN  Pave  127500  Germany
1       2.0   NaN  106000      NaN
2       4.0   NaN  178100    China

   NumRooms Alley   Price  country
0      99.0  Pave  127500  Germany
1       2.0    99  106000       99
2       4.0    99  178100    China

```

————————————————

### pd.get_dummies()函数

在数据预处理过程中，我们需要将一个特征变量变为计算机能读懂的特征距离,其中用到的为one-hot-encoding

 one-hot的基本思想：将离散型特征的每一种取值都看成一种状态，若你的这一特征中有N个不相同的取值，那么我们就可以将该特征抽象成N种不同的状态，one-hot编码保证了每一个取值只会使得一种状态处于“激活态”，也就是说这N种状态中只有一个状态位值为1，其他状态位都是0。举个例子，假设我们以学历为例，我们想要研究的类别为小学、中学、大学、硕士、博士五种类别，我们使用one-hot对其编码就会得到：



![img](https:////upload-images.jianshu.io/upload_images/9742431-171284de9c1518af.png?imageMogr2/auto-orient/strip|imageView2/2/w/538/format/webp)

函数参数：

```python
pandas.get_dummies(data,
                   prefix=None,
                   prefix_sep='_',
                   dummy_na=False,
                   columns=None,
                   sparse=False,
                   drop_first=False)
		Convert categorical variable intodummy/indicator variables
```

data：array-like，Series或DataFrame，传入的是要处理的矩阵或者是Tensor

prefix：string，字符串列表或字符串dict，默认为None，自定义前缀，当为None时，使用的是原列名

prefix_sep：string，默认为"\__"(下划线)，改变编码后的索引列的名称中的符号，如果要附加前缀，分隔符可以传					递与前缀一样的列表或字典

dummy_na：是否为缺失值（NaN）创建一个哑变量列，默认为False

columns：要进行哑变量转换的列名列表或名称或整数或布尔型的索引器（表示需要将哪些列进行编码）



**dummy_na参数示例：**

```
# 若dummy_na = True时
import pandas as pd
import os
# 先将文件路径组合起来，然后使用os.makedirs函数进行递归创建文件夹，如果文件夹已经创建，则忽略报错
os.makedirs(os.path.join('.','数据文件库'), exist_ok = True)
data_file = os.path.join('.','数据文件库','house_price.csv')
with open(data_file,'w') as f:
    f.write('NumRooms,Alley,Price,country\n')  # 列名
    f.write('NA,Pave,127500,Germany\n')  # 每行表示一个数据样本
    f.write('2,NA,106000,NaN\n')
    f.write('4,NA,178100,China\n')

data = pd.read_csv(data_file)
print(data)
print(pd.get_dummies(data,dummy_na = True))

>>> # 将会为值为NaN创建新的列，用于表示NaN，若dummy_na = False,则将不会有NaN这一列 
   NumRooms Alley   Price  country
0       NaN  Pave  127500  Germany
1       2.0   NaN  106000      NaN
2       4.0   NaN  178100    China
   NumRooms   Price  Alley_Pave  ...  country_China  country_Germany  country_nan
0       NaN  127500        True  ...          False             True        False
1       2.0  106000       False  ...          False            False         True
2       4.0  178100       False  ...           True            False        False
```



**普通示例：**

```python
import pandas as pd
import os
# 先将文件路径组合起来，然后使用os.makedirs函数进行递归创建文件夹，如果文件夹已经创建，则忽略报错
os.makedirs(os.path.join('.','数据文件库'), exist_ok = True)
data_file = os.path.join('.','数据文件库','house_price.csv')
with open(data_file,'w') as f:
    f.write('NumRooms,Alley,Price,country\n')  # 列名
    f.write('NA,Pave,127500,Germany\n')  # 每行表示一个数据样本
    f.write('2,NA,106000,Singapore\n')
    f.write('4,NA,178100,China\n')
    

data = pd.read_csv(data_file)
print(data)
print(pd.get_dummies(data))

>>>
   NumRooms Alley   Price    country
0       NaN  Pave  127500    Germany
1       2.0   NaN  106000  Singapore
2       4.0   NaN  178100      China

   NumRooms   Price  ...  country_Germany  country_Singapore
0       NaN  127500  ...             True              False
1       2.0  106000  ...            False               True
2       4.0  178100  ...            False              False

[3 rows x 6 columns]
```



————————————————————————————————————————————

### 将数据转换为张量格式

当我们将数据预处理完毕后可以将DataFrame类型的数据重新转换为Tensor张量类型

```python
import torch

X, y = torch.tensor(inputs.values), torch.tensor(outputs.values)
X, y

>>>
(tensor([[3., 1., 0.],
         [2., 0., 1.],
         [4., 0., 1.],
         [3., 0., 1.]], dtype=torch.float64),
 tensor([127500, 106000, 178100, 140000]))
```



——————————————————————————————————————————————







## 2.3线性代数



### 标量

标量由只有一个元素的张量表示，简单点来说其实标量就是一个常数，但是这个常数被赋给了一个变量，则成这个张量为标量



—————————————————————————————————————————————

### 向量

向量可以被视为标量值组成的列表，这些标量值被称为向量的*元素*或*分量*,向量通常有一个轴为1，但是大量的文献认为，**列向量时向量的默认方向**，因此我们可以把向量理解成 **n行1列**的**矩阵**



——————————————————————————————————————————————

### 长度、维数、形状

向量只是一个数字数组，就像每个数组都有一个长度一样，每个向量也是如此，而向量的长度通常称为向量的**维度**

与普通python 的数组一样，我们可以通过调用python的内置len（）函数来访问张量的长度

```python
import torch
a = torch.arange(6)
print(len(a))

>>>
6
```



当用张量表示一个向量（只有一个轴）时，我们也可以通过.shape属性访问向量的长度。形状（shape）是一个元素组，列出了张量言每个轴的长度（维数）。对于只有一个轴的张量，形状只有一个元素

```python
import torch
a = torch.arange(6).reshape(2,3)
print(len(a))      # 这里的获取的是张量的行数
print(a.shape)     

>>>
2
torch.Size([2, 3])
```



注意：***维度***这个词在不同上下文时往往会有不同的含义，而一般来讲

***向量*** 或***轴*** 的维数被用来表示*向量* 或*轴* 的**长度**，即向量或轴的元素数量

然而，**张量的维度**用来表示**张量具有的轴数**，也就是说，张量有多少维，而张量的某个轴的维数就是这个轴的长度

简单点来说，如果时多维的时候，维度表示的是张量的维度（轴的**个数**）

​							当为一维（一个轴有值）时，维度表示的是这个轴的**长度**



——————————————————————————————————————————————————

### 矩阵

正如**向量**将标量从零阶推广到**一阶**，**矩阵**将向量从一阶推广到**二阶**

当调用的函数来实例化张量是，我们可以通过指定两个分量m和n来创建一个形状为m x n的矩阵

```python
A = torch.arange(20).reshape(5, 4)
print(A)

>>>
tensor([[ 0,  1,  2,  3],
        [ 4,  5,  6,  7],
        [ 8,  9, 10, 11],
        [12, 13, 14, 15],
        [16, 17, 18, 19]])
```

当交换矩阵的行或列时，结果称为矩阵的转置，通常用aT表示矩阵的转置

```python
import torch
a = torch.arange(12).reshape(3,4)
print(a)
print(a.T)

>>>
tensor([[ 0,  1,  2,  3],
        [ 4,  5,  6,  7],
        [ 8,  9, 10, 11]])
tensor([[ 0,  4,  8],
        [ 1,  5,  9],
        [ 2,  6, 10],
        [ 3,  7, 11]])
```

矩阵中有很多类型的矩阵，其中有一种叫对称矩阵

```python
import torch
a = torch.arange(9).reshape(3,3)
b = a.T
c = a + b
print(c)
print(c==c.T)

>>>
ensor([[ 0,  4,  8],
        [ 4,  8, 12],
        [ 8, 12, 16]])
tensor([[True, True, True],
        [True, True, True],
        [True, True, True]])
```



————————————————————————————————————————————————

### Hadamard积

两个矩阵按元素乘法，即一个矩阵对应的元素乘另一个元素中位置对应的元素

![1682850095323](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1682850095323.png)

简单点来解释：其实Hadamard就是matlab中的点乘

```python
A = torch.arange(20, dtype=torch.float32).reshape(5, 4)
B = A.clone()  # 通过分配新内存，将A的一个副本分配给B
print(A*B)

>>>
tensor([[  0.,   1.,   4.,   9.],
        [ 16.,  25.,  36.,  49.],
        [ 64.,  81., 100., 121.],
        [144., 169., 196., 225.],
        [256., 289., 324., 361.]])
```

将张量乘以或加上一个标量不会改变张量的形状，其中张量的每个元素都将与标量相加或相乘。



——————————————————————————————————————————————

### 降维

我们可以对任意张量进行的一个有用的操作是计算其元素的和，数字表示法使用∑符号表示求和

为了表示长度为d的向量中元素的总和，可以记为

$$
\sum_{i=0}^d
$$
默认情况下，调用**求和函数**会沿所有的轴**降低张量的维度**，，使它一个标变成量。我们还可以指定张量沿着哪一个轴来通过求和降低维度。

以矩阵为例，为了通过求和所有行的元素来降维（轴0），可以在调用函数时指定`axis=0`。 由于输入矩阵沿0轴降维以生成输出向量，因此输入轴0的维数在输出形状中消失。

```python
import torch
A = torch.arange(20, dtype=torch.float32).reshape(5, 4)
print(A)
A_sum_axis0 = A.sum(axis=0)    # 按列相加
print(A_sum_axis0)
print(A_sum_axis0.shape)

>>>
tensor([[ 0.,  1.,  2.,  3.],
        [ 4.,  5.,  6.,  7.],
        [ 8.,  9., 10., 11.],
        [12., 13., 14., 15.],
        [16., 17., 18., 19.]])
tensor([40., 45., 50., 55.])
torch.Size([4])
```

沿着行和列对矩阵求和，等价于对矩阵的所有元素进行求和。

```python
A.sum(axis=[0, 1])  # 结果和A.sum()相同

>>>
tensor(190.)
```



一个与求和相关的量是*平均值*（mean或average）。 我们通过将总和除以元素总数来计算平均值。 在代码中，我们可以调用函数来计算任意形状张量的平均值。

```python
A.mean(), A.sum() / A.numel()

>>>
(tensor(9.5000), tensor(9.5000))
```



同样，计算平均值的函数也可以沿指定轴降低张量的维度。

```python
A.mean(axis=0), A.sum(axis=0) / A.shape[0]

>>>
(tensor([ 8.,  9., 10., 11.]), tensor([ 8.,  9., 10., 11.]))
```



- 轴（axis)：保护数据的维度，数组最外围的维度axis=0
    - 矩阵（二维数组）
        - 第一轴`(axis=0)`是矩阵的列操作
        - 第二轴`(axis=1)`是矩阵的行操作
    - 三维数组
        - 第三轴`(axis=2)`为图像矩阵的通道

- 秩（rank)：轴的数量，即数组的维度



———————————————————————————————————————————

### 非降维求和

有时在调用函数来计算总和或均值时保持轴数不变会十分有用

```python
import torch
a = torch.arange(12).reshape(3,4)
sum_a = a.sum(axis = 1 ,keepdims = True)   # 按行相加，并且保持轴数，
sum_a1 = a.sum(axis = 0)   # 按列进行相加，并且不保持相加后的形状
sum_a2 = a.sum(axis = 1)   # 按行进行相加，并且不保持相加后的形状，以行的形式输出
print(sum_a)
print(sum_a1)
print(sum_a2)

>>>
tensor([[ 6],
        [22],
        [38]])
tensor([12, 15, 18, 21])
tensor([ 6, 22, 38])
```

————————————————————

#### sum函数

由于我们在使用sum方法的同时指定了一个属性keepdims使得相加之后的张量保持有两个轴，因此可以通过广播进行运算

```python
import torch
a = torch.arange(12).reshape(3,4)
sum_a1 = a.sum(axis = 1,keepdims = True) # 列压缩，即将所有为当行所有列的元素进行相加
sum_a0 = a.sum(axis = 0,keepdims = True) # 行压缩，即将所有为当列所有行的元素进行相加
print(a)
print(sum_a1)
print(sum_a0)
print(sum_a1 + sum_a0)

>>>
tensor([[ 0,  1,  2,  3],
        [ 4,  5,  6,  7],
        [ 8,  9, 10, 11]])
tensor([[ 6],
        [22],
        [38]])
tensor([[12, 15, 18, 21]])
tensor([[18, 21, 24, 27],
        [34, 37, 40, 43],
        [50, 53, 56, 59]])
```



#注意：

np.sum函数，适用于将矩阵进行相加，同时，当axis=0时，将对矩阵进行行压缩

​																					axis=1时，将对矩阵进行列压缩



—————————————————————

#### cumsum函数

如果我们想沿着某个轴计算A元素的累积总和，比如axis=0（按行计算）

1. 对于一维输入a（可以是list，也可以是array），就是当前列之前的和加到当前列上

    ```python
    >>>import numpy as np
    >>> a=[1,2,3,4,5,6,7]
    >>> np.cumsum(a)
    array([  1,   3,   6,  10,  15,  21,  28])
    ```

    

2. 对于二维输入a，axis=0（第一行不动，其他行的值将会加上前面行的值）；

    ​							 axis=1（第一列不动，其他列的值将会加上前面列的值）

```python
>>>import numpy as np
>>> c=[[1,2,3],[4,5,6],[7,8,9]]
>>> np.cumsum(c,axis=0)
array([[ 1,  2,  3],
       [ 5,  7,  9],
       [12, 15, 18]])
>>> np.cumsum(c,axis=1)
array([[ 1,  3,  6],
       [ 4,  9, 15],
       [ 7, 15, 24]])
```



————————————————————————————————————————————

### 点积（dot）

点积就是相同为位置的按元素乘积的和：（与Hadamard积作用相同）
$$
X.T * Y=\sum_{i=1}^dXiYj
$$

```python
import torch
x = torch.arange(4,dtype = torch.float32)
y = torch.ones(4, dtype = torch.float32)
z = torch.dot(x, y)
print(x)
print(y)
print(z)

>>>
tensor([0., 1., 2., 3.])
tensor([1., 1., 1., 1.])
tensor(6.)
```



点积在很多方面都会有用，当权重为非负数且和为1，即：
$$
\sum_{i=1}^d Wi=1
$$
时，点击表示**加权平均**



————————————————————————————————————————————

### 矩阵向量积

相当于矩阵乘以一个向量 

即：

![\mathbf{A} = \begin{bmatrix} a_{11} & a_{12} & \cdots & a_{1n}\\ a_{21} & a_{22} & \cdots & a_{2n}\\ \cdots & \cdots & \cdots & \cdots\\ a_{m1} & a_{m2} & \cdots & a_{mn} \end{bmatrix} \qquad \vec{x} = \begin{bmatrix} x_1\\ x_2\\ \cdots\\ x_n \end{bmatrix}](https://private.codecogs.com/gif.latex?%5Cmathbf%7BA%7D%20%3D%20%5Cbegin%7Bbmatrix%7D%20a_%7B11%7D%20%26%20a_%7B12%7D%20%26%20%5Ccdots%20%26%20a_%7B1n%7D%5C%5C%20a_%7B21%7D%20%26%20a_%7B22%7D%20%26%20%5Ccdots%20%26%20a_%7B2n%7D%5C%5C%20%5Ccdots%20%26%20%5Ccdots%20%26%20%5Ccdots%20%26%20%5Ccdots%5C%5C%20a_%7Bm1%7D%20%26%20a_%7Bm2%7D%20%26%20%5Ccdots%20%26%20a_%7Bmn%7D%20%5Cend%7Bbmatrix%7D%20%5Cqquad%20%5Cvec%7Bx%7D%20%3D%20%5Cbegin%7Bbmatrix%7D%20x_1%5C%5C%20x_2%5C%5C%20%5Ccdots%5C%5C%20x_n%20%5Cend%7Bbmatrix%7D)

那么矩阵与向量的积为：

![\begin{align*} \mathbf{A} \vec{x} &= \begin{bmatrix} a_{11} & a_{12} & \cdots & a_{1n}\\ a_{21} & a_{22} & \cdots & a_{2n}\\ \cdots & \cdots & \cdots & \cdots\\ a_{m1} & a_{m2} & \cdots & a_{mn} \end{bmatrix} \begin{bmatrix} x_1\\ x_2\\ \cdots\\ x_n \end{bmatrix}\\ &= \begin{bmatrix} a_{11}x_1 + a_{12}x_2 + \cdots + a_{1n}x_n\\ a_{21}x_1 + a_{22}x_2 + \cdots + a_{2n}x_n\\ \cdots\\ a_{m1}x_1 + a_{m2}x_2 + \cdots + a_{mn}x_n \end{bmatrix}\\ &= x_1 \begin{bmatrix} a_{11}\\ a_{21}\\ \cdots\\ a_{m1} \end{bmatrix} + x_2 \begin{bmatrix} a_{12}\\ a_{22}\\ \cdots\\ a_{m2} \end{bmatrix} + \cdots + x_n \begin{bmatrix} a_{1n}\\ a_{2n}\\ \cdots\\ a_{mn} \end{bmatrix} \end{align*}](https://private.codecogs.com/gif.latex?%5Cbegin%7Balign*%7D%20%5Cmathbf%7BA%7D%20%5Cvec%7Bx%7D%20%26%3D%20%5Cbegin%7Bbmatrix%7D%20a_%7B11%7D%20%26%20a_%7B12%7D%20%26%20%5Ccdots%20%26%20a_%7B1n%7D%5C%5C%20a_%7B21%7D%20%26%20a_%7B22%7D%20%26%20%5Ccdots%20%26%20a_%7B2n%7D%5C%5C%20%5Ccdots%20%26%20%5Ccdots%20%26%20%5Ccdots%20%26%20%5Ccdots%5C%5C%20a_%7Bm1%7D%20%26%20a_%7Bm2%7D%20%26%20%5Ccdots%20%26%20a_%7Bmn%7D%20%5Cend%7Bbmatrix%7D%20%5Cbegin%7Bbmatrix%7D%20x_1%5C%5C%20x_2%5C%5C%20%5Ccdots%5C%5C%20x_n%20%5Cend%7Bbmatrix%7D%5C%5C%20%26%3D%20%5Cbegin%7Bbmatrix%7D%20a_%7B11%7Dx_1%20&plus;%20a_%7B12%7Dx_2%20&plus;%20%5Ccdots%20&plus;%20a_%7B1n%7Dx_n%5C%5C%20a_%7B21%7Dx_1%20&plus;%20a_%7B22%7Dx_2%20&plus;%20%5Ccdots%20&plus;%20a_%7B2n%7Dx_n%5C%5C%20%5Ccdots%5C%5C%20a_%7Bm1%7Dx_1%20&plus;%20a_%7Bm2%7Dx_2%20&plus;%20%5Ccdots%20&plus;%20a_%7Bmn%7Dx_n%20%5Cend%7Bbmatrix%7D%5C%5C%20%26%3D%20x_1%20%5Cbegin%7Bbmatrix%7D%20a_%7B11%7D%5C%5C%20a_%7B21%7D%5C%5C%20%5Ccdots%5C%5C%20a_%7Bm1%7D%20%5Cend%7Bbmatrix%7D%20&plus;%20x_2%20%5Cbegin%7Bbmatrix%7D%20a_%7B12%7D%5C%5C%20a_%7B22%7D%5C%5C%20%5Ccdots%5C%5C%20a_%7Bm2%7D%20%5Cend%7Bbmatrix%7D%20&plus;%20%5Ccdots%20&plus;%20x_n%20%5Cbegin%7Bbmatrix%7D%20a_%7B1n%7D%5C%5C%20a_%7B2n%7D%5C%5C%20%5Ccdots%5C%5C%20a_%7Bmn%7D%20%5Cend%7Bbmatrix%7D%20%5Cend%7Balign*%7D)

因此矩阵与向量的积，既可以看作A的行向量与列向量的点积，又可以看作A的列向量的加权和

```python
import torch
a = torch.arange(12).reshape(3,4)
b = torch.arange(4)
c = torch.mv(a,b)
print(a)
print(b)
print(c)

>>>
tensor([[ 0,  1,  2,  3],
        [ 4,  5,  6,  7],
        [ 8,  9, 10, 11]])
tensor([0, 1, 2, 3])		# 这里创建向量的时候张量的大小可能是一行四列，也可能是四行一列，矩阵与向量的积的时候将使用四行一列
tensor([14, 38, 62])
```

**向量积就相当于整个向量乘以矩阵中的每一行的相加的和所组成另一个向量。**



————————————————————————————————————————————

### 矩阵-矩阵乘法

矩阵乘法就是**行乘列**或**列称行**

注：两个矩阵相乘要么**形状一样**，要么**第一个矩阵的列数等于第二个矩阵的行数，**才可以进行相乘。

```python
import torch
a = torch.arange(12).reshape(3,4)
b = torch.arange(8).reshape(4,2)
c = torch.mm(a,b)               # 矩阵相乘，行乘列
print(a)
print(b)
print(c)

>>>
tensor([[ 0,  1,  2,  3],
        [ 4,  5,  6,  7],
        [ 8,  9, 10, 11]])
tensor([[0, 1],
        [2, 3],
        [4, 5],
        [6, 7]])
tensor([[ 28,  34],
        [ 76,  98],
        [124, 162]])
```



————————————————————————————————————————————

### 范数

范数就是一条将向量转换为标量的函数，常用的范数有：

————————————————————

#### L1范数：曼哈顿距离

$$
||x|| =  \sum_{i}^n|Xi|
$$

————————————————————

#### L2范数：欧几里得范数

$$
||x|| =  \sqrt \sum_{i}^n Xi^2
$$



例子：

```python
import torch
a = torch.tensor([3, 4])
print(a)
print(a.type())
c = torch.Tensor([3,4])
print(c)
print(c.type())
b = torch.norm(c)       # 这里使用的是欧几里得范数，这个函数需要输入的类型为浮点型或复数型
print(b)

>>>
tensor([3, 4])
torch.LongTensor        # 当使用的是tensor函数将会创建一个数据类型为整数型的张量
tensor([3., 4.])
torch.FloatTensor       # 当使用的是实例化Tensor类来创建张量的话将会创建一个浮点型的张量
tensor(5.)
```



——————————————————————————————

#### torch.norm(**input, p, dim,** keepdim, out, dtype)

input：输入张量。它的数据类型必须是**浮点型**或**复数型**。对于复数的输入，范数使用每个元素的绝对值。注意，输入张量中元素的数据类型一定得是浮点型或者是复数哦，不然就会报错！这个就是主要变化，其次是不能使用 input.norm

p：范数的阶数。默认是2阶—“fro”，也就是弗罗贝尼乌斯范数（Frobenius norm）。如果输入p=某个正整数，则求解对应的p阶范数。其公式为  sum(abs(x)**p)**(1./p)。

dim：对输入的张量计算其指定维度（如dim=1，则表示计算第二个维度）上所有元素的范数。如果不对dim进行赋值，则会计算输入张量所有维度上的范数。当然如果指定维数不在输入张量的尺寸之内，将出现错误。

**注：**输入的数据的数据类型必须为**浮点型**或**复数型**，如果不是这两种类型将会报错**RuntimeError**

——————————————————————————————

与L2范数相比，L1范数受异常值的影响较小。



类似于向量的***L2范数*</u>**，矩阵x的**Frobenius范数**是矩阵元素平方和的平方根：

![1683342118389](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683342118389.png)

```python
torch.norm(torch.ones((4, 9)))

>>>
tensor(6.)
```



———————————————————————————————————————————————

### 范数与目标

在深度学习中，**目标**通常被表达成**范数**，他的作用是解决**优化问题**

**优化问题**：*最大化分配给观测与真实观测之间的距离，使用向量标识物品，以便最小化相似项目之间的距离，最大化不同项目之间的距离*



——————————————————

### torch.sum()函数

**作用：**将张量（按某个维度进行）相加，当有dim时将按照指定维度进行相加，当没有使用dim参数的时候			将会将所有的值进行相加

格式：torch.sum(input, list: dim, bool: keepdim=False, dtype=None) → Tensor

参数：**input**:输入一个tensor
	        **dim**:要求和的维度，可以是一个列表
			**keepdim**:求和之后这个dim的元素个数为１，所以要被去掉，如果要保留这个维度，则应当			   		    keepdim=True

```python
import torch
a = torch.arange(12).reshape(3, 4)
print(a)
b = torch.sum(a, dim=0)
print(b)

>>>
tensor([[ 0,  1,  2,  3],
        [ 4,  5,  6,  7],
        [ 8,  9, 10, 11]])
tensor([12, 15, 18, 21])

```



———————————————————

注：*在使用 torch.norm求范数的时候应该将传入的张量数据类型转换为FloatTensor等的数据*

```python
import torch
import numpy as np
a = np.arange(24).reshape(2,3,4)
a = torch.Tensor(a)# 因为需要使用norm函数进行运算，所以需要先将张量的数据类型转换为指定格式
print(a) 
print(a.type())
b = torch.norm(a, dim=1)
print(b)

>>>
tensor([[[ 0.,  1.,  2.,  3.],
         [ 4.,  5.,  6.,  7.],
         [ 8.,  9., 10., 11.]],

        [[12., 13., 14., 15.],
         [16., 17., 18., 19.],
         [20., 21., 22., 23.]]])
torch.FloatTensor
tensor([[ 8.9443, 10.3441, 11.8322, 13.3791],
        [28.2843, 29.9833, 31.6860, 33.3916]])
```

———————————————————————————————————————————————









## 2.4微积分

逼近法就是***积分*** 的起源

在深度学习中，我们“训练”模型，不断更新他们，

使它们在看到越来越多的数据时变得越来越好。 通常情况下，变得更好意味着最小化一个***损失函数***（loss function）， 即一个衡量“模型有多糟糕”这个问题的分数。

最终，我们真正关心的是生成一个模型，它能够在未见过的数据上能够达到我们的要求，因此我们可以将拟合模型的任务分解为两个**关键问题**：

- **优化：**使用模型**拟合**观测数据的过程
- **泛化：**生成出有效性超出用于训练的数据集本身的模型，即生成能够**适应新样本**的模型



————————————————————————————

### 导数

如果   **f‘（x）**存在，则称 f 在在a处是可微的。如果 f 在一个区间内的每个数上都是可微的，则此函数在此区间中都是可微的。也可以说导数就是**曲线的斜率**

我们可以将 [(2.4.1)](https://zh.d2l.ai/chapter_preliminaries/calculus.html#equation-eq-derivative)中的导数  **f'(x)** 解释为 **f(x)**相对于**x**的*瞬时*（instantaneous）变化率

 所谓的瞬时变化率是基于**x**中的变化ℎ，且ℎ接近0。

![1683356991061](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683356991061.png)



———————————————————————————

### 偏导数

导数就是仅含有一个变量的函数的微分，而偏导数则就是多个变量的函数的微分

![1683358696294](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683358696294.png)

   

———————————————————————————

### 梯度

梯度就是一个包含多元函数对其所有变量的偏导数所组成的向量

**![1683361744302](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683361744302.png)**



———————————————————————————

### 链式法则

![1683363045175](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683363045175.png)







## 2.5自动微分

深度学习框架通过自动计算导数，即 *自动微分* 来加快求导

——————————

#### 最小二乘法

最小二乘法通常使用在损失函数中，放大误差，当最小二乘函数趋近于0，则就表示实际输出与期望输出的值误差相当的小

形式主要如下式：
$$
损失函数 = \sum(目标样本值 - 实际理论值)^2
$$



——————————

#### 梯度下降法

梯度下降算法就是通过实际输出和期望输出之间的误差E和梯度，确定连接权重的w的调整值，得到新的连接权重w。然后按照这个步骤不断调整权重以使误差达到最小，从中学习得到最优的连接权重

![1683379270332](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683379270332.png)

 梯度下降法的具体做法是：

**通过最小二乘法计算损失函数，然后对损失函数进行求导，得到梯度，然后乘以步长然后对权重以及偏置进行调整，具体公式为**;

![1683434806193](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683434806193.png)

其中

Wj为新的权重值，简单点来说可以理解成：
$$
新权重Wj=现权重Wj+(-损失函数的导数（-为反向）*步长)
$$
a为步长，当a值很大的时候，那么梯度下降的过程中我们将会迈大步子下山

​				 当a的值很小的时候，那么梯度下降的过程中我们将会迈小步子下山



——————————

### 反向传播算法（bp算法）

反向传播算法一般使用计算图的方式进行模块化的运算

![1683435323312](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683435323312.png)

做法：

（1）通过期望输出减去实际输出计算出损失函数

（2）通过对损失函数进行求导决定梯度

其中L对w的偏导 = L对y的偏导 * y对w的偏导，即求出了梯度，这种方法叫做**链式法则**

即$df/dx = df/dy*dy/dz*dz/dx$其中，$dz/dx$是下一层权重参数对上一层权重参数的梯度，该梯度使用雅可比矩阵进行表示

（3）乘以步长

（4）相乘后与原来的权重W或b相减，进行调整



———————————————————————————————————————————————

### 自动求导

深度学习框架通过自动计算导数，即***自动微分*** 来加快求导。来加快求导。

自动微分能够使系统能够随后反向传播梯度。

举个栗子：

![1683444842536](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683444842536.png)

首先，我们创建变量x并为其分配一个初始值

```python
import torch
x = torch.arange(4.0, requires_grad=True)
# 这里的requires_grad=True的作用是让backward（反向传播）可以跟踪这个参数并且计算它的梯度，即使当前的参数的梯度可以被保存在grad中
```

只有requires_grad=True的参数才会参与求导，如果没有这个参数，那么参数在进行求导的时候会报错

注：如果一个变量a被赋值给另一个变量b的时候，那么变量b也会由requires_grad=True这个参数

由于我们这里是对 函数及逆行求导的，所以：

```python
z = 3 * torch.dot(x,x)  # 将函数赋值给z，并把x传入进去
z.backward()            # 计算函数的梯度向量,返回的是向量
print(x)
print(x.grad， x.requires_grad)
print(x.grad == 6 * x)  # 验证关于x的梯度值是否正确

>>>
tensor([0., 1., 2., 3.], requires_grad=True)
tensor([ 0.,  6., 12., 18.])
tensor([True, True, True, True])
```



———————————————————————————————————————————

### 非标量变量的反向传播

如果y不是标量时，向量y将会是向量x的导数矩阵。对于高阶和高维的`y`和`x`，求导的结果可以是一个高阶张量。

```python
# 对非标量调用backward需要传入一个gradient参数，该参数指定微分函数关于self的梯度。
# 本例只想求偏导数的和，所以传递一个1的梯度是合适的
x.grad.zero_()  # 在默认情况下，PyTorch会累积梯度，我们需要清除之前的值
y = x * x
# 等价于y.backward(torch.ones(len(x)))   # 后面这个传入的张量将会与计算好梯度后的向量点乘
y.sum().backward()
print(x.grad)

>>>
tensor([0., 2., 4., 6.])
```



———————————————————————————————————————————

### 分离计算 detach()函数

有时我们希望将某些计算移动到记录的计算图之外

假设有模型A和模型B，我们需要将A的输出作为B的输入，但训练时我们只能训练模型B，那么就可以使用torch.Tensor.detach()函数，返回一个新的张量，该张量与当前的计算图分离，结果将不需要梯度

```python
import torch
a = torch.arange(4.0, requires_grad=True)
b = a * a
u = b.detach()
z = u * a
z.sum().backward()     # 这里对z进行了求导，但由于u为b的分离变量，因此将u看作常数
print(a.grad)		   # 然后进行计算关于x的偏导数，因此导出来即变成 z = u * 1
print(a.grad == u)
print(a.grad == a**2)

>>>
tensor([0., 1., 4., 9.])    
tensor([True, True, True, True])
tensor([True, True, True, True])
```



———————————————————————————————————————————

### Python控制流的梯度计算

```python
import torch
def f(a):
    b = a * 2
    while b.norm() < 1000:   # 范数：先平方过后相加然后开根号
        print(b.norm())
        b = b * 2
    if b.sum() > 0:
        c = b
    else:
        c = b * 100
    return c
a = torch.ones(size=(), requires_grad=True)
d = f(a)
d.backward()
print(a.grad)          # 这里的意思是：对于任何a，存在某个常量标量k使它满足上
print(d/a)			   # 面的条件，因此这里的公式为f(a)=k*a
print(d)  			   # 当求其梯度的时候，开导结果就为，

>>>
tensor(2., grad_fn=<LinalgVectorNormBackward0>)
tensor(4., grad_fn=<LinalgVectorNormBackward0>)
tensor(8., grad_fn=<LinalgVectorNormBackward0>)
tensor(16., grad_fn=<LinalgVectorNormBackward0>) 
tensor(32., grad_fn=<LinalgVectorNormBackward0>)
tensor(64., grad_fn=<LinalgVectorNormBackward0>)
tensor(128., grad_fn=<LinalgVectorNormBackward0>)
tensor(256., grad_fn=<LinalgVectorNormBackward0>)
tensor(512., grad_fn=<LinalgVectorNormBackward0>)
tensor(1024.)
tensor(1024., grad_fn=<DivBackward0>)
tensor(1024., grad_fn=<MulBackward0>)
```

size=()里面没有数是生成标量，有一个数就是向量，两个就是矩阵。

在张量中，**标量是没有维度**的，只有**一个维度**的叫**向量，**有**两个维度**的叫**矩阵**

一般来说**tensor可以生成标量**，但**Tensor不能生成标量**只能生成**向量**或**矩阵**

————————————

问题：在已经进行一次backward求导过后能不能在进行求导

```python
import torch
def f(a):
    b = a * 2
    while b.norm() < 1000:   # 范数：先平方过后相加然后开根号
        # print(b.norm())
        b = b * 2
    if b.sum() > 0:
        c = b
    else:
        c = b * 100
    return c
a = torch.ones(size=(), requires_grad=True)
d = f(a)
d.sum().backward(retain_graph=True)
d.sum().backward()       # 当做第二次反向传播求导的时候，将会对求导的结果与上一次求导的结果进行相加
print(a.grad)
# print(d/a)
print(d)

>>>
tensor(2048.)
tensor(1024., grad_fn=<MulBackward0>)
```

由于pytroch在进行求导的时候将会将计算图抹除以节省内存消耗，因此当需要进行多次的反向传播求导的时候需要加上retain_graph=True

并且**多次求导过后的结果**将会是**所有求导结果的相加结果**



————————————————————————————————————————————

### 概率

在统计学中，我们把从概率分布中抽取样本的过程称为抽样，就比如，掷色子，得到的一面的值就将这个面记录一次，这个就称为抽样

笼统来说，可以把分布看作对事件的概率分配

————————————————

#### 多项分布multinomial.Multinomial()

多项分布Multinomial()是torch.distributions.multinomial中的一个类，接受四个参数

(**total_count**=**1**, **probs**=**None**, **logits**=**None**, **validate_args**=**None**)：

参数：

》**total_count**接受的int型参数，指的是单次抽样中的抽取样本的个数

》**probs**接受的是Tensor型参数，指的是个**事件发生的概率**，也可以传入频数，如果传入的是频数，则可以通过probs属性查看对应的概率分布

》**logits接受**的是Tensor型参数，和probs的作用一样，不过其指的是各事件概率的自然对数，也可以传入频数，在传入频数后可以通过logits属性查看相应的对数频率分布

》**validate_args**用于指定是否检查参数的合法性



————————————————

#### sample()

sample()是类Multinomial()中**用于抽样的函数**，仅接受一个参数（sample_shape=torch.Size()），用来指定要抽取多少次，默认情况下仅抽样一次，输出一个形状为《len(probs),1》的张量，否则输出为（sample_shape,len(probs)）的张量

————————————————

```python
# 掷色子采样
import torch
from torch.distributions import multinomial

fair_probs = torch.ones([6])/6
print(fair_probs)
mul = multinomial.Multinomial(1,fair_probs)  # 对概率进行多项分布，也就是将概率给到各个对象中
mul = mul.sample()   # 对已经多项分布的对象进行概率抽取，抽取一个
print(mul)

>>>
tensor([0.1667, 0.1667, 0.1667, 0.1667, 0.1667, 0.1667])
tensor([0., 0., 0., 1., 0., 0.])

```

同样的我们也可以看这个些概率如何随着时间的推移收敛到真实概率

```python
import torch
from torch.distributions import multinomial
import matplotlib.pyplot as plt
probs = torch.ones([6])
count = multinomial.Multinomial(10, probs=probs).sample((500,)) # 抽样500次，每次抽10个
cum_count = count.cumsum(dim=0)
last_count = cum_count/cum_count.sum(dim=1, keepdims=True)   # 每个数字被抽中的次数除以总共抽样的次数得到概率
plt.figure(figsize=(6, 5))
plt.axhline(y=0.167, color='black', linestyle='dashed')
for i in range(6):
    plt.plot(last_count[:, i].numpy(), label=("P(die=" + str(i + 1) + ")"))
plt.show()

>>>
```

![1683595113106](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683595113106.png)



————————————

#### 映射

映射是指两个元素集之间的相互的对应关系，相当于函数

![映射](https://bkimg.cdn.bcebos.com/pic/7aec54e736d12f2e89cbcbb64dc2d5628435681d?x-bce-process=image/resize,m_lfit,w_536,limit_1)

例如上图中的 f ，就是集合A相对于集合B的映射



——————————

### 概率论公式

在处理骰子掷出时，我们将集合S={1,2,3,4,5,6} 称为***样本空间***（sample space）或*结果空间*（outcome space）， **其中每个元素都是*结果***（outcome）。 ***事件***（event）是一组给定样本空间的**随机结果**。 例如，“看到5”（{5}）和“看到奇数”（{1,3,5}）都是掷出骰子的有效事件。 注意，如果一个随机实验的结果在A中，则事件A已经发生。 也就是说，如果投掷出3点，因为3∈{1,3,5}，我们可以说，“看到奇数”的事件发生了。

*概率* 可以被认为是将集合映射到真实值的函数

概率的三大公理：

1）概率具有非负性，即任何概率都是大于等于0的

2）概率具有规范性，即整个样本空间的概率P(S)应该是1

3）概率具有可列可加性。即对于一系列互不相容的事件，它们并集的概率，等于各自的概率之和：![1683597047435](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683597047435.png)

即如果两个集合没有交集，那么，这两个集合的并的概率，自然应该等于这两个集合的概率的和



—————————————————————————————————————————————

### 随机变量

随机变量几乎可以是任何数量，并且它可以在随机实验的一组可能性中取一个值

在掷色子的问题中，我们将S = {1,2,3,4,5,6}称为***样本空间*** 或者***结果空间*** 其中的每个元素都是***结果*** ，其中**随机变量的X**的值就在这个**样本空间S**中，我们可以将事件“看到一个5”表示为{X=5}或X=5， 其概率表示为P({X=5})或P(X=5)。

我们可以将**P(X)**表示为**随机变量X**上的**分布**，分布告诉我们呢X获得某一值的概率

离散随机变量

连续随机变量



——————————————————————————————————————————————

### 联合概率

即给定任意值**a**和**b**,联合概率可以回答： A = a和B = b**同时满足的概率**是多少，

注：对于任何a和b的取值，P(A=a,B=b) 的概率一定会 < P(A=a)，因为要考虑的东西从只有a到要同时考虑a和b，那么这是A=a和B=b同时发生的可能性不大于A=a或是B=b单独发生的概率



——————————————————————————————————————————————

### 条件概率

即给定任意值**a**和**b**,**当A已经等于a的时候，B等于b的概率**

**即以前面的事件已经发生为前提，而后面事件发生的概率**



——————————————————————————————————————————————

### 贝叶斯定理

![1683613122828](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683613122828.png)

贝叶斯定理就是用于解决**"逆概率"**的问题，即使用**未能真正解决问题的信息**求出**最后解决疑问问题发生**的概率

由上面的公式我们先看三个名词：

##### 先验概率：

先验概率就是在*<u>不知道</u>* **最终结果**和**关于发生这个结果的信息**的前提下，我们对于结果的主观判断

————————

##### 可能性函数

P(B|A)/P(B)被称为“可能性函数”，这是一个**调整因子**，也就是在得知关于发生结果的信息后我们所作的**调整**，其作用就是将**先验概率**调整到更接近真实概率



当可能性函数>1的时候，则意味着**先验概率的增强**，即这个结果最后发生的可能性变大

当可能性函数=1的时候，则意味着关于发生结果的信息对判断结果的可能性没有任何帮助

当可能性函数<1的时候，意味着**先验函数被削弱**，结果发生的可能性变小

————————

##### 后验概率

P(A|B)称为“后验概率”，即在得到先验概率和得到关于发生这个结果的信息后，最终得到的发生结果的概率

![1683614202587](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683614202587.png)

简单点来说贝叶斯定理就是使用少的信息来计算最后发生结果的概率信息



——————————————————————————————————————————————

### 边际化

即在相对多变量的联合分布而言，一个变量的概率的总和

也可以说，边际概率是一个事件的概率，与另一个变量的结果无关，即只包含其中部分变量的概率分布



——————————————————————————————————————————————

### 独立与依赖

如果两个随机变量A和B是独立的，意味着**事件A的发生**与**事件B的发生无关**，而根据贝叶斯定理，马上就能同样得到**P(A|B)=P(A)**

相反在所有其他情况下，我们称A和B依赖

比如，两次连续抛出一个骰子的事件是相互独立的。 相比之下，灯开关的位置和房间的亮度并不是（因为可能存在灯泡坏掉、电源故障，或者开关故障）。

由于P(A|B)=P(A,B)/P(B)=P(A)等价于P(A,B) = P(A)P(B)，因此两个随机变量是独立的，当且仅当两个随机变量的联合分布是其各自分布的乘积



——————————————————————————————————————————————

### 应用

![1683620559259](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683620559259.png)

![1683620574323](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683620574323.png)



——————————————————————————————————————————————

### 期望与方差

**期望**是实验中可能的结果的概率乘以其结果的总和

**方差**是在概率论和统计方差衡量随机变量或一组数据时的离散程度的度量，换句人话说就是数据之间的离散程度

![1683621088993](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683621088993.png)



————————————————————————————————————————————



### 参数初始化



### 为什么需要初始化权重

当我们在训练神经网络时，合理的权重初始化将直接决定你的模型能否收敛，如果权过小，那么输入层的信息将随着网络的深入而`逐渐消失`

我们使用sigmoid函数解释一下：

![img](https://pic3.zhimg.com/80/v2-3cdcaf82efd74be92024c15ad154498e_720w.webp)

如果我们的权重过小，那么我们输入层的值经过计算后的值将会接近于0，这也就意味着模型学习不到什么，所以堆隐层也就消失了

同样的如果输入层的权重过大，**导致到激活层的输入值过大，那么梯度接近饱和，也就接近于0，模型同样学习不到什么**







#### 默认初始化

当我们不指定初始化方法的时候，框架将会使用默认的随机初始化方法





#### Xavier初始化

对于每一个网络中的隐层，我们**希望每一层的输出方差能够固定**，因为这样能够防止我们的信号变得很大/直接消失。换句话来说，**我们需要一种权重初始化的手段，使得输入、输出的方差保持不变，**这就是Xavier初始化做的事。

Xavier初始化从均值为0，方差为
$$
\sigma^2=2/(n_i+n_o)
$$
的高斯分布中抽样权重









——————————————————————————————————————————————、











## 3.1线性回归

回归实际就是**最佳拟合**，是能为一个或多个自变量与因变量之间关系建模的一类方法，多数情况下，回归经常用来表示输入和输出之间的关系

在机器学习中，现实生活中收集的**真实数据的集合**（真实数据集）一般称为**训练数据集**

数据集中的一组对应数据称之为**样本，**即数据即中的一部分个体

试图预测的目标（比如预测房屋价格）称为***标签***（label）或***目标***（target）

预测所依据的自变量称为**特征**或**协变量**，即预测所使用的自变量可以称之为**特征**

![1683622753197](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683622753197.png)

换句话来说，这些内容是输入特征的一个*仿射变换* 

仿射变换的特点是通过加权对特征进行线性变换，并通过偏置项来进行*平移*



————————————————————————————————————————————

### 线性模型

一个常见的线性模型是：
$$
y = wx+b
$$
其中的***w***称为**权重**，权重**决定了每个特征对我们预测值的影响**

***b***称之为**偏置**（bias）、偏移量（offset）或截距（intercept），偏置是指当所有特征都取值为0时，预测值应该为多少，如果没有偏置项，我们的模型表达能力将会受到限制

给定一个数据集，我们的目标是寻找模型的权重***W***和偏置***b，***使得根据模型作出的预测大体符合数据里的真实目标，其中输出的**预测值由权重w和偏置b决定**

![1683623578133](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683623578133.png)

![1683629952155](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683629952155.png)

这个过程中的求和将使用广播机制。给定训练数据特征**X**和对应的已知标签y

线性回归的目标是**找到一组权重向量w和偏置b****：当给定从**X**的同分布中取样的新样本特征时，这组权重向量和偏置能够**使得新的样本预测标签的误差尽可能小**

虽然我们给定**x**进行预测**y**的最佳模型会是线性的，但我们很难找到一个有n个样本的真实数据集，无论我们使用什么手段来观察特征**x**和标签**y**，都可能会出现少量的观测误差。因此，即使我们坚信特征与模型的潜在关系是线性的，我们也会加入一个**噪声项**来考虑观测误差带来的影响



———————————————————————————————————————————

### 损失函数

损失函数能够量化目标的***真实值***与***预测值***之间的差距。通常我们的损失函数都是非负的，并且数值越小代表损失越小，完美预测时的损失为0

回归问题中最常用的损失函数是**平方误差函数**

![1683630920160](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683630920160.png)

由于平方误差函数中的二次方项，**估计值**与**预测值**之间**较大的差异将导致更大的损失**。为了度量模型在整个数据集上的质量，我们需计算在训练集n个样本上的损失函数（也等价于求和）

![1683679294783](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683679294783.png)

也就是说平方误差的最终的公式为：

![1683631318557](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683631318557.png)

![1683631582024](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683631582024.png)



———————————————————————————————————————————

### 解析解

线性回归是一个很简单的优化问题，一般来说，线性回归的解可以用一个公式简单的表达出来，这类的解叫做**解析解**，也就是说**解析解就是一条用于表达线性回归的解的公式**

首先，我们将**偏置b**合并到**参数w**中，合并的方法是在包含所有参数的矩阵中附加一列

![1683635355565](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683635355565.png)



————————————————————————————————————————————

### 随机梯度下降

在很多任务上，哪些难以优化的模型效果都要好很多，因此弄清楚如何训练这些难以优化的模型是非常重要的。

我们使用的是梯度下降法，它通过不断地在**损失函数递减**的方向上更新参数来降低误差

梯度下降法最简单的用法就是计算损失函数（数据集中所有样本的损失均值）关于模型参数的导数（在这里也可以称为梯度）。由于在每次更新参数之前，我们都必须要遍历整个数据集，因此，我们通常会在每次需要计算更新的时候随机抽取一小批量样本，这种变体称为**小批量随机梯度下降**



在每次迭代中，我们首先随机抽样一个小批量**B**， 它是由固定数量的训练样本组成的。 然后，我们计算小批量的平均损失关于模型参数的导数（也可以称为梯度）。 最后，我们将梯度乘以一个预先确定的正数**n**，并从当前参数的值中减掉。

![1683640326257](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683640326257.png)

总结一下，算法的步骤如下： （1）初始化模型参数的值，如随机初始化； （2）从数据集中随机抽取小批量样本且在负梯度的方向上更新参数，并不断迭代这一步骤。 对于平方损失和仿射变换，我们可以明确地写成如下形式:

![1683640474735](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683640474735.png)

公式中的**w**和**x**都是向量，|***B***|表示每个小批量中的样本数

***n***表示学习率，批量大小和学习率的值通常都是手动预先指定的，而不是通过模型训练获得的，这些可以调整但不在训练过程中更新的参数称为***超参数（hyperparameter）***

***调参（hyperparameter tuning）***是**选择超参数**的过程，超参数通常是我们根据训练迭代结果来调整的，而训练迭代结果是在独立的***验证数据集（validation dataset）***上评估得到的

在训练了预先确定的若干迭代次数后（或者直到满足某些其他停止条件后）， 我们记录下模型参数的估计值，表示为w^,b^。 但是，即使我们的函数确实是线性的且无噪声，这些估计值也不会使损失函数真正地达到最小值。 因为算法会使得损失向最小值缓慢收敛，但却<u>不能在有限的步数内非常精确地达到最小值</u>。

**泛化**：指找到一组参数，这组参数能够使得我们的模型在其他没见过的情况下能够实现较低的损失



————————————————————————————————————————————

### 用模型进行预测

当我们**使用“已学习”的线性模型**并且**通过未包含在数据集中的一个或多个随机变量**来进行对<u>新的结果的预测</u>，这种*<u>给定特征估计目标</u>*的过程称为***预测***或***推断***



————————————————————————————————————————————

### 矢量化加速

在训练我们的模型的时候，我们通常希望能够同时处理整个小批量的样本，为了实现这一点，需要我们对计算进行矢量化，从而利用线性代数库

矢量：既有方向又有大小的量，也可以说是向量

为了说明矢量化为什么如此重要，我们考虑对向量相加的两种方法。 我们实例化两个全为1的10000维向量。 在一种方法中，我们将使用Python的for循环遍历向量； 在另一种方法中，我们将依赖对`+`的调用。

```python
import time
import torch
import math
import numpy as np

class Timer:
    def __init__(self):
        self.timelist = []
        self.start()

    def start(self):
        self.a = time.time()
    def end(self):
        res_time = time.time() - self.a
        return res_time

i = 1000
c = torch.zeros([i])
a = torch.ones([i])
b = torch.ones([i])
timer = Timer()
for n in range(i):
    c[n] = a[n] + b[n]
print(f'{timer.end():.5f} sec')
timer.start()
d = a + b
print(f'{timer.end():.5f} sec')

>>>
0.00619 sec
0.0000000000 sec
```

结果很明显，第二种方法比第一种方法快的多，矢量化代码通常会带来数量级的加速。另外，我们将更多的数学运算放到库中，而无须自己编写那么多的计算，从而减少了出错的可能性。



——————————————————————————————————————————————

### 正太分布与平方损失

![1683686957900](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683686957900.png)

```python
def normal(x, mu, sigma):
    p = 1 / math.sqrt(2 * math.pi * sigma**2)
    return p * np.exp(-0.5 / sigma**2 * (x - mu)**2)
 
 # 再次使用numpy进行可视化、 
x = np.arange(-7, 7, 0.01)

# 均值和标准差对
params = [(0, 1), (0, 2), (3, 1)]
d2l.plot(x, [normal(x, mu, sigma) for mu, sigma in params], xlabel='x',
         ylabel='p(x)', figsize=(4.5, 2.5),
         legend=[f'mean {mu}, std {sigma}' for mu, sigma in params])
         
>>>
```

### ![../_images/output_linear-regression_216540_70_0.svg](https://zh.d2l.ai/_images/output_linear-regression_216540_70_0.svg)

可以看到改变均值会产生沿着x轴的偏移，增加方差将会使得分布的宽度增加

![1683688043356](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683688043356.png)



————————————————



#### Xavier初始化





————————————————

#### 似然

似然与概率是互逆的，已知到结果出现的可能性，对分布的参数进行估计或则是猜测，估计参数的可能性	

即根据已经发生的结果来判断事情本身的性质

简单点来说似然求的是参数



————————————————

#### 概率

概率是从分布中采样是从已知的信息中得到的结果出现的可能性

在统计学中，概率是在特定环境下某件事情发生的可能性，即在结果没有产生前，我们使用已知的参数对结果发生的可能性的一个估计

概率求的是事情发生的可能性

————————————————

#### 最大似然估计

利用已知的样本标记结果，**反推**最大概率导致这些样本结果出现的**模型参数**





—————————————————————————————————————————————

### 线性回归从零开始实现

我们的任务是使用有限样本的数据集来恢复模型的参数



##### 步骤一：生成训练集

在下面的代码中，我们将生成一个包含1000个样本的数据集，每个样本包含从标准正态分布中采样的2个特征，

```python
import torch
import random
import matplotlib.pyplot as plt
def synthetic_data(w, b, example_num):
    X = torch.normal(0, 1, (example_num, len(w)))
    y = torch.matmul(X , w) + b
    y += torch.normal(0, 0.1, y.shape)
    print(y.shape)
    print(X.shape)
    return X, y

true_w = torch.tensor([3.14, -1.3])
true_b = 4.2
x, res = synthetic_data(true_w, true_b, 1000)
print('x', x[0])
print('res', res[0])
plt.figure(figsize=(6, 5))
plt.scatter(x[:, 0].detach().numpy(), res)
plt.scatter(x[:, 1].detach().numpy(), res)
plt.show()

>>>
torch.Size([1000])
torch.Size([1000, 2])
x tensor([-0.1160,  2.2321])
res tensor(0.8713)
```

![1683701680821](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683701680821.png)



##### 步骤二：读取数据集

当我们训练模型的时候要对数据集进行遍历，每次抽取一小批量样本，并使用它们来更新我们的模型，

在下面的代码中，我们定义一个data_iter函数，该函数接收**批量大小**、**特征矩阵**和**标签向量**作为<u>输入</u>，生成大小为batch_size的小批量，每个小批量包含一组特征和标签

```python
def data_iter(batch_size, features, labels):  # 传入批量的大小，特征，标签
    example_num = len(features)     # 获取维度1的特征个数
    indices = list(range(example_num))  # 根据维度1的特征个数建立数字表
    random.shuffle(indices)         # random.shuffle函数用于将列表打乱
    for i in range(0, example_num, batch_size):  # 遍历1000个特征和标签，并且每次间隔10，即批量大小为10
        batch_indices = torch.tensor(indices[i:min(i+batch_size,1000)])   # 将得到的10个索引创建成张量的形式
        yield features[batch_indices], labels[batch_indices]   # yield生成器，返回指定的特征值，和标签值
batch_size = 10
for x,y in data_iter(batch_size, x, res):
    print(x,'\n',y)
    
>>>
tensor([[-0.3746, -0.8597],
        [ 1.5802, -0.1383],
        [ 1.4816, -0.5512],
        [ 0.8667,  0.6771],
        [ 1.2265, -0.2049],
        [ 1.7889, -0.1030],
        [-2.2421, -0.8650],
        [ 2.0361, -2.0575],
        [ 0.1986,  1.2264],
        [ 0.0135, -0.2687]]) 
 tensor([ 4.1040,  9.3118,  9.6484,  5.8194,  8.3751,  9.8716, -1.7335, 13.2489,
         3.3533,  4.6096])
         ...
```

我们直观感受一下小批量运算：读取第一个小批量数据样本并打印。 每个批量的特征维度显示批量大小和输入特征数。 同样的，批量的标签形状与`batch_size`相等。

当我们运行迭代时，我们会连续地获得不同的小批量，直至遍历完整个数据集。上面实现的迭代对教学来说很好，但它的执行效率很低，可能会在实际问题上陷入麻烦。 例如，它要求我们将所有数据加载到内存中，并执行大量的随机内存访问。 在深度学习框架中实现的**内置迭代器**效率要高得多， 它可以处理存储在文件中的数据和数据流提供的数据。



————————————————————————————————————————————

### 定义模型

接下来，我们必须定义模型，将模型的输入和参数同模型的输出关联起来。

```python
def linemodel(X, w, b):
    '''线性回归模型'''
    return torch.matmul(X,w)+b
```



————————————————————————————————————————————

### 定义损失函数

因为需要计算损失函数的梯度，所以我们应该先定义损失函数

```python
def square_loss(y_hat, y):
    '''平方损失函数'''
    return (y_hat-y.reshape(y_hat.shape))**2/2
```



————————————————————————————————————————————

### 定义优化算法

在每一步中，使用从数据集中随机抽取的一个小批量，然后根据参数计算损失的梯度。 接下来，朝着减少损失的方向更新我们的参数。 下面的函数实现小批量随机梯度下降更新。 该函数接受模型参数集合、学习速率和批量大小作为输入。每 一步更新的大小由学习速率`lr`决定。 因为我们计算的损失是一个批量样本的总和，所以我们用批量大小（`batch_size`） 来规范化步长，这样步长大小就不会取决于我们对批量大小的选择。

```python
def sdg(params, lr, batch_size):
    '''优化算法'''
    with torch.no_grad:     # 每次进行梯度更新的时候，先把先前自动计算出的梯度清零，然后在反向传播时，该tensor就会自动求导，（注意，当requires_grad=True的时候，可以看作这个权重处于计算图中，而在计算图中，这个权重又与别的权重相关联，而计算图并不能直接更改，因此我们需要将其设置为False来打破这层关系，此时就相当于将这个权重从计算图中取了出来进行更新），而使用了with torch.no_grad就可以打破这层关系，当程序执行到下一次循环的时候（离开with板块时），重新更新过的权重的requires_grad又会重新变为True
        for param in params: # 遍历参数
            param -= lr * param.grad / batch_size # 对参数实现梯度下降算法
            param.grad.zero_()  # 将梯度清零
```



————————————————————————————————————————————

### 训练

现在我们已经准备好了模型训练所有需要的要素，可以实现主要的训练过程部分了。在每次迭代中，我们读取一小批量训练样本，并通过我们的模型来获得一组预测。 计算完损失后，我们开始反向传播，计算并存储每个参数的梯度。 最后，我们调用优化算法`sgd`来更新模型参数。

```python
'''线性模型'''
import torch
import random
import matplotlib.pyplot as plt

'''生成数据集'''
def synthetic_data(w, b, example_num):
    X = torch.normal(0, 1, (example_num, len(w)))
    y = torch.matmul(X , w) + b
    y += torch.normal(0, 0.1, y.shape)
    # print(y.shape)
    # print(X.shape)
    return X, y

true_w = torch.tensor([3.14, -1.3])
true_b = 4.2
x, res = synthetic_data(true_w, true_b, 1000)  # 返回特征值和标签

# print('x', x[0])
# print('res', res[0])
# plt.figure(figsize=(6, 5))
# plt.scatter(x[:, 0].detach().numpy(), res)
# plt.scatter(x[:, 1].detach().numpy(), res)
# plt.show()

'''随机读取数据集'''
def data_iter(batch_size, features, labels):  # 传入批量的大小，特征，标签
    example_num = len(features)     # 获取维度1的特征个数
    indices = list(range(example_num))  # 根据维度1的特征个数建立数字表
    random.shuffle(indices)         # random.shuffle函数用于将列表打乱
    for i in range(0, example_num, batch_size):  # 遍历1000个特征和标签，并且每次间隔10，即批量大小为10
        batch_indices = torch.tensor(indices[i:min(i+batch_size,1000)])   # 将得到的10个索引创建成张量的形式
        yield features[batch_indices], labels[batch_indices]   # yield生成器，返回指定的特征值，和标签值
# batch_size = 10
# for x,y in data_iter(batch_size, x, res):
#     print(x,'\n',y)

def linemodel(X, w, b):
    '''线性回归模型'''
    return torch.matmul(X,w)+b     # 输入我们要回归的模型

def square_loss(y_hat, y):
    '''平方损失函数'''
    return (y_hat - y.reshape(y_hat.shape))**2/2  # 直接使用平方损失函数

def sdg(params, lr, batch_size):
    '''优化算法'''
    with torch.no_grad():     # 所有计算得出的tensor的requires_grad都自动设置为False
        for param in params: # 遍历参数
            param -= lr * param.grad / batch_size # 对参数实现梯度下降算法
            param.grad.zero_()  # 将梯度清零

lr = 0.02 # 设置学习率
num_epochs = 10 # 设置训练次数
net = linemodel
loss = square_loss
w = torch.normal(0, 0.01, size=(2,1), requires_grad=True)
b = torch.zeros(1, requires_grad=True)
batch_size = 10
for epoch in range(num_epochs):    # 循环训练
    for feature, label in data_iter(batch_size, x, res):  # 随机读取数据集中的数据,获取特征值和标签

        l = loss(net(feature, w, b), label)   # 预测值与真实值的批量损失
        l.sum().backward()   # 计算损失函数的梯度并存储在 l.grad中
        sdg([w,b], lr, batch_size)

    # loss2 = np.mean(l.data.numpy())
#     print(f'epoch{epoch}','loss:',loss2)
#         # print("last loss: " + str(loss(net(feature, w, b), label)))
# print(w,b)

    with torch.no_grad():
        train_l = loss(net(x, w, b), res)
        print("epoch ", str(epoch+1), "loss: ",float(train_l.mean())))
    
>>>
epoch  1 loss:  0.265867680311203
epoch  2 loss:  0.009706390090286732
epoch  3 loss:  0.004930813796818256
epoch  4 loss:  0.004797463770955801
epoch  5 loss:  0.004792340565472841
epoch  6 loss:  0.004797650035470724
epoch  7 loss:  0.004795545246452093
epoch  8 loss:  0.0047917794436216354
epoch  9 loss:  0.004792542662471533
epoch  10 loss:  0.004797756671905518
```



————————

#### with torch.no_grad()

这个函数用于torch中指定不需要进行计算梯度的部分，并且with能够在合适的时候取消这个函数的作用

——————————————————————————————————————————————



### 线性回归的简洁实现

参考上面的线性回归简单的实现，我们其实有更加简单的回归模型实现方式

————————————

#### 生成数据集

我们首先生成数据集

我们使用回上面的生成函数

```python
import torch
from torch.utils import data
import numpy as np

def synthetic_data(w, b, example_num):
	x = torch.normal(0, 1, (example_num, len(w)))
	y = torch.matmul(x, w) + b
	y += torch.normal(0, 0.1, y.shape)
	return x, y
	
true_w = torch.tensor([3.14, 4.12])
true_b = 4
features, label = synthetic_data(true_w, true_b, 1000)
```



————————————

#### 读取数据集

我们可以调用框架中现有的API来读取数据，我们将features和labels作为API的参数传递，并且通过batch_size 将数据集分成多块样本，同时使用布尔值is_train表示是否希望数据迭代器对象在每个迭代周期内打乱数据。

```python
def load_array(data_array, batch_size, is_train=True):    # 读取数据集
    dataset = data.TensorDataset(*data_array)     # 对生成的标签进行打包，打包成一个数据集
    return data.DataLoader(dataset, batch_size, shuffle=is_train)   # 对数据集进行分包，并且打乱
batch_size = 10
data_loader = load_array(synthetic_data(true_w, true_b, 1000), batch_size)
print(next(iter(data_loader)))

>>>
[tensor([[-2.3627e-01,  7.1433e-01],
        [ 4.8762e-01, -5.8030e-01],
        [-3.6872e-01, -1.4212e-03],
        [-1.0333e+00, -4.0260e-01],
        [-3.9095e-01,  4.0843e-01],
        [-5.2561e-01, -1.0884e+00],
        [-9.6195e-01,  6.7750e-01],
        [-1.0069e+00, -1.5371e+00],
        [-5.5252e-01,  9.6581e-01],
        [-7.5039e-01,  7.9979e-01]]), tensor([ 6.2200,  3.2867,  2.9192, -0.9658,  4.3943, -2.0996,  3.7692, -5.5858,
         6.1784,  4.8919])]
```



——————————

#### 定义模型

实现线性回归时， 我们明确定义了模型参数变量，并编写了计算的代码，这样通过基本的线性代数运算得到输出。 但是，如果模型变得更加复杂，且当我们几乎每天都需要实现模型时，自然会想简化这个过程。 这种情况类似于为自己的博客从零开始编写网页。 做一两次是有益的，但如果每个新博客就需要工程师花一个月的时间重新开始编写网页，那并不高效。



对于标准深度学习模型，我们可以使用框架的预定义好的层。这使我们只需关注使用哪些层来构造模型，而不必关注层的实现细节。 我们首先定义一个模型变量`net`，它是一个`Sequential`类的实例。 `Sequential`类将多个层串联在一起。 当给定输入数据时，`Sequential`实例将数据传入到第一层， 然后将第一层的输出作为第二层的输入，以此类推。 在下面的例子中，我们的模型只包含一个层，因此实际上不需要`Sequential`。 但是由于以后几乎所有的模型都是多层的，在这里使用`Sequential`会让你熟悉“标准的流水线”。

上面我们使用的是单层神经网络结构，这一单层被称为***全连接层*** 因为它的每一个 输入都通过矩阵-向量乘法得到它的每个输出



在pytorch中，全连接层在linear类中定义，指的注意的是，我们将传递两个参数到nn.Linear中，**第一个指定输入特征形状，第二个指定输出特征形状，输出特征形状为单个标签**

```python
# nn是神经网络的缩写
from torch import nn

net = nn.Sequential(nn.Linear(2, 1))
```



——————————

#### 初始化模型参数

深度学习框架通常有预定义的方法来初始化参数。 在这里，我们指定每个权重参数应该从均值为0、标准差为0.01的正态分布中随机采样， 偏置参数将初始化为零。

```python
net[0].weight.data.normal_(0, 0.01) # 第一层权重设置为0到0.1的随机正态分布
net[0].bias.data.fill_(0) # 偏置为0
```

正如我们在构造`nn.Linear`时指定输入和输出尺寸一样， 现在我们能直接访问参数以设定它们的初始值。 我们通过`net[0]`选择网络中的第一个图层， 然后使用`weight.data`和`bias.data`方法访问参数。 我们还可以使用替换方法`normal_`和`fill_`来重写参数值。



——————————

#### 定义损失函数

计算均方误差使用的是MSELoss类，也称为**平方L2范数**

计算公式为：

```
def MSELoss(pred,target):
    return (pred-target)**2
```

具体实现方式

```python
loss = nn.MSELoss()
```



——————————

#### 定义优化算法

小批量随机梯度下降算法是一种优化神经网络的标准工具，Pytorch在optim模块中实现了该算法的许多变种。

当我们实例化一个SGD实例时，我们要指定优化的参数（可通过net.parameters()从我们的模型中获得）以及优化算法所需要的超参数字典。

```python
trainer = torch.optim.SGD(net.parameters(), lr=0.03)
```



——————————

#### 训练

通过深度学习框架的高级API来实现我们的模型只需要相对较少的代码。 我们不必单独分配参数、不必定义我们的损失函数，也不必手动实现小批量随机梯度下降。 当我们需要更复杂的模型时，高级API的优势将大大增加。 当我们有了所有的基本组件，训练过程代码与我们从零开始实现时所做的非常相似。

回顾一下：在每个迭代周期里，我们将完整遍历一次数据集（`train_data`）， 不停地从中获取一个小批量的输入和相应的标签。 对于每一个小批量，我们会进行以下步骤:

- 通过调用`net(X)`生成预测并计算损失`l`（前向传播）。
- 通过进行反向传播来计算梯度。
- 通过调用优化器来更新模型参数。



——————————————————————————————————————————————





## Softmax回归

### 分类问题

softmax回归与线性回归的区别是，前者是用于预测这是什么的问题，后者用于预测多少的问题，

通常，机器学习实践者用*分类*这个词来描述两个有微妙差别的问题： 1. 我们只对样本的**“硬性”**类别感兴趣，即**属于哪个类别**； 2. 我们希望得到**“软性”类别**，即得到属于每个**类别的概率**。 这两者的界限往往很模糊。其中的一个原因是：即使我们只关心硬类别，我们仍然使用软类别的模型。



首先我们从图像分类问题开始，假设我们有一个2x2的灰度图像，我们可以使用一个标量表示每个像素值，**每个图像对应着四个特征x1,x2,x3,x4**，也就是说**样本就是一张图片**，**特征就是这张图片中的像素点**

此时我们假设每个图像属于类别“猫”、“鸡”和“狗”中的一个

接下来，我们要选择如何表示标签。 我们有两个明显的选择：最直接的想法是选择x∈{1,2,3}， 其中整数分别代表狗猫鸡{狗,猫,鸡}。 这是在计算机上存储此类信息的有效方法。 如果类别间有一些自然顺序， 比如说我们试图预测婴儿儿童青少年青年人中年人老年人{婴儿,儿童,青少年,青年人,中年人,老年人}， 那么将这个问题转变为回归问题，并且保留这种格式是有意义的。

但是一般的分类问题并不与类别之间的自然顺序有关。 幸运的是，统计学家很早以前就发明了一种表示分类数据的简单方法：***独热编码*（one-hot encoding）**。 独热编码是一个向量，它的分量和类别一样多。 类别对应的分量设置为1，其他所有分量设置为0。 在我们的例子中，标签y将是一个三维向量， 其中(1,0,0)对应于“猫”、(0,1,0)对应于“鸡”、(0,0,1)对应于“狗”：

![1683796828500](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683796828500.png)

通常来说分类通常会有多个输出，并且输出的**i**是预测为**第i类的置信度**



——————————————————————————————————————————————

### 网络架构

为了估计所有可能类别的条件概率，我们需要一个有多个输出的模型，每个类别对应一个输出。 为了解决线性模型的分类问题，我们需要和输出一样多的*仿射函数*（affine function）。 每个输出对应于它自己的仿射函数。 在我们的例子中，**由于我们有4个特征和3个可能的输出类别， 我们将需要12个标量来表示权重（带下标的w）， 3个标量来表示偏置（带下标的b）**。 下面我们为每个输入计算三个*未规范化的预测*（logit）：o1、o2和o3。

![1683797077821](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683797077821.png)

——————

##### 仿射函数

仿射函数是由**1阶多项式构成的函数**，一般形式为：
$$
f(x)=Ax+b
$$
其中A为一个M x k的矩阵，x是一个k向量，b是一个m向量

仿射函数的作用是维度改变或者形状、方向改变，这个过程叫做**仿射变换**

——————

![1683797780788](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683797780788.png)



——————————

##### 归一化

归一化也称数据标准化

归一化就是将需要处理的数据经过一定的算法，将数据限定在一定的范围内，使得能更好的看出数据间的差别

*作用:*

- 1、数据映射到指定的范围内进行处理，更加便捷快速。
- 2、把有量纲表达式变成无量纲表达式，便于不同单位或量级的指标能够进行比较和加权。经过归一化后，将有量纲的数据集变成纯量，还可以达到简化计算的作用。

*常见做法：Min-Max归一化*

![1683805580715](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683805580715.png)

——————————

### 全连接层的参数开销

![1683809329294](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683809329294.png)



——————————————————————————————————————————————

### softmax运算

现在我们将优化参数以最大化观测数据的概率。 为了得到预测结果，我们将设置一个阈值，如选择具有最大概率的标签。

1）我们**通过将输入特征和权重做线性叠加得到o1,o2,o3等的线性公式**，但是此时得到的o1，o2，o3依旧不是我们想要的，因为这三个输出都依旧为未规范化的预测， 一方面，我们没有限制这些输出数字的总和为1。 另一方面，根据输入的不同，它们可以为负值。 这些违反了 [2.6节](https://zh.d2l.ai/chapter_preliminaries/probability.html#sec-prob)中所说的概率基本公理。

2）**使用softmax函数将o1，o2，o3归一化**，是其变成规范化的预测，即为0至1的范围之间，最终得出的每个y的预测值相加为1

这一步的图解为：

![1683814874089](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683814874089.png)

其中softmax函数的具体实现为：

![1683814913335](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683814913335.png)

在softmax回归中，**校准**通常指**通过调整模型参数来提高模型的预测准确率**

——————————————————————————————————————————————

#### 小批量矢量化

![1683860798821](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683860798821.png)

——————————————————————————————————————————————

#### 交叉熵损失函数

在softmax回归中，我们需要使用一个损失函数来度量预测的效果，我们将使用**最大似然估计**

![1683868080201](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1683868080201.png)

其中最小化负对数似然与交叉熵损失是相通的，可以看成是相同的

**注意**：交叉熵损失函数中的log是以e为底的

——————————

##### exp函数

高等数学中以自然常数e为底的指数函数

——————————

#### 信息熵

一般来说，交叉熵损失函数与信息熵的公式相似

![1684158853397](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1684158853397.png)

位为比特（bit）

——————————

#### softmax和交叉熵损失

交叉熵常用来衡量两个概率的区别，即两个概率之间的差距

同样的交叉熵损失也分二分类与以及多分类损失

![1684052059405](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1684052059405.png)





——————————

##### torch.squeeze(input, dim=None, out=None)

该函数用于降维，去除size为1的维度，

- 其中squeeze(0)代表若**第一维度值为1**则去除第一维度
- squeeze(1)代表若**第二维度值为1**则去除第二维度
- -1，去除最后维度值为1的维度
- 参数:
    - input (Tensor) – 输入张量
    - dim (int, optional) – 如果给定，则input只会在给定维度挤压，维度的索引（从0开始）
    - out (Tensor, optional) – 输出张量

——————————

##### zip()

zip()函数用于**将可迭代的对象**作为参数，将对象中的对应的元素**打包成一个个元组**，然后**返回由这些元组组成的列表**，

——————————

##### flatten()方法

将输入“压平”，即把多维的输入一维化，就是把高纬度的数组按照 **X轴**或 **Y轴**进行拉伸，**变成一维数组**

——————————

##### plt.subplot()函数

用于直接指定划分方式和位置进行绘图

可有两个返回值

fig-------即figure，画窗
ax-------即axex，画窗中创建的笛卡尔坐标区

一般都会先使用figure()函数过后再使用该函数

例如：

```python
# 使用plt.subplot来创建小图. plt.subplot(221)表示将整个图像窗口分为2行2列, 当前位置为1.
plt.subplot(221)
# plt.subplot(222)表示将整个图像窗口分为2行2列, 当前位置为2.
plt.subplot(222) # 第一行的右图
# plt.subplot(223)表示将整个图像窗口分为2行2列, 当前位置为3.
plt.subplot(223)
# plt.subplot(224)表示将整个图像窗口分为2行2列, 当前位置为4.
plt.subplot(224)
```

注意：其中各个参数也可以用逗号`,`分隔开。**第一个参数代表子图的行数**；**第二个参数代表该行图像的列数**； **第三个参数代表每行的第几个图像**。



matplotlib.pyplot模块提供了一个 subplots() 函数，它的使用方法和 subplot() 函数类似。其不同之处在于，**subplots() 既创建了一个包含子图区域的画布**，**又创建了一个 figure 图形对象**，而 subplot() 只是创建一个包含子图区域的画布。

subplots 的函数格式如下：

fig , ax = plt.subplots(nrows, ncols)

nrows 与 ncols 表示两个整数参数，它们指定**子图所占的行数**、**列数**。

函数的**返回值是一个元组，包括一个图形对象和所有的 axes 对象。其中 axes 对象的数量等于 nrows * ncols，且每个 axes 对象均可通过索引值访问（从1开始）**。

```python
import matplotlib.pyplot as plt
_, axes = plt.subplots(2,9,figsize=(3, 13.5))
print(_)
print(axes)

>>>
Figure(300x1350)
[[<Axes: > <Axes: > <Axes: > <Axes: > <Axes: > <Axes: > <Axes: > <Axes: >
  <Axes: >]
 [<Axes: > <Axes: > <Axes: > <Axes: > <Axes: > <Axes: > <Axes: > <Axes: >
  <Axes: >]]
```



——————————

##### plt.figure()函数

用于创建一块画布

——————————

##### enumerate()函数

1. enumerate()函数是python的内置函数
2. 对于一个可迭代的（iterable）/可遍历的对象（如列表、字符串），可利用enumerate函数同时获取对象的索引和值

这个函数一般在for中使用

```python
dict = [{"name":"小二", "age":18}, {"name":"小五", "age":24}, {"name":"小八", "age":28}]
for index,t in enumerate(dict):
    print (index, t)

>>>
0 {'name': '小二', 'age': 18}
1 {'name': '小五', 'age': 24}
2 {'name': '小八', 'age': 28}
```



——————————

##### torch.utils.data.DataLoaders

torch.utils.data.DataLoader是一个迭代器，主要是用于多线程的读取数据，并且可以实现batch和shuffle的读取

```
torch.utils.data.DataLoader(dataset, batch_size=1, shuffle=False, sampler=None,
batch_sampler=None, num_workers=0, collate_fn=None,
pin_memory=False, drop_last=False, timeout=0,
```

各个参数的介绍： 

1.dataset(Dataset): 传入的数据集
2.batch_size(int, optional): 每个batch有多少个样本
3.shuffle(bool, optional): 在每个epoch开始的时候，对数据进行重新排序
4.sampler(Sampler, optional): 自定义从数据集中取样本的策略，如果指定这个参数，那么       shuffle必须为False

5.batch_sampler(Sampler, optional): 与sampler类似，但是一次只返回一个batch的indices（索引），需要注意的是，一旦指定了这个参数，那么batch_size,shuffle,sampler,drop_last    就不能再制定了（互斥——Mutually exclusive）

6.num_workers (int, optional): 这个参数决定了有几个进程来处理data loading。0意味着所      有的数据都会被load进主进程。（默认为0）
7.collate_fn (callable, optional): 将一个list的sample组成一个mini-batch的函数

8.pin_memory (bool, optional)： 如果设置为True，那么data loader将会在返回它们之前，       将tensors拷贝到CUDA中的固定内存（CUDA pinned memory）中

9.drop_last (bool, optional): 如果设置为True：这个是对最后的未完成的batch来说的，比如     你的batch_size设置为64，而一个epoch只有100个样本，那么训练的时候后面的36个就被     扔掉了…如果为False（默认），那么会继续正常执行，只是最后的batch_size会小一点。10.timeout(numeric, optional): 如果是正数，表明等待从worker进程中收集一个batch等待的     时间，若超出设定的时间还没有收集到，那就不收集这个内容了。这个numeric应总是           大于等于0。默认为0
11.worker_init_fn (callable, optional): 每个worker初始化函数 If not None, this will be called       on each

————————————————————————————————————————————————

### 读取数据

```python
from torch.utils import data     # 执行数据集操作的包
import torchvision               # 用于处理计算机视觉的库，它提供了许多预训练模型以及加载数据集、数据增强、预处理的工具
import matplotlib.pyplot as plt
import torch

trans = torchvision.transforms.ToTensor() # 通过ToTensor实例将图像数据从PIL类型变换成32位浮点数格式，
mnist_train = torchvision.datasets.FashionMNIST("./data/", train=True, transform=trans, download=True)
mnist_test = torchvision.datasets.FashionMNIST("./data/", train=False, transform=trans, download=True)

def get_fashion_mnist_labels(labels):
    """返回Fashion-MNIST数据集的文本标签"""
    text_labels = ['t-shirt', 'trouser', 'pullover', 'dress', 'coat',
                   'sandal', 'shirt', 'sneaker', 'bag', 'ankle boot']
    return [text_labels[int(i)] for i in labels]

def show_images(imgs, rows, col, titles = None, scale=1.5):
    '''绘制图像列表'''
    fig_size = (col*scale, rows*scale)
    _, axes = plt.subplots(rows, col, figsize=fig_size)   #
    axes = axes.flatten()                                # 将多维数组压平为一维数组的形式
    for i, (ax, img) in enumerate(zip(axes, imgs)):
        if torch.is_tensor(img):
            ax.imshow(img.numpy())
        else:
            ax.imshow(img)
        ax.axes.get_xaxis().set_visible(False)  # 设置x轴标签不可见
        ax.axes.get_yaxis().set_visible(False)  # 设置y轴标签不可见
        if titles:
            ax.set_title(titles[i])
    return axes  # 返回画布

# x, y = next(iter(data.DataLoader(mnist_train, batch_size=18)))
# show_images(x.reshape(18, 28, 28), 2, 9, titles=get_fashion_mnist_labels(y))
# plt.show()

'''读取小批量'''
batch_size = 256
def get_dataloadaer_workers():
    return 4

'''这里生成一个迭代器，传入了训练数据，并且每个块（batch）中包含多少个样本，并且传入使用多少个线程进行加载数据'''

train_iter = data.DataLoader(mnist_train, batch_size, shuffle=True, num_workers=get_dataloadaer_workers())
```

![1684057231910](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1684057231910.png)



——————————————————————————————————————————————————

### softmax回归开始实现

​	transforms.Compose() 函数接收一个列表作为参数，列表中的每个元素都是一个变换函数。然后，将这些变换函数组合成一个新的变换函数，该函数会按照给定的顺序依次应用这些变换。例如，如果我们将 transforms.Resize() 和 transforms.ToTensor() 这两个变换函数组合起来，那么新的变换函数会先将图像大小调整为指定大小，然后将图像转换为 PyTorch 张量。



#### 初始化模型参数

和之前线性回归的例子一样，这里的每个样本都将用固定长度的向量表示。 原始数据集中的每个样本都是28×28的图像。 **本节将展平每个图像，把它们看作长度为784的向量**。 在后面的章节中，我们将讨论能够利用图像空间结构的特征， 但**现在我们暂时只把每个像素位置看作一个特征**。

回想一下，在softmax回归中，我们的输出与类别一样多。 因为我们的数据集有10个类别，所以网络输出维度为10。 因此，权重将构成一个784×10的矩阵， 偏置将构成一个1×10的行向量。 与线性回归一样，我们将使用正态分布初始化我们的权重`W`，偏置初始化为0。



#### 定义softmax操作

实现softmax由三个步骤组成：

1. 对每个项求幂（使用`exp`）；
2. 对每一行求和（小批量中每个样本是一行），得到每个样本的规范化常数；
3. 将每一行除以其规范化常数，确保结果的和为1。

在查看代码之前，我们回顾一下这个表达式：

![1684059570906](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1684059570906.png)



#### 定义模型







——————————————————————————————————————————————





## 多层感知机



### 隐藏层













## torch计算图

pytorch是动态图机制，所以在训练模型时候，每迭代一次都会构建一个新的计算图。而计算图其实就是代表程序中变量之间的关系。举个列子： $y=(a+b)(b+c)$ 在这个运算过程就会建立一个如下的计算图：

![img](https://pic4.zhimg.com/80/v2-8cdd08224268020e3652c42004f8bf4b_720w.webp)



在最底层，a、b、c为叶子节点，当进行前向传播运算的时候，将会自动求每个节点的梯度，即：

![img](https://pic3.zhimg.com/80/v2-d49100009fa98eb736125ca32f8d084a_720w.webp)

最后再更具每个节点的梯度进行反向传播并乘以学习率更新参数	











## 计算机视觉



### 图像处理模块

#### cv2.cvtColor()

OpenCV则提供了各种彩色模型（色彩空间）相互转换的接口，比如可以从BGR转换为HSV，HSV转换为BGR，也可以从BGR转换为灰度图。

色彩空间的转换函数cvtColor()的接口形式：

```
dst=cv2.cvtColor(src, code[, dst[, dstCn]])
```

* src为源图像对象；

* code是OpenCV中色彩空间定义的宏常量，比较常用的有COLOR_BGR2GRAY、COLOR_GRAY2BGR、COLOR_BGR2HSV、COLOR_BGR2RGB
* dstCn为目标图像的通道数，如果设置为0，会自动从源图像计算目标图像的通道数。





#### cv2.circle()

在图像中画圆圈

```
cv2.circle(img, center, radius, color, thickness=None, lineType=None, shift=None)
		   原图、中心点、  半径、   颜色、   轮廓粗细、        线类型
```





#### cv2.copyMakeBorder()

如果你想给你的图片设置边界框，就像一个相框一样的东西，你就可以使用cv2.copyMakeBorder()函数。但其在卷积操作、零填充等也得到了应用，并且可以用于一些数据增广操作。

参数

* src ： 输入的图片
* top, bottom, left, right ：相应方向上的边框宽度
* borderType：定义要添加边框的类型，它可以是以下的一种：
* cv2.BORDER_CONSTANT：添加的边界框像素值为常数（需要额外再给定一个参数）
* cv2.BORDER_REFLECT：添加的边框像素将是边界元素的镜面反射，类似于gfedcba|abcdefgh|hgfedcba
* cv2.BORDER_REFLECT_101 or cv2.BORDER_DEFAULT：和上面类似，但是有一些细微的不同，类似gfedcb|abcdefgh|gfedcba
* cv2.BORDER_REPLICATE：使用最边界的像素值代替，类似于aaaaaa|abcdefgh|hhhhhhh
* cv2.BORDER_WRAP：不知道怎么解释，直接看吧，cdefgh|abcdefgh|abcdefg
    value：如果borderType为cv2.BORDER_CONSTANT时需要填充的常数值。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200409201527237.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM2NTYwODk0,size_16,color_FFFFFF,t_70)







#### cv2.findContours()

通常，为了提高物体轮廓检测的准确率，首先要将彩色图像或者灰度图像处理成二值图像（黑白图像）或者使用Canny边缘检测算法对原图像进行一次滤波处理，这样可以在不丢失轮廓信息的前提下降低图像语义信息的复杂度，更有助于我们准确地分析物体轮廓。因此，在opencv里边，寻找轮廓的过程更像是在黑色背景中寻找白色物体。



>参数说明：
>
>thresh：图像数据（二值图像或经过Canny算法处理之后的图像）
>cv2.RETR_TREE：轮廓检索方式，还有cv2.RETR_LIST、cv2.RETR_EXTERNAL、cv2.RETR_CCOMP
>cv2.CHAIN_APPROX_SIMPLE：轮廓的估计方法，除此之外还有 cv2.CHAIN_APPROX_NONE

第二个参数指定的不同轮廓检索方法有什么区别呢？

轮廓检索方法	作用

> cv2.RETR_LIST	这是最简单的一种寻找方式，它不建立轮廓间的子属关系，也就是所有轮廓都属于同一层级
> cv2.RETR_TREE	完整建立轮廓的层级从属关系
> cv2.RETR_EXTERNAL	只寻找最高层级的轮廓
> cv2.RETR_CCOMP	把所有的轮廓只分为2个层级，不是外层的就是里层的
> 详情请参考 cv2.findContours()的轮廓层级关系.

前边说了物体轮廓是具有相同灰度值的形状的边界。它是以形状边界上的点的坐标（x,y）储存的，但是cnts里边是储存了边界上所有点的坐标吗？还是只储存了个别点的坐标？这是由第三个参数轮廓的估计方法指定的。如果传递 cv2.CHAIN_APPROX_NONE，则存储所有边界点。 但实际上我们需要所有的点吗？ 例如，您找到了一条直线的轮廓。 你需要线上的所有点来代表那条线吗？ 不，我们只需要那条线的两个端点。 这就是 cv.CHAIN_APPROX_SIMPLE 所做的。 它去除所有冗余点并压缩轮廓，从而节省内存。如图1所示。

![在这里插入图片描述](https://img-blog.csdnimg.cn/b7763891949e42748e925dff9aeaa105.png)

　　　　　　图1. 不同轮廓估计方法的效果图

cv2.findContours()返回了两个变量：**contours**, **hierarchy。**

输出变量说明：

> contours：一个包含了图像中所有轮廓的list对象。其中每一个独立的轮廓信息以边界点坐标（x,y）的形式储存在numpy数组中。
> hierarchy：一个包含4个值的数组：[Next, Previous, First Child, Parent]。
> Next：与当前轮廓处于同一层级的下一条轮廓
> Previous：与当前轮廓处于同一层级的上一条轮廓
> First Child：当前轮廓的第一条子轮廓
> Parent：当前轮廓的父轮廓
> 因为一般不使用hierarchy，所以这里不讨论轮廓的层级关系，想深入研究的朋友请移步：cv2.findContours()的轮廓层级关系.
>
>
> 原文链接：https://blog.csdn.net/Just_do_myself/article/details/124215020



#### cv2.drawContours()


计算得到图像中物体轮廓之后，我们需要将轮廓在图像中绘制出来才能更直观地体验到。这时候需要用到cv2.drawContours()方法。

* 它的第一个参数是**图像**，
* 第二个参数是**储存轮廓信息的python 列表**，
* 第三个参数是**要绘制的轮廓的索引**（在绘制单个轮廓时很有用。要绘制所有轮廓，传递 -1）
* 其余参数是**颜色**、**厚度** 等等。

该函数没有返回值

```
import cv2
import numpy as np

img = cv2.imread(r"data\dog_head\doghead.jpg")
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
gray = cv2.GaussianBlur(gray, (3, 3), 0)
canny_img = cv2.Canny(gray, 60, 180)
contours, hierarchy = cv2.findContours(canny_img, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
print(contours)

cv2.imshow("canny", canny_img)
if cv2.waitKey(0) == ord('q'):
    cv2.destroyWindow("canny")


cv2.drawContours(img, contours, -1, (0, 255, 0), 1)
cv2.imshow("binary", img)
if cv2.waitKey(0) == ord('q'):
    cv2.destroyWindow("binary")

```

![1701747777492](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1701747777492.png)





### 灰度变换



灰度线性变换是一种灰度变换，通过建立灰度映射的方式来调整图像的灰度，达到图像增强的目的，灰度映射通常使用灰度变化曲线来表示

灰度线性变换就是将图像的像素值通过指定的线性函数进行变换，以此增强或减弱图像的灰度。灰度线性变换的公式是常见的一维线性函数：
$g ( x , y ) = k ⋅ f ( x , y ) + b$



设x为原始灰度值，则变换后的灰度值y为：
$y=k⋅x+b……(0≤y≤255)$

k表示直线的斜率，即倾斜程度，b 表示线性函数在y 轴的截距。
 

| k、b取值        | 意义                                                         |
| --------------- | ------------------------------------------------------------ |
| k>1             | 增大图像的对比度，图像的像素值在变换后全部增大，整体效果被增强 |
| k = 1           | 通过调整b，实现对图像亮度的调整                              |
| 0 &lt; k &lt; 1 | 图像的对比度被削弱                                           |
| k &lt; 0        | 原来图像亮的区域变暗，原来图像暗的区域变亮                   |

http://t.csdnimg.cn/qbsXO





### 图像平滑

#### 平均滤波

原文链接：https://blog.csdn.net/haier123888/article/details/106167151/

均值滤波也称为线性滤波，其采用的主要方法为邻域平均法。均值滤波是图像处理中最常用的手段，从频率域观点来看均值滤波是一种低通[滤波器](https://so.csdn.net/so/search?q=滤波器&spm=1001.2101.3001.7020)，高频信号将会去掉，因此可以帮助**消除图像尖锐噪声，实现图像平滑，模糊等功能**。



线性滤波的基本原理是用均值代替原图像中的各个像素值，即对待处理的当前像素点（x，y），选择一个模板，该模板由其近邻的若干像素组成，求模板中所有像素的均值，再把该均值赋予当前像素点（x，y），作为处理后图像在该点上的灰度g（x，y），即g（x，y）=∑f（x，y）/m ，m为该模板中包含当前像素在内的像素总个数。

不足之处：均值滤波本身存在着固有的缺陷，即它不能很好地保护图像细节，在图像去噪的同时也破坏了图像的细节部分，从而使图像变得模糊，不能很好地去除噪声点。

均值滤波原理

​       对于二维图像，我们在图像中采取3*3的矩阵，里面有9个像素点，我们将9个像素进行排序，最后将这个矩阵的中心点赋值为这九个像素的中值。



通常情况下，我们会以该当前像素为中心，对行数和列数相等的一块区域内的所有像素点的像素取平均值。
 例如,我们可以以当前像素点的像素周围3x3区域内所有像素点的像素取平均值，也可以对周围5x5区域内所有像素点的像素值取平均值。

![在这里插入图片描述](https://img-blog.csdnimg.cn/8c7fc9693f0d4921a9af14eca72dce00.png)

图2-1  一幅图像的像素值示例

 当前像素点的位置为第5行第5列时，我们对其周围5*5区域内的像素值取平均，计算方法如下：
像素点新值=
[(197+25+106+156+159）
(149+40+107+5+71)+
(163+198+226+223+156) +
(222+37+68+193+157)+
(42+72+250+41+75)]/25 = 126

计算得到新值以后，我们将新值作为当前像素点均值滤波后的像素值。



具体均值滤波函数：**cv2.blur()**

语法格式：dst = cv2.blur(src, ksize, anchor, borderType)

* dst为返回值
* src为滤波处理前的图像
* ksize卷积核大小，卷积核的大小就是在均值处理的过程中，其领域图像的高度和宽度
* anchor是锚点，其默认值是（-1，-1），表示当前计算均值以及替换值的点位于核的中心位置，在特殊情况下可以指定不同的点来作为锚点
* borderType是边界样式，通常情况下，这个参数并不需要赋值，直接使用默认值即可

通常情况下，使用该函数的时候，都可以忽略anchor、borderType的值，直接默认即可，因此调用函数的格式应该为：**dst = cv2.blur(src, ksize)**

案例

```
# 均值滤波
import cv2
import matplotlib.pyplot as plt
img = cv2.imread(r"data\dog_head\doghead.jpg")
dst3 = cv2.blur(img, (3, 3))
dst5 = cv2.blur(img, (5, 5))
dst9 = cv2.blur(img, (9, 9))
plt.subplot(1, 3, 1)
plt.imshow(dst3)

plt.subplot(1, 3, 2)
plt.imshow(dst5)

plt.subplot(1, 3, 3)
plt.imshow(dst9)

plt.show()

```

![1701772946702](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1701772946702.png)





#### 高斯滤波

在高斯滤波中，卷积核的值不再是1。例如，一个3×3的卷积核可能如图2-1所示。
![在这里插入图片描述](https://img-blog.csdnimg.cn/31d90f66f41f4a7bbaeafb0674f12d00.png)
图2-1  高斯滤波卷积核示例



在实际计算时，使用的卷积核如图2-3中的卷积核所示。

![在这里插入图片描述](https://img-blog.csdnimg.cn/77d44d92d7c44535a5eea0e30eef9380.png)

图2-3  实际计算中的卷积核

 使用图2-3中的卷积核，针对第 4 行第 3 列位置上的像素值为 226 的像素点进行高斯滤波处理，计算方式为：
新值=(40×(1/20)+107×(2/20)+5×0.05)
+(198×0.1+226×0.4+223×0.1)
+(37×0.05+68×0.1+193×0.05)
=164

```
# 高斯滤波
import cv2
import matplotlib.pyplot as plt

img = cv2.imread(r"data\dog_head\doghead.jpg")
dst3 = cv2.GaussianBlur(img, (3, 3), 0)
dst5 = cv2.GaussianBlur(img, (5, 5), 0)
dst9 = cv2.GaussianBlur(img, (9, 9), 0)

plt.subplot(1, 3, 1)
plt.imshow(dst3)

plt.subplot(1, 3, 2)
plt.imshow(dst5)

plt.subplot(1, 3, 3)
plt.imshow(dst9)

plt.show()
```

![1701773270992](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1701773270992.png)





#### 中值滤波

中值滤波会选取数字图像或数字序列中像素点及其周围临近像素点（一共有奇数个像素点）的像素值，将这些像素值排序，然后将位于中间位置的像素值作为当前像素点的像素值，让周围的像素值接近真实值，从而消除孤立的噪声点。

 例如，针对图2-1中第4行第4列的像素点，计算它的中值滤波值。

![在这里插入图片描述](https://img-blog.csdnimg.cn/0efdd64113824d09944e12b65532483c.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Y2K5aOV5pil5rC0,size_11,color_FFFFFF,t_70,g_se,x_16)

图2-1  一幅图像的像素值示例

 将其邻域设置为3×3大小，对其3×3邻域内像素点的像素值进行排序（升序降序均可），按升序排序后得到序列值为：[66,78,90,91,93,94,95,97,101]。在该序列中，处于中心位置（也叫中心点或中值点）的值是“93”，因此用该值替换原来的像素值


中值滤波函数：cv2.medianBlur()

其语法格式如下：

​     **dst=cv2.medianBlur（src,ksize）**

​    式中：

​    ● dst是返回值，表示进行中值滤波后得到的处理结果。

​     ● src 是需要处理的图像，即源图像。它能够有任意数量的通道，并能对各个通道独立处理。图像深度应该是CV_8U、CV_16U、CV_16S、CV_32F 或者 CV_64F中的一种。

​    ● ksize 是滤波核的大小。滤波核大小是指在滤波处理过程中其邻域图像的高度和宽度。需要注意，核大小必须是比1大的奇数，比如3、5、7等。 

例程

```
# 中值滤波
import cv2

img = cv2.imread(r"data\dog_head\doghead.jpg")

dst = cv2.medianBlur(img, 3)

cv2.imshow("origin", img)            # 左图为原图
if cv2.waitKey(0) == ord("q"):
    cv2.destroyWindow("origin")

cv2.imshow("blur_img", dst)			 # 右图为原图
if cv2.waitKey(0) == ord("q"):
    cv2.destroyWindow("blur_img")
```

![1701773673462](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1701773673462.png)





#### 双边滤波

https://www.guyuehome.com/41381

双边滤波的基本思路时同时考虑将要被**滤波的像素点的空域信息和值域信息**

 双边滤波是一种非线性滤波器，可以达到保持边缘、降噪平滑的效果，和其他滤波原理一样，双边滤波也是采用加权平均的方法，用周边像素亮度值的加权平均代表某个像素的强度，所用的加权平均基于高斯滤波

特点：

1） 双边滤波在去除噪声的同时保持边缘清晰锐利非常有效

2）与其他滤波器相比，该操作速度较慢

函数定义：

```
cv2.bilateralFilter(src, d, sigmaColor, sigmaSpace, borderType = BORDER_DEFAULT)
```

* src：表示待处理的输入图像
* d：表示在过滤器件使用的每个像素邻域的直径。如果输入d非0，则sigmaSpace由d计算得出， 如果sigmaColor没输入，则sigmaColor由sigmaSpace计算得出
* sigmaColor：表示色彩空间的标准方差，一般尽可能大。较大的参数值意味着像素邻域内较远的颜色可能会混合在一起，从而产生更大面积的半相对颜色
* sigmaSpace：表示坐标空间的标准方差（像素单位），一般尽可能小。参数值越大意味着颜色猪狗相近的颜色影响越大。当d>0时，它指定邻域大小而不考虑sigmaSpace。否则，d与sigmaSpace成正比





### 仿射变换

仿射变换是一种常见的图像集合变换，包括：平移、旋转、缩放、翻转、剪切等

![1701788912130](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1701788912130.png)



![img](https://pic4.zhimg.com/80/v2-c3a501287e129177a731dc39dd17cdc7_720w.webp)

#### 图像平移

在opencv中，通过warpAffine函数实现仿射变换，格式为：

```
def warpAffine(src, M, dsize, dst=None, flags=None, borderMode=None, borderValue=None)
```

* src：输入图像
* M：运算矩阵，2行3列的，数据类型要求是float32位及以上
* dsize：运算后矩阵的大小，也就是输出图片的尺寸
* dst：输出图像
* flags：插值方法的组合，与resize函数中的插值一样，可以查看cv2.resize
* borderMode：像素外推方法，详情参考官网
* borderValue：在恒定边框的情况下使用的borderValue值；默认情况下，它是 0

各种插值方法

![1701792748021](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1701792748021.png)





#### 图像旋转

opencv中getRotationMatrix2D函数可以直接生成旋转矩阵M，而不需要计算三角函数

**getRotationMatrix2D(center, angle, scale)**

* center 旋转中心点
* angle旋转角度，单位是角度，逆时针为正方向，角度为正值代表逆时针
* scale缩放倍数，值等于1.0时表示尺寸不变
* 函数返回的时变换矩阵

`注意：该函数是负责计算转换函数M，得出M后需要调用warpAffine函数对图像进行转换`





### 边缘检测的思想与步骤

边缘检测的基本步骤：

1. 图像获取

先进行图像的获取，再根据相应的条件转化为灰度图像，进而进行分析

2. 图像滤波

由于导数计算对噪声比较敏感，必须使用滤波其来改善与噪声相关的边缘检测器的性能

3. 图像增强

增强边缘的基础是确定图像各点邻域强度的变化值，增加算法可以将邻域强度有显著变化的点突出显示出来

4. 图像检测

图像中很多点的梯度幅值变化比较大，但是并不是边缘，可以用一些方法进行测点，最简单的判断是梯度幅值阈值判据

5. 图像定位

图像边缘定位是对边缘图像处理过后得到的单像素的二值边缘图像，常使用的技术是阈值法和零交叉法



#### Roberts算子

Roberts算子是一种斜向偏差分的梯度计算方法，梯度的大小代表边缘的强度，梯度的方向与边缘走向垂直（正交）

梯度算子的定义：![G(x, y)=\sqrt{\nabla_{x} f(x, y)^{2}+\nabla_{y} f\left(x, y^{2}\right)}](https://private.codecogs.com/gif.latex?G%28x%2C%20y%29%3D%5Csqrt%7B%5Cnabla_%7Bx%7D%20f%28x%2C%20y%29%5E%7B2%7D&plus;%5Cnabla_%7By%7D%20f%5Cleft%28x%2C%20y%5E%7B2%7D%5Cright%29%7D)

为了简化计算，一般梯度算子可以近似为:

G(x,y)=|∇xf(x,y)|+|∇yf(x,y)|

由此，我们可得图像离散化（差分代替偏导）的对角线Roberts算子：

​                                                                ![\left\{\begin{array}{l}{\bigtriangledown {x} f(x, y)=f(x, y)-f(x-1, y-1)} \\ {\bigtriangledown {y} f(x, y)=f(x-1, y)-f(x, y-1)}\end{array}\right.](https://private.codecogs.com/gif.latex?%5Cleft%5C%7B%5Cbegin%7Barray%7D%7Bl%7D%7B%5Cbigtriangledown%20%7Bx%7D%20f%28x%2C%20y%29%3Df%28x%2C%20y%29-f%28x-1%2C%20y-1%29%7D%20%5C%5C%20%7B%5Cbigtriangledown%20%7By%7D%20f%28x%2C%20y%29%3Df%28x-1%2C%20y%29-f%28x%2C%20y-1%29%7D%5Cend%7Barray%7D%5Cright.)

![ââ](http://imgtec.eetrend.com/sites/imgtec.eetrend.com/files/201809/blog/17673-36662-1.png)             

**优缺点**

 从图像处理的实际效果来看，计算简单，边缘定位较准，但对噪声极敏感。适用于边缘明显且噪声较少的图像分割。

 

在python中，Roberts算子主要通过numpy定义模板，再调用OpenCV的filter2D()函数实现边缘提取，该函数是利用内核实现对图像的卷积运算

函数原型：

```
dst=cv.filter2D(src, ddepth, kernel[, dst[, anchor[, delta[, borderType]]]])
```

参数：

| 参数       | 描述                                                         |
| ---------- | ------------------------------------------------------------ |
| src        | 原图像                                                       |
| dst        | 目标图像，与原图像尺寸和通过数相同                           |
| ddepth     | 目标图像的所需深度                                           |
| kernel     | 卷积核（或相当于相关核），单通道浮点矩阵;如果要将不同的内核应用于不同的通道，请使用拆分将图像拆分为单独的颜色平面，然后单独处理它们。 |
| anchor     | 内核的锚点，指示内核中过滤点的相对位置;锚应位于内核中;默认值（-1，-1）表示锚位于内核中心。 |
| detal      | 在将它们存储在dst中之前，将可选值添加到已过滤的像素中。类似于偏置。 |
| borderType | 像素外推法，参见BorderTypes                                  |





### 图像分割



#### 基于阈值化的分割思想

利用图像灰度直方图得到分割阈值，使用一个或多个阈值将图像的灰度级别分为几个部分，这种算法假设不同目标相邻像素间灰度值相似，不同目标相邻像素间灰度有差异，反映在直方图上，**不同目标和背景对应不同的峰**，阈值选择两个峰值间的谷处，如果有多个目标，灰度直方图有多峰特性，也就有多个分割阈值

![1702102355031](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1702102355031.png)



#### 基于图像分割的方法

![1702102398275](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1702102398275.png)





#### 基于聚类的分割方法思想

**属于同一目标的像素具有较高的相似性**，如灰度值、色彩等，将数据集划分为若干组和类，并**使得同一个组内的数据对象具有较高的相似度**，而不同组中的数据对象是不相似的



常用的聚类方法

* K-means(均值聚类法)
* 模糊C均值算法
* 最大期望算法



使用聚类方法的要求：

1. 需要选定某种距离度量作为样本间的相似性度量
2. 确定某个评价聚类结果质量的准则函数
3. 给定某个初始分类，然后通过迭代算法找出使准则函数取得极值的最好聚类结果



聚类算法
![1702102789909](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1702102789909.png)

具体算法使用：https://www.zhihu.com/question/44164453





图像阈值化分割使一种传统的、最常用的图像分割方法，因其实现简单、计算量小、性能较稳定，称为图像分割中最基本和应用最广泛的分割技术

其适用于目标和背景占据不同灰度级范围的图像，在很多情况下使进行图像分析、特征提取和模式识别之前必要的图像预处理过程

![1702104545029](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1702104545029.png)



#### 固定阈值分割																

使用的函数：**cv2.threshold(src, thresh, maxval, type[,dst])->retval**

其中：

* src为输入图像

* thresh表示阈值

* maxval表示最大值，一般是255

* type表示阈值化类型

    常见的取值和含义：

    * cv2.THRESH_BINARY超过阈值部分取255，否则取0；
    * cv2.THRESH_BINARY_INV超过阈值部分取0，否则取255；
    * cv2.THRESH_TRUNC大于阈值部分设为阈值，否则不变
    * cv2.THRESH_TOZERO大于阈值部分不改变，否则设为0；
    * cv2.THRESH_TOZERO_INV大于阈值部分设置为0，小于部分不改变；
    * cv2.THRESH_OTSU自动处理，图像自适应二值化；

* 返回值为**retval（阈值）**，**dst（输出图像）**

示例程序

```
import cv2
import numpy as np
import matplotlib.pyplot as plt

img = cv2.imread(r"data\dog_head\lena.jpg")
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

ret, thres_img1 = cv2.threshold(gray, 127, 255, cv2.THRESH_BINARY)     # 超过阈值部分取255，否则为0
ret, thres_img2 = cv2.threshold(gray, 127, 255, cv2.THRESH_BINARY_INV) # 超过阈值部分取0，否则为255
ret, thres_img3 = cv2.threshold(gray, 127, 255, cv2.THRESH_TRUNC)      # 大于阈值部分设置为阈值，小于的不变
ret, thres_img4 = cv2.threshold(gray, 127, 255, cv2.THRESH_TOZERO)     # 大于阈值部分不改变，小于设置为0
ret, thres_img5 = cv2.threshold(gray, 127, 255, cv2.THRESH_TOZERO_INV) # 大于阈值部分不改变，小于阈值设为0
ret, thres_img6 = cv2.threshold(gray, 127, 255, cv2.THRESH_OTSU)       # 自适应二值化

plt.subplot(2, 3, 1)
plt.imshow(thres_img1, cmap='gray')
plt.title('cv2.THRESH_BINARY', fontdict={'size':8})

plt.subplot(2, 3, 2)
plt.imshow(thres_img2, cmap='gray')
plt.title('cv2.THRESH_BINARY_INV', fontdict={'size':8})

plt.subplot(2, 3, 3)
plt.imshow(thres_img3, cmap='gray')
plt.title('cv2.THRESH_TRUNC', fontdict={'size':8})

plt.subplot(2, 3, 4)
plt.imshow(thres_img4, cmap='gray')
plt.title('cv2.THRESH_TOZERO', fontdict={'size':8})

plt.subplot(2, 3, 5)
plt.imshow(thres_img5, cmap='gray')
plt.title('cv2.THRESH_TOZERO_INV', fontdict={'size':8})

plt.subplot(2, 3, 6)
plt.imshow(thres_img6, cmap='gray')
plt.title('cv2.THRESH_OTSU', fontdict={'size':8})

plt.show()

```

![1702107419910](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1702107419910.png)





#### 自适应阈值分割

自适应阈值分割可以根据图像不同区域亮度分布计算局部阈值，对图像各个部分进行分割，一般有采用均值、中值、高斯加权来确定阈值

在opencv中，采用adaptiveThreshold函数进行自适应阈值分割，该函数声明如下：

adaptiveThreshold(src,  maxValue, adaptiveMethod,,thresholdType, blockSize, C[, dst]) —>dst

* src：输入图像
* maxValue：像素最大值，一般为255
* adaptiveMethod：在一个邻域内计算阈值所采用的算法，有两个取值，分别为**ADAPTIVE_THRESH_MEAN_C**和**ADAPTIVE_THRESH_GAUSSIAN_C**
    * ADAPTIVE_THRESH_MEAN_C的计算方法是计算处邻域的平均值再减去double C的值
    * ADAPTIVE_THRESH_GAUSSIAN_C的计算方式是计算处邻域的高斯均值再减去参数double C的值
* thresholdType：阈值类型，只有两个取值，分别为THRESH_BINARY（二进制）和THRESH_BINARY_INV（反二进制）
* blockSize：adaptiveThreshold的计算单元是像素的邻域块，这是局部邻域大小，3、5、7等
* double C：偏移量调整量，用均值和高斯计算阈值过后，再减或加这个值就是最终阈值



### 图像金字塔

图像金字塔是由一幅图像的多个不同分辨率的子图构成的图像集合，是通过一个图像不断的降低采样率产生的，最小的图像可能仅仅有一个像素点。

![image-20211103135027005](https://img-blog.csdnimg.cn/img_convert/e04e0ea8b87b4df1919621df3cb60994.png)

通常情况下，图像金字塔的底部是待处理的高分辨率图像（原始图像），而顶部则为其降低分辨率的近似图像，向金字塔顶部移动时，图像的尺寸和分辨率都不断地降低。通常情况下，每向上移动一级，图像的宽和高都降低为原来的二分之一。



1. #### 向下采样：

 最简单的图像金字塔可以通过不断的删除图像的偶数行和偶数列得到的。例如，有一幅图像，其大小是N*N，删除其偶数行和偶数列后得到一幅(N/2)*(N/2)大小的图像。经过上述处理后，图像的大小变为原来的四分之一，不断重复该过程，就可以得到该图像的图像金字塔。

 也可以通过先对原始图像滤波，得到原始图像的近似图像，然后将近似图像的偶数行和偶数列删除以获取向下采样的结果。有多种滤波器可以选择。

领域滤波器：采用邻域平均值计算求原始图像的近似图像。该滤波器能够产生平均金字塔。

高斯滤波器：采用高斯滤波器对原始图像进行滤波，得到高斯金字塔。这是OpenCV函数cv2.pyrDown()所采用的的方式。

高斯金字塔是通过不断地使用高斯金字塔滤波、采样所产生的，其过程如下：


![image-20211103141432789](https://img-blog.csdnimg.cn/img_convert/22c3b4fb208440361b9a8220fabfa967.png)





2. #### 向上采样：

在向上采样的过程中，通常将图像的宽度和高度都变为原来的2倍。这意味着，向上采样的结果图像的大小是原始图像的4倍。因此，要在结果图像中补充大量的像素点。对新生成的像素点进行赋值的行为，称为 **插值**。该过程可以通过多种方式实现，例如最邻近插值就是使用最邻近的像素点给当前还没有值的像素点赋值。



#### 高斯金字塔

高斯金字塔再简单降采样的基础上加上了高斯滤波，将图像金字塔每层的一张图像**使用不同参数做高斯模糊**，使得金字塔的每层含有多张高斯模糊图像，将金字塔每层多张图像合称为**一组**

![1702188048985](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1702188048985.png)

![1702188066530](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1702188066530.png)

具体使用的函数为：

**pyrDown(src, dst=None, dstsize=None, borderType=None)**

* src：输入图像
* dstsize：目标图像，输出图像的大小，默认为**Size((src.cols+1)/2, (src.rows+1)/2)**
* borderType：像素外推方法
* dst：输出图像





图像向上取样是由小图像不断放大图像的过程，将图像再每个方向上扩大到原图的两倍，新增行列军用0填充，应使用与“向下采样”相同的卷积核乘以4（确保新插入的值的分布不会改变）



高斯滤波的具体操作是：用一个模板（或称卷积、掩模）扫描图像中的每一个像素，用模板确定的邻域内像素的加权平均灰度值去替代模板中心像素点的值。

  对应均值滤波和方框滤波来说，其邻域内每个像素的权重是相等的。而在高斯滤波中，会将中心点的权重值加大，远离中心点的权重值减小，在此基础上计算邻域内各个像素值不同权重的和。
**（这是由于权重的原因，当进行卷积过后，计算出来的像素值会增加卷积核的核的核权重总和倍，因此需要做归一化来确保滤波的有效性）**



![1702190167490](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1702190167490.png)



#### 拉普拉斯金字塔

拉普拉斯金字塔可以从高斯金字塔计算的来，拉普拉斯金字塔主要应用于**图像融合**，其通过计算残差图来还原原图，拉普拉斯金字塔数学定义如下

![1702193548461](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1702193548461.png)

拉普拉斯函数的原型如下：

**cv2.Laplacian(src, ddepth[, dst[, ksize[,scale[,delta[,borderType]]]]])—>dst**

参数：

* src：原图
* dst：目标图像
* ddepth：表示目标图像的深度
* ksize：表示用于计算二阶导数滤波器的孔径大小，必须为正数和奇数
* scale用于计算拉普拉斯的可选比例因子，默认情况下，不应用缩放
* delta表示结果存储在dst之前添加到结果中的可选增量值
* borderType用于决定在图像发生几何变换或者滤波操作（卷积）时边沿像素的处理方式





### 图像形态学

数学形态学：是指一系列处理图像形状特征的图像处理技术，基本思想是利用一些预先设计好的小规模结构来测量或提取图像中相应的形状或特性 

形态学处理在图像处理上的应用有：**消除噪声**、**边界提取**、**区域填充**、**连通分量提取**、**凸壳**、**细化**、**粗化**，分割出独立的图像元素或者图像中相邻的元素，求取图像中明显的极大值区域和极小值区域，以及求取图像梯度等

数学形态学是由一组形态学的代数运算子组成的，基本运算由4个：

* 膨胀（或扩张）
* 腐蚀（或侵蚀）
* 开运算
* 闭运算

利用数学形态学，我们可以实现如下的功能：

* 数学形态学滤波，去除图像中的噪点
* 连通域分割，将原来连通在一起的区域，分离为两个独立的连通域
* 连通域拼接，将两个独立的连通域拼接为一个连通域
* 提取图像轮廓
* 突出图像中的亮斑或者暗斑



#### 击中、击不中

假设由两幅图像B、X，若存在这样一个点，它即是b的元素，又是X的元素，则称B**击中**，记作B↑X

![img](https://img-blog.csdn.net/20140803162953421)

又假设有两幅图像B、X。若不存在任何一个点，它即使B





#### 腐蚀

腐蚀能够消融物体的边界，具体的腐蚀结果与图像本身和结构元的形状有关

常用的腐蚀操作是指定形状和大小的**结构元素**与二值图像进行卷积。结构元素通常是一个小的图像区域，可以是矩形、圆形、十字形等形状。

腐蚀的步骤：

（1）选择一个结构元素：结构元素是一个小的二进制矩阵，用于定义腐蚀的形状和大小。通常选择一个正方形或圆形的结构元素。

（2）将结构元素放置在图像的每一个像素上，并与之对应的区域进行逐元素比较。

（3）如果**结构元素中**的所有像素都**与相应的图像区域中的像素匹配**，则将该像素**保留**为白色（或者其他亮度）。

（4）如果结构元素中的任何一个像素与相应的图像区域中的像素**不匹配**，则将该像素设为黑色（或者其他暗度）（黑色其实就是将其腐蚀掉）。

![img](https://img-blog.csdnimg.cn/ba3da589ba9146a189448aef694acbc2.png)

##### 如何选取合适的结构元

* 根据图像的图像质量、分辨率，应用场景不同，需要尝试取不同的值
* 结构元越大，其中的1越多，腐蚀效果越强

opencv中使用腐蚀操作，我们需要新建一个核，即结构元素：

**kernel = np.ones()**

然后将核传入**erode函数**

**erorsion_img = cv2.erode(img, kernel, iterations=1)**

* img是输入的图像
* kernel是结构元
* iterations表示腐蚀操作的次数



#### 膨胀

膨胀与腐蚀恰好是一对相反的操作，膨胀将与物体接触的所有背景点合并到该物体中，是边界向外布扩张的过程，膨胀可以用来填补物体上的空洞，

图像膨胀的原理和图像腐蚀几乎一致，只不过最后赋值不同，腐蚀赋予黑色，膨胀赋予白色，当然不一定是黑色和白色，还得看你的二值图具体是哪两个值，我这是0和255，对应就是黑白。



#### 开运算

开运算等于对图像先进行腐蚀，然后进行膨胀，与腐蚀操作相比，具有可以基本保持目标原有大小不变的优点，同时开运算还能用来去除小粒噪声

![1702215152012](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1702215152012.png)



#### 闭运算

闭运算先对图像进行膨胀，然后进行腐蚀，闭运算用来填充物体内细小空洞、连接邻近物体、平滑边界，同时并不明显改变图像的面积，并消除图像内部细小的空洞

其函数为：

**opening = cv2.morphologyEx(img, cv2.MORPH_CLOSE, kernel)**









#### 计算机视觉的坐标问题

机器视觉系统有三大坐标系，分别是：1、图像（像素）坐标系，2、摄像机坐标系，3、世界坐标系。
1.图像（像素）坐标系
以图像左上角为原点建立以像素为单位的二维坐标系u-v。像素的横坐标u与纵坐标v分别是在其图像数组中所在的列数与行数。（在OpenCV中对应为x-y)

![图像坐标系](https://img-blog.csdnimg.cn/20200316132123667.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3VzdGN5cg==,size_16,color_FFFFFF,t_70)

图像坐标系和像素坐标系对同一副图的描述本质上是相同的。图像坐标系（x-y)的单位是米或毫米，是连续图像坐标或者空间坐标，以图片对角线交点O1（也称为图像的主点）作为基准原点。像素坐标系（u-v)的单位为像素（pixel），是离散图像坐标或像素坐标，原点在图片的左上角O0。

————————————————


### 卷积神经网络

![1685261663956](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1685261663956.png)

### 卷积层

卷积是卷积神经网络的核心，在图像识别里，我们提到的卷积是二维卷积，即卷积核（离散二维滤波器）与二维图像做卷积操作，简单点讲就是**卷积核**按照指定的**步长**滑动到二维图像上的所有位置，并在每个位置上与该像素点以及其领域像素点做**内积**操作。并且不同的卷积核可以提取不同的特征，通过卷积操作可以提取出图像低级到复杂的特征

![网络解析（一）：LeNet-5详解](https://img-blog.csdnimg.cn/img_convert/f993a6a934a7722b9d0d5b66552980dd.gif)

其中卷积还具有两个特征： 

- 局部连接：每个**神经元**（卷积过后的一个元素）仅与**输入神经元的一块区域**连接，这块局部区域称作感受野（receptive field），**简单点来说就是一个卷积得出的对应的元素（神经元）是与卷积核大小相同的一块区域（感受野）相关联的，这一个神经元具有整个感受野的特征**。在图像卷积操作中，即神经元在空间维度（spatial dimension，即上图示例H和W所在的平面）是局部连接，但在深度上是全部连接。对于二维图像本身而言，也是局部像素关联较强。这种局部连接保证了学习后的过滤器能够对于局部的输入特征有最强的响应。局部连接的思想，也是受启发于生物学里面的视觉系统结构，视觉皮层的神经元就是局部接受信息的。
- 权重共享：**计算同一个深度切片的神经元时采用的滤波器是共享的**。例上图中计算o[:,:,0]的每个每个神经元的滤波器均相同，都为W0，这样可以很大程度上减少参数。共享权重在一定程度上讲是有意义的，例如图片的底层边缘特征与特征在图中的具体位置无关。但是在一些场景中是无意的，比如输入的图片是人脸，眼睛和头发位于不同的位置，希望**在不同的位置学到不同的特征** 。==请注意权重只是对于同一深度切片的神经元是共享的，在卷积层，通常采用多组卷积核提取不同特征，即对应不同深度切片的特征，不同深度切片的神经元权重是不共享==，（简单点说就是要抽取的特征数等于卷积核的数量，每个特征对应的卷积核是不一样的，输出的通道数的数量也对应着特征数量）。另外，偏重对同一深度切片的所有神经元都是共享的。

通过介绍卷积计算过程及其特性，可以看出卷积是线性操作，并具有平移不变性（shift-invariant），平移不变性即在图像每个位置执行相同的操作。卷积层的局部连接和权重共享使得需要学习的参数大大减小，这样也有利于训练较大卷积神经网络。

卷积核的维度取决于输入通道数，

而卷积核的个数取决于我们想要提取的特征的个数

——————————————————



卷积的具体

实际上就是说卷积就是通过计算卷积核，卷积核就是学习得到的，用来匹配图像特征的，当图像和这个卷积核代表的特征越相似，那么这个卷积的值就越大，而感受野越大，那么也就是说和他们相关的特征就越多，类似于在浅层的时候，他可能只和纹理相关，但是后面越来越深的时候，他代表的东西可能就是有这个纹理，并且有别的特征组合到一起，这样就是一个完整的指定物品ss



### 池化层

![网络解析（一）：LeNet-5详解](https://img-blog.csdnimg.cn/img_convert/2e77be8879c71bf91c5bbe173057f5af.png)

池化是非线性下采样的一种形式，主要作用是通过减少网络的参数来减少计算量，并且能够在一定程度上控制过拟合（增加网络深度），通常在卷积层的后面会加上一个池化层。池化层包括最大池化、平均池化等。其中最大池化是用不重叠的矩形框将输入层分为不同的区域，对于每个矩形框的数取最大值作为输出层



——————————————————————————————————————————————



## ResNet

[ResNet——CNN经典网络模型详解(pytorch实现)_cnn网络模型-CSDN博客](https://blog.csdn.net/weixin_44023658/article/details/105843701)

在ResNet网络提出之前，传统的卷积神经网络都是通过将一系列卷积层与下采样层进行堆叠得到的。但是当堆叠到一定网络深度时，就会出现两个问题。

梯度消失或梯度爆炸。
退化问题(degradation problem)。
在ResNet论文中说通过数据的预处理以及在网络中使用BN（Batch Normalization）层能够解决梯度消失或者梯度爆炸问题。。但是对于退化问题（随着网络层数的加深，效果还会变差，如下图所示）并没有很好的解决办法。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429165427509.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDAyMzY1OA==,size_16,color_FFFFFF,t_70)



所以ResNet论文提出了residual结构（残差结构）来减轻退化问题。下图是使用residual结构的卷积网络，可以看到随着网络的不断加深，效果并没有变差，反而变的更好了。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429170028926.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDAyMzY1OA==,size_16,color_FFFFFF,t_70)

### **残差结构（residual）**

残差指的是什么？
其中ResNet提出了两种mapping：一种是identity mapping，指的就是下图中”弯弯的曲线”，另一种residual mapping，指的就是除了”弯弯的曲线“那部分，所以最后的输出是 y=F(x)+x

identity mapping
顾名思义，就是指本身，也就是公式中的x，而residual mapping指的是“差”，也就是y−x，所以残差指的就是F(x)部分。

下图是论文中给出的两种残差结构。左边的残差结构是针对层数较少网络，例如ResNet18层和ResNet34层网络。右边是针对网络层数较多的网络，例如ResNet101，ResNet152等。为什么深层网络要使用右侧的残差结构呢。因为，右侧的残差结构能够减少网络参数与运算量。同样输入一个channel为256的特征矩阵，如果使用左侧的残差结构需要大约1170648个参数，但如果使用右侧的残差结构只需要69632个参数。明显搭建深层网络时，使用右侧的残差结构更合适。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429170308771.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDAyMzY1OA==,size_16,color_FFFFFF,t_70)



**ResNet34**

![在这里插入图片描述](https://img-blog.csdnimg.cn/aff4f6d9579547dcadd9e59be43be95f.png)e

![在这里插入图片描述](https://img-blog.csdnimg.cn/79464093f3874be1ad65c7948f69ba15.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA54ix5ZCD6Iu55p6c55qE5rS-5aSn5pif,size_20,color_FFFFFF,t_70,g_se,x_16)

**残差F(X)的作用**：是修正恒等映射X的误差，使网络拟合的更好。
如果X足够好，则残差的参数均为0，使输出的F(X)=0;
如果X不够好，F(X)在X的基础上优化。

其中，F(X)与X相加时，shape必须相同，若F(X)的数据维数变化（如stride>1降维），则X也需要进行相应的变化（如对X做1x1的卷积）。

求F(X)残差的卷积均使用3x3conv，下采样大小降维一半。

由于恒等映射X的存在，反向传播时，梯度可以从深层直接给到浅层，避免了梯度消失与爆炸。

![在这里插入图片描述](https://img-blog.csdnimg.cn/2b61b1c9b6ba48b19058c414104242f5.png)

改进的残差块：


——————————————————————————————————————————————



### nn.Conv2d()函数

```
参数

torch.nn.Conv2d(
	in_channels, 
	out_channels, 
	kernel_size, 
	stride=1, 
	padding=0, 
	dilation=1, 
	groups=1, 
	bias=True, 
	padding_mode='zeros', 
	device=None, 
	dtype=None
)
```

in_channels：输入的通道数，RGB 图像的输入通道数为 3
out_channels：输出的通道数
kernel_size：卷积核的大小，一般我们会使用 5x5、3x3 这种左右两个数相同的卷积核，因此这种情况只需要写 kernel_size = 5这样的就行了。如果左右两个数不同，比如3x5的卷积核，那么写作kernel_size = (3, 5)，注意需要写一个 tuple，而不能写一个 list。
stride = 1：卷积核在图像窗口上每次平移的间隔，即所谓的步长。
padding：指图像填充，后面的int型常数代表填充的多少（行数、列数），默认为0。需要注意的是这里的填充包括图像的上下左右，以padding=1为例，若原始图像大小为[32, 32]，那么padding后的图像大小就变成了[34, 34]
dilation：是否采用空洞卷积，默认为1（不采用）。从中文上来讲，这个参数的意义从卷积核上的一个参数到另一个参数需要走过的距离，那当然默认是1了，毕竟不可能两个不同的参数占同一个地方吧（为0）。更形象和直观的图示可以观察Github上的Dilated convolution animations，展示了dilation=2的情况。
groups：决定了是否采用分组卷积，groups参数可以参考groups参数详解
bias：即是否要添加偏置参数作为可学习参数的一个，默认为True。
padding_mode：即padding的模式，默认采用零填充。





#### 预训练模型

预训练模型指的是已经使用大量数据进行训练的相对完整的网络，并且模型已经学习到了高级特征，，我们可以使用预训练模型以及预训练参数进行微调，使得模型重新适用于我们的需求，从而达到好的结果，而不需要重新进行训练。

**与从头开始训练的模型相比，使用迁移学习和预训练模型可以提高准确性，而无需花费太多时间来收敛**

一般来说预训练模型可以重训练，即不使用预训练的参数进行微调，而是使用自己的数据集对模型进行重训练

如果要加载预训练的模型，譬如加载到第n层，那么前n层的网络就没法改了，只能改n层以上的网络。加载完后可以采用微调 使模型对加载的参数进行梯度更新，也可以固定住，只更新n层以上的参数。







#### torchvision.transformers.ColorJitter(brightness=0, contrast=0, saturation=0,hue=0)

函数解析：
随机改变一个图像的亮度、对比度、饱和度和色调。如果图像是 tensor，那么它的 shape 为[…，1或3，H，W]，其中…表示 batch。如果图像是PIL图像，那么不支持模式 “1”、“I”、"F "和带有透明度（alpha通道）的模式。

参数：
**brightness** (类型为 float 或 tuple: float (min, max)) - 亮度的偏移程度。 brightness_factor可以是 [max(0, 1 - 					brightness), 1 + brightness]，也可以直接给出最大、最小值的范围 [min, max]，然后从中随机采					样。brightness_factor 值应该是非负数。

**contrast** (类型为 float 或 tuple: float (min, max)) - 对比度的偏移程度。 contrast_factor 可以是 [max(0, 1-					contrast), 1 + contrast]，也可以直接给出最大、最小值的范围 [min, max]，然后从中随机采样。					contrast_factor 值应该是非负数。

**saturation** (类型为 float 或 tuple: float (min, max)) - 饱和度的偏移程度。 saturation_factor 可以是 [max(0, 1 -      					saturation), 1 + saturation]，也可以直接给出最大、最小值的范围 [min, max]，然后从中随机采样。					saturation_factor 值应该是非负数。

**hue** (类型为 float 或 tuple: float (min, max)) - 色调的偏移程度。hue_factor 可以是 [-hue, hue]，也可以直接给					出最大、最小值的范围 [min, max]，然后从中随机采样，它的值应当满足 0<= hue <= 0.5 或者 -0.5<= 					min <= max <= 0.5。为了使色调偏移，输入图像的像素值必须是非负值，以便转换到 HSV 颜色空					间。因此，如果将图像归一化到一个有负值的区间，或者在使用这个函数之前使用会产生负值的插值					方法，那么它就不会起作用。





#### torch.nn.DataParallel函数

在多卡的GPU服务器上，当我们在上面跑程序的时候，当迭代次数或epoch足够大的时候，我们通常会使用**nn.DataParallel**函数来用多个GPU来加速训练，

```python
model = model.cuda() 
device_ids = [0, 1] 	# id为0和1的两块显卡
model = torch.nn.DataParallel(model, device_ids=device_ids)

```

Parameters 参数：
module即表示你定义的模型；
device_ids表示你训练的device；
output_device这个参数表示输出结果的device；

而这最后一个参数output_device一般情况下是省略不写的，那么默认就是在device_ids[0]，也就是第一块卡上，**也就解释了为什么第一块卡的显存会占用的比其他卡要更多一些**。





#### torchvision.datasets.ImageFolder

ImageFolder是一个通用的数据加载器，用于加载数据以用来进行训练神经网络dataset=torchvision.datasets.ImageFolder(
root, transform=None,
target_transform=None,
loader=datasets.folder.default_loader,
is_valid_file=None)

**参数详解：**

*root*：图片存储的根目录，即各类别文件夹所在目录的上一级目录。
*transform*：对图片进行预处理的操作（函数），原始图片作为输入，返回一个转换后的图片。
*target_transform*：对图片类别进行预处理的操作，输入为 target，输出对其的转换。 如果不传该参数，即对 *target* 不做任何转换，返回的顺序索引 0,1, 2…
*loader*：表示数据集加载方式，通常默认加载方式即可。
*is_valid_file*：获取图像文件的路径并检查该文件是否为有效文件的函数(用于检查损坏文件)

<u>返回的dataset都有以下三种属性：</u>

self.classes：用一个 list 保存类别名称
self.class_to_idx：类别对应的索引，与不做任何转换返回的 target 对应
self.imgs：保存(img-path, class) tuple的 list

```
from torchvision.datasets import ImageFolder
from torchvision import transforms

#加上transforms
normalize=transforms.Normalize(mean=[.5,.5,.5],std=[.5,.5,.5])
transform=transforms.Compose([
    transforms.RandomCrop(180),
    transforms.RandomHorizontalFlip(),
    transforms.ToTensor(), #将图片转换为Tensor,归一化至[0,1]
    normalize
])

dataset=ImageFolder('./data/train',transform=transform)
```



——————————————————————————————————————————————



#### transforms.Normalize()函数

Normalize()函数的作用式将数据转换为标准正态分布 ，也可以说是归一化，使得模型更加容易收敛

计算公式为：
 `input[channel] = (input[channel] - mean[channel]) / std[channel]`

**其中 mean 和 std 的3个值分表表示图像的3个通道**

如果数据集为3通道（RGB）的数据，则需要传入三个均值，以及三个标准差，使每个通道的数据进行归一化操作

如果是单通道的灰度图，可以写成 transforms.Normalize(mean=[0.5], std=[0.5])

我们可能会看到很多代码里面是这样的：
**==torchvision.transforms.Normalize(mean=[0.485, 0.456, 0.406], std=[0.229, 0.224, 0.225])==**
这一组值是怎么来的呢？答案就是通过数据集，提前抽样计算出来的



## BN层

[Batch Normalization（BN）超详细解析-CSDN博客](https://blog.csdn.net/weixin_44023658/article/details/105844861)

BN层简称批量归一化

Batch Normalization，简称BatchNorm或BN，翻译为“批归一化”，是神经网络中一种特殊的层，如今已是各种流行网络的标配。在原paper中，BN被建议插入在（每个）ReLU激活层前面，如下所示，
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429181809222.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDAyMzY1OA==,size_16,color_FFFFFF,t_70)

如果batch size为m，则在前向传播过程中，网络中每个节点都有m个输出，所谓的Batch Normalization，就是对该层每个节点的这m个输出进行归一化再输出.

我们在图像预处理过程中通常会对图像进行标准化处理，这样能够加速网络的收敛，

如下图所示，对于Conv1来说输入的就是满足某一分布的特征矩阵，但对于Conv2而言输入的feature map就不一定满足某一分布规律了**（注意这里所说满足某一分布规律并不是指某一个feature map的数据要满足分布规律，理论上是指整个训练样本集所对应feature map的数据要满足分布规律）**。而我们Batch Normalization的目的就是使我们的feature map满足均值为0，方差为1的分布规律。

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020042917374735.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDAyMzY1OA==,size_16,color_FFFFFF,t_70)



——————————————————————————————————————————————



#### net.named_parameters()

named_parameters函数返回一个数据**生成器**，数据生成器**返回一个将网络模型中可学习、可被更行的参数打包成一个元组然后叠加生成的列表**，因为都是可更新的参数，因此其返回的数据的require_grad属性都是True

```python
import torchvision.models as models

model = models.resnet18()
for param_tuple in model.named_parameters():
    name, param = param_tuple
    print("name = ", name)
    print("-" * 100)
    print("param_tuple = ", param_tuple)
    print("*" * 200)
    
>>>
param_tuple =  ('conv1.weight', Parameter containing:
tensor([[[[-1.4115e-05,  2.9187e-02,  2.9325e-03,  ..., -4.2247e-02,
            1.7490e-02, -4.5253e-02],
          [-2.4594e-02, -3.0836e-02,  3.8604e-02,  ...,  3.5473e-02,
           -4.7046e-03, -2.9440e-02],
          [ 2.4811e-02,  1.2679e-02,  1.0070e-02,  ..., -8.3476e-03,
            1.7960e-02, -1.7406e-02],
          ...,
          [-1.3021e-02,  2.9023e-02, -6.1800e-02,  ..., -5.2802e-02,
           -4.7817e-02, -2.2377e-02],
          [-3.8513e-03, -1.0603e-02, -3.9712e-02,  ...,  5.1941e-03,
            8.2868e-03, -8.3469e-03],
          [ 3.8993e-03,  3.2017e-02, -3.6292e-02,  ..., -2.0210e-02,
           -4.0358e-02,  1.7709e-02]],

         [[-1.0894e-03,  1.5720e-02,  7.0129e-03,  ..., -1.2024e-02,
            1.8644e-02,  1.7892e-02],
          [-2.3866e-02,  9.1136e-03,  3.5243e-02,  ..., -1.6756e-02,
            1.4441e-03,  4.7943e-02],
          [-2.0514e-03,  4.3022e-02,  2.6358e-02,  ..., -2.3662e-02,
           -7.8241e-04,  1.0167e-02],
        ...

         [[-4.6689e-02, -1.1407e-03,  1.8674e-02,  ...,  1.2649e-03,
           -2.9532e-02,  6.4535e-04],
          [ 1.4171e-03, -1.9274e-02, -8.6811e-03,  ...,  2.4428e-02,
            6.9516e-03,  4.3715e-02],
          [ 1.9982e-02,  1.3124e-02,  9.1508e-03,  ...,  2.5405e-02,
           -1.3132e-02,  4.0835e-02],
          ...,
          [-3.4174e-03,  1.8623e-02, -1.4386e-02,  ...,  1.0627e-03,
           -5.1297e-04,  2.2055e-02],
          [ 2.7333e-02,  2.4858e-02, -5.4305e-02,  ..., -1.2139e-02,
            1.7735e-03, -3.4184e-03],
          [ 1.1412e-03,  1.5794e-02, -2.0699e-02,  ..., -1.7846e-02,
            3.7425e-02, -1.6059e-02]]],
        ...,
```

它与models.parameters()的区别在于，models.parameters返回的数据为网络模型的所有参数

它与models.state_dict函数返回由所有layer_name:layer_param的键值信息存储的dict形式，并且state_dict函数返回值的require_grad 为False



——————————————————————————————————————————————



#### models.state_dict()

返回网络模型中所有的layer_name和layer_param的键值对信息，并且将其存储为dict形式，同时返回的模型参数的tensor的require_grad属性都是False，此函数通常用于保存与加载模型

```python
import torch
import torch.nn as nn
import torch.optim as optim
 
# 定义模型
class TheModelClass(nn.Module):
    def __init__(self):
        super(TheModelClass, self).__init__()
        self.conv1 = nn.Conv2d(3, 6, 5)
        self.pool = nn.MaxPool2d(2, 2)
        self.conv2 = nn.Conv2d(6, 16, 5)
        self.fc1 = nn.Linear(16 * 5 * 5, 120)
        self.fc2 = nn.Linear(120, 84)
        self.fc3 = nn.Linear(84, 10)
 
    def forward(self, x):
        x = self.pool(F.relu(self.conv1(x)))
        x = self.pool(F.relu(self.conv2(x)))
        x = x.view(-1, 16 * 5 * 5)
        x = F.relu(self.fc1(x))
        x = F.relu(self.fc2(x))
        x = self.fc3(x)
        return x
 
# 初始化模型
model = TheModelClass()
 
# 初始化优化器
optimizer = optim.SGD(model.parameters(), lr=0.001, momentum=0.9)
 
# 打印模型的状态字典
print("Model's state_dict:")
for param_tensor in model.state_dict():
    print(param_tensor, "\t", model.state_dict()[param_tensor].size())
 
# 打印优化器的状态字典
print("Optimizer's state_dict:")
for var_name in optimizer.state_dict():
    print(var_name, "\t", optimizer.state_dict()[var_name])
    
>>>
```

![img](https://img-blog.csdnimg.cn/b13c32e09a894272a193e8d29b6bb5c6.png)

从以上代码及运行结果可知，state_dict将模型的每一层映射到一个参数张量。在Python中，可以对state_dict进行保存、加载、更新、修改等操作。



```python
# 将模型保存到当前路径，名称为test_state_dict.pth
PATH = './test_state_dict.pth'
torch.save(model.state_dict(), PATH)
 
model = TheModelClass()    # 首先通过代码获取模型结构
model.load_state_dict(torch.load(PATH))   # 然后加载模型的state_dict
model.eval()
```

注意：load_state_dict()函数只接受字典对象，不可直接传入模型路径，所以需要先使用torch.load()反序列化已保存的state_dict。

另外，在使用模型做推理之前，需要调用model.eval()函数将dropout和batch normalization层设置为评估模式，否则会导致模型推理结果不一致。 

当然，除了保存state_dict，PyTorch还支持保存和加载整个模型。



——————————————————————————————————————————————



#### torch.stack()函数

==torch.stack(sequence, dim=0)==

沿一个新维度对输入张量序列进行连接，序列中所有张量应为相同形状；stack 函数返回的结果会新增一个维度，而stack（）函数指定的dim参数，就是新增维度的（下标）位置。

**sequence**：参与创建新张量的几个张量；

**dim**：新增维度的（下标）位置，当dim = -1时默认最后一个维度；

```python
import torch
a = torch.tensor([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
b = torch.tensor([[11, 22, 33], [44, 55, 66], [77, 88, 99]])
c = torch.stack([a, b], 0)
print(a)
print(b)
print(c)
 
# 输出信息：
tensor([[1, 2, 3],
        [4, 5, 6],
        [7, 8, 9]])
tensor([[11, 22, 33],
        [44, 55, 66],
        [77, 88, 99]])
tensor([[[ 1,  2,  3],
         [ 4,  5,  6],
         [ 7,  8,  9]],
 
        [[11, 22, 33],
         [44, 55, 66],
         [77, 88, 99]]])
```



————————————————————————————————————————————



#### pyplot.Rectangle函数

 在一幅图片里作出一个或多个矩形框

```
Rectangle(xy,width,heigth,angle=0,**kwargs)
参数
xy:2元组，矩形左下角坐标
width：矩形的宽度
height：矩形的高度
angle：float，可选，矩形相对于x轴逆时针旋转角度，默认0
fill：bool，可选，是否填充矩形
```

```python
import torch
import matplotlib.pyplot as plt

def bbox_to_rect(bbox, color):
    return plt.Rectangle(xy=(bbox[0][0], bbox[0][1]), width=bbox[0][2]-bbox[0][0], 					height=bbox[0][3]-bbox[0][1],fill=False, edgecolor=color, linewidth=2)
                         
boxes = [[18, 17, 69, 66]]
add = "C:\\Users\\R\\Desktop\\R\\4132.jpg"
img = plt.imread(add)
dog_img = plt.imshow(img)
dog_img.axes.add_patch(bbox_to_rect(boxes, "blue"))
plt.show()
```

![1685948732505](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1685948732505.png)



—————————————————————————————————————————————



#### torch.meshgrid()函数

torch.meshgrid()的功能是生成网格，可以用于生成坐标。函数输入两个数据类型相同的一维张量，两个输出张量的行数为第一个输出张量的元素个数，列数为第二个输入张量的元素个数

作用：从某个维度顺序依次获得各个点的x坐标值和y坐标值

```python
import torch
x_range = torch.tensor([0, 1, 2, 3, 4])
y_range = torch.tensor([0, 2, 3])
y, x = torch.meshgrid(y_range, x_range)
print(x)
print(y)
>>>
tensor([[0, 1, 2, 3, 4],
        [0, 1, 2, 3, 4],
        [0, 1, 2, 3, 4]])
tensor([[0, 0, 0, 0, 0],
        [2, 2, 2, 2, 2],
        [3, 3, 3, 3, 3]])
```

参数：

**tensors**：张量（张量列表）标量或者一维张量的列表

**str（optional）**：索引模式为”xy“或”ij“， 默认为”ij“，当选择的是”**xy**“，则第一个维度对应于第二个输入的基数(即第一个维度对应于第二个输入的行数)，第二个维度对应第一个输入的基数(即第二个维度				对应于第一个输入的列数)。 如果选择了”**ij**“， 则维度的顺序与输入的基数相同

**return**：返回与输入张量数量相同的张量



每个交叉点都是**网格点**，描述这些**网格点**的坐标的矩阵，就是**坐标矩阵**

![这里写图片描述](https://img-blog.csdn.net/20180809112934345?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xsbHh4cTE0MTU5MjY1NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

A,B,C,D,E,F是6个网格点，坐标如图，如何用矩阵形式（坐标矩阵）来批量描述这些点的坐标呢？
答案如下：
$$
x=\begin{bmatrix}
0&1&2\\
0&1&2
\end{bmatrix}
\\

y=\begin{bmatrix}
1&1&1\\
0&0&0
\end{bmatrix}
$$
这就是坐标矩阵——横坐标矩阵X XX中的每个元素，与纵坐标矩阵Y YY中对应位置元素，共同构成一个点的完整坐标。

当这种矩阵参数相当多的时候，特别是我们要生成多个锚框的中心点的时候，一个一个的去录入将会相当的浪费时间，因此我们可以使用`torch.meshgrid`函数

例如上面这个坐标矩阵我们可以这样生成

```python
import torch
a = (0, 1, 2)
b = (1, 0)
a = torch.tensor(a)
b = torch.tensor(b)
c, d = torch.meshgrid(a, b, indexing="xy")
print(c)
print(d)

>>>
tensor([[0, 1, 2],
        [0, 1, 2]])
tensor([[1, 1, 1],
        [0, 0, 0]])
```



————————————————————————————————————————————



#### numpy.repeat函数

作用：可用于重复数组中的元素

语法： numpy.repeat(a, repeats, axis=None)

- 参数：a: array_like
    输入的想要进行repeat的数组
- repeats：int or array of ints
    repeats参数应该是int类型或者是一个int数组。是对每一个元素repeat的次数。repeats将被广播去适应给`axis`的shape。
- axis: int, optional
    repeat操作进行的维度，可选，int值。如果未指定，默认情况下，会将数组展平(flattened)，然后返回一个扁平的重复后的数组。
- repeated_array : ndarray
    返回的repeat后的数组，除了在指定的`axis`维度以外，其余各维度的shape与原数组`a`一致。

```python
>>> np.repeat(3, 4)
array([3, 3, 3, 3])

# 下面这个例子中，x被展平(flattened，返回的数组也是一个扁平数组)
>>> x = np.array([[1,2],[3,4]])
>>> np.repeat(x, 2)
array([1, 1, 2, 2, 3, 3, 4, 4])

# 下面这个例子指定了axis=1，axis=1的维度上的shape值为2，
# 而只给定了3一个数字，所以进行了广播，即进行的操作实际为（3，3）
>>> np.repeat(x, 3, axis=1)
array([[1, 1, 1, 2, 2, 2],
       [3, 3, 3, 4, 4, 4]])

# 下面这个例子指定了axis=0，同时给定了repeats数组
# 其长度等于axis=0的shape值。对第一行重复1次，对第二行重复两次。       
>>> np.repeat(x, [1, 2], axis=0)
array([[1, 2],
       [3, 4],
       [3, 4]])
       
# 如果给定的repeats数组长度与axis不一致，会报错，can not broadcast
>>> y = np.array([[1,2],[3,4],[5,6],[7,8]])
>>> np.repeat(y,(3,1),axis = 0)
ValueError: operands could not be broadcast together with shape (4,) (2,)

# 如果未指定axis，默认展平，但是repeats是数组，同样会报错。
>>> np.repeat(y,(3,1))
ValueError: operands could not be broadcast together with shape (8,) (2,)

```

——————————————————————————————



#### torch.repeat

**torch.tensor.repeat()函数可以对张量进行重复扩充**

**1) 当参数只有两个时：（行的重复倍数，列的重复倍数），1表示不重复。**

**2) 当参数有三个时：（通道数的重复倍数，行的重复倍数，列的重复倍数），1表示不重复。**

**3.1 输入一维张量，参数为一个，即表示在列上面进行重复n次**

```
a = torch.randn(3)
a,a.repeat(4)

结果如下所示：
(tensor([ 0.81, -0.57,  0.10]),
 tensor([ 0.81, -0.57,  0.10,  0.81, -0.57,  0.10,  0.81, -0.57,  0.10,  0.81,
         -0.57,  0.10]))
```

**3.2 输入一维张量，参数为两个(m,n)，即表示先在列上面进行重复n次，再在行上面重复m次，输出张量为二维**

```
a = torch.randn(3)
a,a.repeat(4,2)

(tensor([ 0.06, -0.76, -0.59]),
 tensor([[ 0.06, -0.76, -0.59,  0.06, -0.76, -0.59],
         [ 0.06, -0.76, -0.59,  0.06, -0.76, -0.59],
         [ 0.06, -0.76, -0.59,  0.06, -0.76, -0.59],
         [ 0.06, -0.76, -0.59,  0.06, -0.76, -0.59]]))

```

**3.3 输入一维张量，参数为三个(b,m,n)，即表示先在列上面进行重复n次，再在行上面重复m次，最后在通道上面重复b次，输出张量为三维**

```
a = torch.randn(3)
a,a.repeat(3,4,2)

输出结果如下：
(tensor([2.25, 0.49, 1.47]),
 tensor([[[2.25, 0.49, 1.47, 2.25, 0.49, 1.47],
          [2.25, 0.49, 1.47, 2.25, 0.49, 1.47],
          [2.25, 0.49, 1.47, 2.25, 0.49, 1.47],
          [2.25, 0.49, 1.47, 2.25, 0.49, 1.47]],
 
         [[2.25, 0.49, 1.47, 2.25, 0.49, 1.47],
          [2.25, 0.49, 1.47, 2.25, 0.49, 1.47],
          [2.25, 0.49, 1.47, 2.25, 0.49, 1.47],
          [2.25, 0.49, 1.47, 2.25, 0.49, 1.47]],
 
         [[2.25, 0.49, 1.47, 2.25, 0.49, 1.47],
          [2.25, 0.49, 1.47, 2.25, 0.49, 1.47],
          [2.25, 0.49, 1.47, 2.25, 0.49, 1.47],
          [2.25, 0.49, 1.47, 2.25, 0.49, 1.47]]]))

```

**3.4 输入二维张量，参数为两个(m,n)，即表示先在列上面进行重复n次，再在行上面重复m次，输出张量为两维**（**注意参数个数必须大于等于输入张量维度个数**）

```
a = torch.randn(3,2)
a,a.repeat(4,2)

输出结果如下：
(tensor([[-0.58, -1.21],
         [-0.35,  0.68],
         [ 0.33,  0.70]]),
 tensor([[-0.58, -1.21, -0.58, -1.21],
         [-0.35,  0.68, -0.35,  0.68],
         [ 0.33,  0.70,  0.33,  0.70],
         [-0.58, -1.21, -0.58, -1.21],
         [-0.35,  0.68, -0.35,  0.68],
         [ 0.33,  0.70,  0.33,  0.70],
         [-0.58, -1.21, -0.58, -1.21],
         [-0.35,  0.68, -0.35,  0.68],
         [ 0.33,  0.70,  0.33,  0.70],
         [-0.58, -1.21, -0.58, -1.21],
         [-0.35,  0.68, -0.35,  0.68],
         [ 0.33,  0.70,  0.33,  0.70]]))

```

**3.5 输入二维张量，参数为三个(b,m,n)，即表示先在列上面进行重复n次，再在行上面重复m次，最后在通道上面重复b次，输出张量为三维。（注意输出张量维度个数为参数个数）**

```
a = torch.randn(3,2)
a,a.repeat(3,4,2)

输出结果如下：
(tensor([[-0.75,  1.20],
         [-1.50,  1.75],
         [-0.05,  0.40]]),
 tensor([[[-0.75,  1.20, -0.75,  1.20],
          [-1.50,  1.75, -1.50,  1.75],
          [-0.05,  0.40, -0.05,  0.40],
          [-0.75,  1.20, -0.75,  1.20],
          [-1.50,  1.75, -1.50,  1.75],
          [-0.05,  0.40, -0.05,  0.40],
          [-0.75,  1.20, -0.75,  1.20],
          [-1.50,  1.75, -1.50,  1.75],
          [-0.05,  0.40, -0.05,  0.40],
          [-0.75,  1.20, -0.75,  1.20],
          [-1.50,  1.75, -1.50,  1.75],
          [-0.05,  0.40, -0.05,  0.40]],
 
         [[-0.75,  1.20, -0.75,  1.20],
          [-1.50,  1.75, -1.50,  1.75],
          [-0.05,  0.40, -0.05,  0.40],
          [-0.75,  1.20, -0.75,  1.20],
          [-1.50,  1.75, -1.50,  1.75],
          [-0.05,  0.40, -0.05,  0.40],
          [-0.75,  1.20, -0.75,  1.20],
          [-1.50,  1.75, -1.50,  1.75],
          [-0.05,  0.40, -0.05,  0.40],
          [-0.75,  1.20, -0.75,  1.20],
          [-1.50,  1.75, -1.50,  1.75],
          [-0.05,  0.40, -0.05,  0.40]],
 
         [[-0.75,  1.20, -0.75,  1.20],
          [-1.50,  1.75, -1.50,  1.75],
          [-0.05,  0.40, -0.05,  0.40],
          [-0.75,  1.20, -0.75,  1.20],
          [-1.50,  1.75, -1.50,  1.75],
          [-0.05,  0.40, -0.05,  0.40],
          [-0.75,  1.20, -0.75,  1.20],
          [-1.50,  1.75, -1.50,  1.75],
          [-0.05,  0.40, -0.05,  0.40],
          [-0.75,  1.20, -0.75,  1.20],
          [-1.50,  1.75, -1.50,  1.75],
          [-0.05,  0.40, -0.05,  0.40]]]))

```







————————————————————————————————————————————



#### repeat_interleave()函数

函数原型
**torch.repeat_interleave(input, repeats, dim=None) → Tensor**

详解
重复张量的元素

输入参数：

`input` (类型：torch.Tensor)：输入张量
`repeats`（类型：int或torch.Tensor）：每个元素的重复次数。repeats参数会被广播来适应输入张量的维度
`dim`（类型：int）需要重复的维度。默认情况下，将把输入张量展平（flatten）为向量，然后将每个元素重复								repeats次，并返回重复后的张量。

例：

```python
>>> x = torch.tensor([1, 2, 3])
>>> x.repeat_interleave(2)
tensor([1, 1, 2, 2, 3, 3])
# 传入多维张量，默认`展平`
>>> y = torch.tensor([[1, 2], [3, 4]])
>>> torch.repeat_interleave(y, 2)
tensor([1, 1, 2, 2, 3, 3, 4, 4])
# 指定维度
>>> torch.repeat_interleave(y,3,0)
tensor([[1, 2],
        [1, 2],
        [1, 2],
        [3, 4],
        [3, 4],
        [3, 4]])
>>> torch.repeat_interleave(y, 3, dim=1)
tensor([[1, 1, 1, 2, 2, 2],
        [3, 3, 3, 4, 4, 4]])
# 指定不同元素重复不同次数
>>> torch.repeat_interleave(y, torch.tensor([1, 2]), dim=0)
tensor([[1, 2],
        [3, 4],
        [3, 4]])

```



————————————————————————————————————————————



#### [:, None]

对数组在保证数据不改变的情况下，追加一个新的维度

![img](https://img-blog.csdnimg.cn/20210405092220457.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTAwODczMzg=,size_16,color_FFFFFF,t_70)

None是NPnewaxis的别名，它创建一个长度为1的轴，这对于矩阵乘法等的运算是有用的

也就是建立一个新的索引维度并且新建的维度的长度为1，更简单来说就是新建一个维度并使用reshape函数

————————————————



#### [..., None]

也是在保证数据不变的情况下，追加一个新的维度，同时x[...]的效果等同于x[:]，而且x[...]还适用于任何维度，它的重要用途为对高维数据结构进行切片

![img](https://img-blog.csdnimg.cn/20210405092827403.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTAwODczMzg=,size_16,color_FFFFFF,t_70)



——————————————————————————————————————————————————



#### torch.full()函数

*torch.full(size, fill_value, *, out=None, dtype=None, layout=torch.strided, device=None, requires_grad=False)* return：Tensor

返回创建size大小的维度的张量，里面的元素全部填充为fill_value

```python
x = torch.full(size=(2,3),fill_value=5)
x

>>>
tensor([[5, 5, 5],
        [5, 5, 5]])

```



—————————————————————————————————————————————————



#### torch.nonzero()函数

==torch.nonzero(input, out=None) → LongTensor==

参数：

**input** (Tensor) – 源张量
**out** (LongTensor, optional) – 包含只索引值的结果张量

代码示例

输出张量中的每行包含输入中非零元素的索引。

```python
x = torch.tensor([0, 0, 1, 5, 8])
y = torch.nonzero(x)
print(y)
print(y.shape)
>>>
tensor([[2],
        [3],
        [4]])
torch.Size([3, 1])
```

如果输入input有n维，则输出的索引张量output的形状为 z x n, 这里 z 是输入张量input中所有非零元素的个数。

```python
x = torch.tensor([[0, 0, 1, 5],
                  [1, 5, 0, 8],
                  [2, 8, 9, 0]])
y = torch.nonzero(x)
print(y)
print(y.shape)
>>>
tensor([[0, 2],
        [0, 3],
        [1, 0],
        [1, 1],
        [1, 3],
        [2, 0],
        [2, 1],
        [2, 2]])
torch.Size([8, 2])
```



————————————————————————————————————————————



#### torch.max()函数

返回输入张量所有元素中最大的值

==torch.max(input, dim, max=**None**, max_indices=**None**) -> (Tensor, LongTensor)==

返回输入张量给定维度上每行的最大值，并同时返回每个最大值的位置索引。

参数:

- input (Tensor) – 输入张量
- dim (int) – 指定的维度
- max (Tensor, optional) – 结果张量，包含给定维度上的最大值
- max_indices (LongTensor, optional) – 结果张量，包含给定维度上每个最大值的位置索引

```python
import torch
x = torch.tensor([0, 0, 1, 5, 8])
y = torch.nonzero(x)
# print(y)
print(torch.max(x, dim=0))

>>>
torch.return_types.max(
values=tensor(8),
indices=tensor(4))
```



—————————————————————————————————————————————



### 目标检测

首先目标检测的输出将会是nxm的矩阵形式，其中n为输入图片的数量，而m则为模型预测的结果的向量，为了容易解释我们先使用一张单类别的图片进行识别。

那么我们首先会将一张图片输入到我们的模型中，然后经过卷积神经网络的预测，我们将会得到一个输出向量

这个输出向量的内容有：

==【Pc(是否包含对象的概率)， bx1, by1, bx2, by2, 对象的具体类别(这个需要使用one-hot的形式输出)】==

bx1，by1：为对象的真实边界框的左上角坐标

bx2，by2：为对象的真实边界框的右下角坐标

例如：

![1686034598013](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1686034598013.png)

我们在这张图片中只有一个对象，我们将所有类别列出来

【1（汽车），2（背景）】

所以我们的label将会是【1，0.5(图片尺寸的0.5)，0.7(图片尺寸的0.7)，真实边界框的宽度，高度，（1，0）】

因此我们的平方损失函数最终会是：

==loss(Y, y) =  (Y1 - y1)^2 + (Y2 - y2)^2 + (Y3 - y3) ^2+ ... + (Y7 - y7)^2==      **if y1 = 1**

==loss(Y, y) = (Y1 - y1)^2==                                                                                  **if y1 = 0**

**注**：实际应用中one-hot的输出可以不对其使用损失函数或是输出



——————————————————————————————————————————————



#### YOLO算法

yolo算法是机器视觉的一个高效的算法之一，它的具体做法是：

1.例如你输入的图像为100x100的，然后**在图像上放一个网格**，这个网格可以是多分辨率的，这里我们为了方便解释我们使用3x3的网格，实际中我们会用到更精细的网格

2.将图像识别或目标定位算法应用到网格中的每个格子中 

3.当图像识别算法识别到有目标图像在网格内时，取对象的中点，然后把这个对象分配给包含这个对象的格子

![1686038955556](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1686038955556.png)

4.那么包含有对象的格子其输出将会是———————————————————————————-**⬆**（这样的）

​	其余不包含对象的格子的输出将会是———————————————————————————————**⬆**

因此当我们的网格数量为3x3时，我们最终的目标输出将会是3x3x8，即对于每个格子都会有一个输出8维向量y

5.将所有格子都输入到卷积神经网络中，那么最终输出的将会是⬆（这个）

![1686039793173](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1686039793173.png)

并且其中的bx，by，bh，bw的值将会是格子尺度的比例 （bx，by的取值必须要在0~1之间）



————————————————————————————————————————————



#### 生成多个锚框

假设输入图像的高度为h， 宽度为w。我们以图像的每个像素为中心生成不同形状的锚框：``缩放比``（scale）s=（0，1]，`宽高比`r > 0 ，那么锚框的宽度以及高度分别为：
$$
hs\sqrt r 或 hs/\sqrt r
$$
**注：当我们给定中心坐标的时候，宽度以及高度已知的锚框时确定的**

要生成多个不同形状的锚框，我们设置许多缩放比取值和许多宽高比取值，当以每个像素为中心使用这些缩放比和宽高比的所有组合时，输入图像将总共有 w · h · n · m个锚框

但实际上我们只考虑包含s1和r1的组合，那么以同一个像素为中心的锚框的数量时n+m-1。对于整个图像而言，将共生成   ***wh（n+m-1）*** 个锚框



**生成思路**

1.首先我们可以获取图片的高和宽以及缩放比个数、高宽比个数

2.根据我们的缩放比个数以及高宽比个数来确定要生成多少个锚框（缩放比个数 + 高宽比个数  - 1）

3.将缩放比以及高宽比转为张量形式

4.设置偏移量，因为我们1个像素的高为1且宽为1，因此我们选择的偏移量中心为0.5

5.设置我们的图片的缩放比，使得模型收敛更快，并且能够很好的替代点的坐标值

6.根据我们的图片缩放比设置我们的中心点横纵坐标值，并且生成中心点的横纵坐标矩阵，并且对坐标矩阵中的所有横纵坐标元素根据上一步设置好的图片缩放比归一化处理，

7.根据公式计算出锚框的所有宽与高的组合

8.根据所有宽与高的组合计算出所有锚框的半宽以及半高，并将其叠加复制，使其的维度到达2042040x4

9.将所有的中点的坐标矩阵进行叠加重复复制，使其的维度与半宽半高的维度相同

10.将所有中点坐标以及半高半宽的矩阵进行相加，进而能够计算出所有锚框的左上坐标以及右下坐标



过程问题：

1）转置叠加过后如何保证每个点的横坐标纵坐标都有对应的半高以及半宽呢

答：由于我们使用了torch.stack函数进行叠加并使用了repeat重复行上的数据，而列数保持左上x，左上y，右下x，右下y的形式建立y的维数为4的张量，并且由于中心点和高宽都复制了高宽以及中心点的所有可能次数，因此每个锚框的高宽都会被计算到，因此我们可以保证每个中心点能够有对应的多尺度锚框



——————————————————————————————————————————————



#### 交并比（IOU）

![1686801801002](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1686801801002.png)



——————————————————————————————————————————————



#### 将真实边界框分配给锚框

![1686801880120](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1686801880120.png)

简单点说就是将最大交并比的锚框分配给真实边界框来进行拟合真实边界框



**代码实现思路：**





——————————————————————————————————————————————



#### torch.clamp()方法

torch.clamp(inp, min, max)

torch.clamp方法将所有输入元素限制在[min, max]范围内，并返回结果张量，如果输入的元素小于min，则将元素重新赋值为0， 如果输入的元素大于max， 则将元素重新赋值为最大的那个值

**参数**

- **inp:**这是输入张量。
- **min:**指定元素最小的范围数
- **max:**指定元素最大的范围数
- **out:**输出张量。

```
import torch
a = torch.arange(-1, 3).clamp(min=0)
print(a)
a = torch.arange(-1, 3).clamp(max=1)
print(a)

>>>
tensor([0, 0, 1, 2])
tensor([-1,  0,  1,  1])
```





——————————————————————————————————————————————



#### torch.full()函数

`torch.full(size, fill_value, *, out=None, dtype=None, layout=torch.strided, device=None, requires_grad=False) → Tensor`

返回创建size大小维度的张量，里面的元素全部填充为fill_value



例：

```
x = torch.full(size=(2,3),fill_value=5)
x

输出结果如下：
tensor([[5, 5, 5],
        [5, 5, 5]])

```



—————————————————————————————————————————————



#### transforms.ToTensor

transforms.ToTensor()函数的作用是将原始的PIL Image格式或者numpy.array格式的数据格式化为可被pytorch快速处理张量类型

官方译文为：

（1）将 PIL Image 或 numpy.ndarray 转为 tensor

（2）如果 PIL Image 属于 (L, LA, P, I, F, RGB, YCbCr, RGBA, CMYK, 1) 中的一种图像类型，或者 numpy.ndarray 格式数据类型是 np.uint8 ，则将 [0, 255] 的数据转为 [0.0, 1.0] ，也就是说将所有数据除以 255 进行归一化。

（3）将 HWC 的图像格式转为 CHW 的 tensor 格式。CNN训练时需要的数据格式是[N,C,N,W]，也就是说经过 ToTensor() 处理的图像可以直接输入到CNN网络中，不需要再进行reshape。






—————————————————————————————————————————————



#### torch.permute函数

torch.permute函数是pytorch中一个函数，用于对张量的维度进行重新排序，它的作用类似于numpy中的transpose函数

格式：

==torch.permute(input, dims) --→ Tensor==

返回原始张量输入的视图，并对其维度进行重新排序

Parameters:

input(Tensor)：输入张量

dims(python的数据类型为int的tuple)：所需的维度排序

```
x = torch.randn(2, 3, 5)
x.size()
>>>torch.size([2, 3, 4])

torch.permute(x, (2, 0, 1)).size()
>>>torch.size([5, 2, 3])
```

当我们进行维度变化的时候，我们的数据也会发生变化，具体的变化为，**两个交换的维度的值进行转置**，例如：

```python
import torch
a = torch.arange(24).reshape(2, 3, 4)
print(a)
a = a.permute(1, 2, 0)
print(a)
print(a.shape)

>>>
tensor([[[ 0,  1,  2,  3],
         [ 4,  5,  6,  7],
         [ 8,  9, 10, 11]],

        [[12, 13, 14, 15],
         [16, 17, 18, 19],
         [20, 21, 22, 23]]])
tensor([[[ 0, 12],
         [ 1, 13],
         [ 2, 14],
         [ 3, 15]],

        [[ 4, 16],
         [ 5, 17],
         [ 6, 18],
         [ 7, 19]],

        [[ 8, 20],
         [ 9, 21],
         [10, 22],
         [11, 23]]])
torch.Size([3, 4, 2])
```

在这里，我们对维度进行变换，则先对块的维度和行的维度进行转置，然后在对列和行的维度进行转置



————————————————————————————————————————————



#### torch.flatten函数

通过将输入重塑为一维张量来展平输入。如果传递start_dim或end_dim，则仅展平以start_dim开头和以end_dim结尾的标注。输入中元素的顺序不变。

**注**：当输入的张量为零维张量的时候将会将张量展平并且返回一维视图

Parameters:

- **input** ([*Tensor*](https://pytorch.org/docs/stable/tensors.html#torch.Tensor)) – the input tensor.
- **start_dim** ([*int*](https://docs.python.org/3/library/functions.html#int)) – the first dim to flatten  （第一个展平的维度）
- **end_dim** ([*int*](https://docs.python.org/3/library/functions.html#int)) – the last dim to flatten    （最后一个要展平的维度）

```python
import torch
t = torch.tensor([[[1, 2], [3, 4]], [[5, 6], [7, 8]]])
print(t.shape)
t = torch.flatten(t, start_dim=1)
print(t)

>>>
torch.Size([2, 2, 2])
tensor([[1, 2, 3, 4],
        [5, 6, 7, 8]])
```



——————————————————————————————————————————————



#### pandas.iterrows()函数

df.iterrows()生成一个可迭代对象，将DataFrame的一行作为（索引，行数据）组成的Series数据对进行迭代，

在for语句中需要两个变量来承接数据：一个为**索引变量**（即使索引在迭代中不会使用），另一个为**数据变量**

df.iterrows()是最常用、最方便的按行迭代方法

```python
import pandas as pd
import torch
import torchvision
import os
def read_data_bananas(is_train=True):
    """读取香蕉检测数据集中的图像和标签"""
    data_dir = d2l.download_extract("banana-detection")
    csv_frame = os.path.join(data_dir, "bananas_train" if is_train else "bananas_val", "label.csv")
    csv_data = pd.read_csv(csv_frame)
    csv_data = csv_data.set_index("img_name")
    images, targets = [], []
    for img_name, target in csv_data.iterrows():   # 对数据转换为可迭代对象然后循环遍历
        images.append(torchvision.io.read_image(
            os.path.join(data_dir, "bananas_train" if is_train else "bananas_val", "images", f"{img_name}")
        ))
        targets.append(list(target))
    return images, torch.tensor(targets).unsqueeze(1) / 256
```



——————————————————————————————————————————————



#### torch.unsqueeze()函数

unsqueeze()函数起升维的作用，参数dim表示在哪个地方加一个维度，并且升维的地方的维数大小为1

**注意dim范围在:[-input.dim() - 1, input.dim() + 1]之间，比如输入input是一维，则dim=0时数据为行方向扩，dim=1时为列方向扩，再大错误。**

![torch.unsqueeze()](https://img-blog.csdnimg.cn/1395dfd12df1404ba69942926beaff5d.png)

```python
x = torch.tensor([1, 2, 3, 4])
y = torch.unsqueeze(x, 0)#在第0维扩展，第0维大小为1
y,y.shape

输出结果如下：
(tensor([[1, 2, 3, 4]]), torch.Size([1, 4]))
```



——————————————————————————————————————————————



#### Matplotlib.axes.Axes.add_patch函数

为`axes`添加补丁，返回补丁，该函数一般用于在坐标系上添加各种形状的图形。它接收一个matplotlib.patches.Patch对象作为参数，用于指定要添加的图形

例：

```python
import matplotlib.pyplot as plt
import matplotlib.patches as patches

# 创建一个图形对象
fig, ax = plt.subplots()

# 创建一个矩形对象
rect = patches.Rectangle((0.1, 0.1), 0.5, 0.5, linewidth=1, edgecolor='r', facecolor='none')

# 将矩形对象添加到坐标系中
ax.add_patch(rect)

# 设置坐标轴范围
ax.set_xlim(0, 1)
ax.set_ylim(0, 1)

# 显示图形
plt.show()

```







——————————————————————————————————————————————



#### getattr()函数

getattr()函数用于返回一个对象属性值

==getattr(object, name[, default])==

- object -- 对象。
- name -- 字符串，对象属性。
- default -- 默认返回值，如果不提供该参数，在没有对应属性时，将触发 AttributeError。

返回值：返回对象属性值。

```python
class Demo(object):
    def __init__(self):
        self.name = '张三'
        self.age = '25'
 
    def first(self):
        print("这是 first 方法")
        return "one"
 
    def second(self):
        print("这是 second 方法")
 
 
a = Demo()
# 如果a对象中有属性name则打印self.name的值，否则打印'non-existent'
print(getattr(a, 'name', 'non-existent'))
print("*" * 100)
 
# 如果a对象中有属性age则打印self.age的值，否则打印'non-existent'
print(getattr(a, 'age', 'non-existent'))
print("*" * 100)
 
# 如果有方法first，打印其地址，否则打印default
print(getattr(a, 'first', 'default'))
print("*" * 100)
 
# 如果有方法first，运行函数并打印返回值，否则，打印default
print(getattr(a, 'first', 'default')())
print("*" * 100)
 
# 如果有方法second，运行函数并打印None否则打印default
print(getattr(a, 'second', 'default')())
```

![img](https://img-blog.csdnimg.cn/e5b2bfb984e041a4ab76b3089f26aba3.png)



——————————————————————————————————————————————



#### setattr()函数

setattr()函数用于设置属性值，该属性不一定是存在的

setattr()语法

```
setattr(object, name, value)
```

- object -- 对象。
- name -- 字符串，对象属性。
- value -- 属性值。

```python
>>>class A(object):
...     bar = 1
... 
>>> a = A()
>>> getattr(a, 'bar')          # 获取属性 bar 值
1
>>> setattr(a, 'bar', 5)       # 设置属性 bar 值
>>> a.bar
5

>>>class A():
...     name = "runoob"
... 
>>> a = A()
>>> setattr(a, "age", 28)
>>> print(a.age)
28

```



——————————————————————————————————————————————



### 多尺度目标检测

在目标检测任务中，被检测的目标大小是不确定的，每个目标的大小有大有小，并且如果被测物品尺度相差过大会导致模型的精度降低。

物体检测领域中各个模型的骨干网络，无外乎不是使用多层卷积逐步提取图像深层信息，生成多层特征图，并基于深层特征图做定位、分类等进一步处理。

在这“由浅到深”的特征提取过程中，**浅层的特征**(指靠近输入的特征)具有较高的分辨率，可以携带丰富的集合细节信息，但感受野很小而且缺乏语义信息，简单点说就是很难描述一个特征，而相反的是深层的特征（指靠近输出层的特征）具有较大的感受野以及丰富的语义信息，但分辨率不高，难以携带几何信息。

![img](https://pic1.zhimg.com/80/v2-0ddb6bf61bd7ed49d2a20aa8b93bd9f0_720w.webp)

而使用图像金字塔就能很好的解决“被测物体尺度变化幅度大导致模型精度降低”的问题，将一张图片处理成图片金字塔后，随着金字塔层数的变化，**单个被测物体也会生成由大到小的多种尺度**。在将这些不同尺度的图片传入模型后，即使模型只擅长对某一尺度范围内的物体进行识别，不论被测物体大或小，总能在金字塔的某一层中被缩放至模型擅长处理的尺度范围内。

——————————————



#### SSD单发多框检测模型

这里可以理解成图片被**卷积层处理**然后获得包含各种特征信息的**不同尺度**（简单理解为大小）的**图片**（特征图），然后在经过对以这些特征图的每个神经元为中心，并使用指定的缩放比和高宽比来画出锚框然后标注锚框的类别等信息，通过这些类别信息等作为依据，对所有不相干的锚框做抑制，使得锚框能够大概框到目标，最后通过损失函数对锚框的位置进行调整（做偏移）以及标注的类别预测做真实近视，得到通过训练来使得锚框以及类别标注近视真实值。

![img](https://img-blog.csdnimg.cn/b08af281b61e4be1a6b6321ad74ff9cc.png)

例如这张图片，我们假设我们生成的特征图为4x4的，因此我们使用特征图的神经元来做锚框的中点然后通过不同缩放比和高宽比来画出其锚框

![img](https://img-blog.csdnimg.cn/d2879573a2234e259df53d42a2f8b15c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA55G-5oCA6L2p,size_15,color_FFFFFF,t_70,g_se,x_16)



——————————————



#### selective search算法

选择性算法与普通的穷举滑动窗口算法不同，其使用的是**候选区域算法**并创建目标检测的**感兴趣区域**（ROI）

**简单点来说就是从图片中找出物体可能存在的区域**

**选择性搜索的思想**

1.使用一种图像分割手段，将图像分割成许多个小区域（1k~2k）

2.查看现有的小区域，根据小区域中图像的相似度（颜色，纹理，大小，形状交叠）来进行合并相似度最高的相邻的两个区域，重复直到整张图象合并成一个区域位置

3.输出所有曾经存在过的区域，即候选区域



——————————————



#### 候选区域算法

用分割不同区域的办法来识别潜在的物体，在分割的时候，我们要合并那些在某些方面（如颜色、纹理）类似的小区域。相比于滑动窗口法在不同位置和大小的穷举，候选区域算法将像素分配到少数的分割区域中。所以最终候选区域算法产生的区域将会少很多。

**召回率**：指在所有正样本中，被正确预测为正样本的比例（召回率越高越好）



——————————————



## RCNN

RCNN，全名局域卷积神经网络，RCNN将CNN带到了目标识别的领域，也就是说，RCNN不仅需要进行类别预测，还要对目标的位置进行预测

R-CNN首先从输出图像中抽取若干个（2000）个左右的**提议区域**（锚框也是一种提议方式），并且标注这个区域的类别和边界框（如偏移量），然后使用卷积神经网络对每个提议区域进行前向传播以提取提议区域的**特征**，然后我们使用每个提议区的特征来**预测类别**和**边界框**![1686211961289](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1686211961289.png)

以上是R-CNN的具体结构

而R-CNN具体的工作包含四个步骤：

1.对输入图像使用**选择性搜索**（选取目标可能出现的区域）来选取多个高质量的**提议区域**， 这些提议区域通常是在多个尺度下选取的，并且具有不同的**形状**和**大小**，每个提议区域都将标注类别和真实边界框

2.选择一个预训练的卷积神经网络，并将其在输出层之前截断，使用**兴趣区域池化层**将每个提议区域变形成网络所需要的输出尺寸，并通过**前向传播输出提取的提议区域的特征**

3.将**每个提议区域的特征连同其标注的类别**作为**一个样本**，训练多个支持向量机对目标进行分类，其中每个支持向量机用来判断样本是否属于一个类别

4.将每个提议区的特征连同其标注的边界框作为一个样本，训练线性回归模型来预测真实的预测边界框

而具体的R-CNN使用SVM来对类别分类

​							使用线性回归模型进行预测框偏移





——————————————



#### 感兴趣区域

有时，我们只对一幅图像中的部分区域感兴趣，而原图像又非常大，如果带着非感兴趣区域来进行处理的或者进行识别目标，这可能会使得特征识别不准确，同时我们的程序的内存也会有很大的负担，因此，我们希望从原始图像中**截取部分图像**后再进行处理，我们将这个区域称作**感兴趣区域**



——————————————



#### 兴趣区域（ROI pooling）池化层

给定一个锚框，均匀分割成nxm块，输出每块里的最大值

![1686210758153](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1686210758153.png)

例如上图中，我们的感兴趣区域为3x3，而我们需要做一个2x2的**ROI pooling**（最大感兴趣区域池化）

也就是说我们将这个感兴趣区域按照普通池化层那样，将感兴趣区域分为2x2个块，然后取每个块中的最大值，最后得到2x2的ROI pooling

其中分成的四个快为：

1.【0，1，4，5】

2.【2，6，0，0】

3.【8，9，0，0】

4.【10，0，0，0】

**注：**当感兴趣区域无法被兴趣区域池化层完整均分的时候，可以想象成需要对不足够的区域块里面**补零**，并且感兴趣区域内的特征不能重复被划分到两个不同的块中



——————————————



#### Fast RCNN

Fast-RCNN的具体做法：

先进行卷积提取特征，然后再使用ss算法进行锚框对目标的位置进行提取，然后锚框映射到卷积生成的特征图中，然后进行感兴趣池化，然后再使用池化提取每个锚框的特征

![1686759502866](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1686759502866.png)





—————————————



#### Mask R—CNN

 Mask R-CNN是基于Faster R-CNN改进而来的，具体来说Mask R-CNN将**兴趣区域汇聚层**替换为了**兴趣区域对齐层**，并使用**双线性插值法**来保留特征图上的空间信息

首先我们要对图像进行像素级的标注处理，而mask R-CNN则能有效的利用这些标注信息进一步提升目标检测的精确度

但在对图像边缘进行标注时，难免会出现像素丢失出现锯齿化，因此我们可以使用双线性插值法来让目标边缘的特征信息得以保存，

##### 双线性插值：

首先我们假设目标图像的数指定像素（2，1），然后附近由数据缺失，但是我们并不知道图像的像素值具体的函数f（x），因此我们假设使用线性的方式来进行生成对应的y值，

![这里写图片描述](https://img-blog.csdn.net/20170324224836233?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveGJpbndvcmxk/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

假如我们想得到未知函数 f 在点 P = (x, y) 的值，假设我们已知函数 f 在 Q11 = (x1, y1)、Q12 = (x1, y2), Q21 = (x2, y1) 以及 Q22 = (x2, y2) 四个点的值。最常见的情况，f就是一个像素点的像素值。首先在 x 方向进行线性插值，得到

![这里写图片描述](https://img-blog.csdn.net/20170324225038843?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveGJpbndvcmxk/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

![这里写图片描述](https://img-blog.csdn.net/20170324225112469?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveGJpbndvcmxk/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


然后在 y 方向进行线性插值，得到

![这里写图片描述](https://img-blog.csdn.net/20170324225141734?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveGJpbndvcmxk/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

综合起来最后**p点的值**就是双线性插值最后的结果：

![这里写图片描述](https://img-blog.csdn.net/20170324225222878?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveGJpbndvcmxk/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

![这里写图片描述](https://img-blog.csdn.net/20170324225231128?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveGJpbndvcmxk/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

简单点来说也可以将图画成这样进行理解

![1686282370926](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1686282370926.png)





————————————————



#### 语义分割

将目标的每一个像素分配给指定的类别

![1686295208805](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1686295208805.png)



—————————————————



#### 实例分割

不仅将图片中的每个像素分类给对应的类别同时还将像素分配给对应的实例对象

![1686295286129](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1686295286129.png)



————————————————



#### **torchvision.transforms.functional.crop(img,i,j,h,w)**

剪裁给定的PIL图片
参数：

- img(PIL图片)——被剪裁的图片
- （i, j) ——左上角图片坐标
- (h,w)——剪裁的图片的高和宽
    returns: 返回剪彩的图片



————————————————



#### torchvision.transforms.RandomCrop.get_params(feature_img, out_size)

用于获取对图像进行裁剪的随机参数

参数：

**feature_img：**要进行裁剪的图片

**out_size:**  裁剪过后的尺寸

**return：**裁剪过后图像的中点坐标以及裁剪的高宽



———————————————



#### \_\_getitem\_\_方法

在Python中，__getitem__函数是一个特殊的方法，用于实现索引操作符[]。它可以让对象像列表或字典一样被索引。

其常见的写法有：

形式一： __getitem__(self, index) 一般用来迭代序列(常见序列如：列表、元组、字符串)，或者求序列中的索引为 index 处的值。
形式二： __getitem__(self, key) 一般用来迭代映射(常见映射如：字典)，或者求映射中的键为 key 出的值。

**该方法返回与指定索引（针对序列）或键（针对映射）相关联的值，使用 对象[index] 或者 对象[key] 将自动调用该方法。**

- 对序列来说，索引应该是0~（n-1）的整数，其中n为序列的长度，一般写成 __getitem__(self, index)
    对于映射来说，假如键就是字典中的键，一般写成__getitem__(self, key)
- 如果在类中定义了__getitem__()方法，那么它的实例对象（假设为P）就可以这样P[index]取值或者这样P[key]取值。当实例对象做P[index/key]运算时，就会调用类中的__getitem__()方法。

​        



```python
class DataTest:
    def __init__(self,id,address):
        self.id=id
        self.address=address
        self.d={self.id:1,
                self.address:"192.168.1.1"
                }
	def __getitem__(self,key):
    	return "hello"
data=DataTest(1,"192.168.2.11")
print data[2]	# 会自动调用 __getitem__方法

结果为：
hello
```



```python
class Tag:
    def __init__(self):
        self.change={'python':'This is python'}
def __getitem__(self, item):
    print('这个方法被调用')
    return self.change[item]
a=Tag()
print(a['python'])

结果为：
This is python
```

**_getitem__方法，可以让对象实现迭代功能**

Python的魔法方法__getitem__ 可以让对象实现迭代功能，这样就可以使用 for…in… 来迭代该对象了

```python
class Animal:
    def __init__(self, animal_list):
        self.animals_name = animal_list
        self.other = 'hello, world'

animals = Animal(["dog","cat","fish"])
for animal in animals:
    print(animal)

```

在用 for…in… 迭代对象时，如果对象没有实现 __iter__ __next__ 迭代器协议，Python的解释器就会去寻找__getitem__ 来迭代对象，如果连__getitem__ 都没有定义，这解释器就会报对象不是迭代器的错误：

TypeError: 'Animal' object is not iterable




———————————————



#### nn.ConvTransposed2d()转置卷积函数





———————————————



#### Momentum梯度下降算法

在普通的梯度下降法中，当梯度下降的过程中不断的震荡，那么我们的损失函数可能难以收敛，并且无法使用大的学习率 

![1686473382020](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1686473382020.png)



———————————————





#### 马尔可夫过程（State + Probability）

**马尔可夫过程** = **状态** + **状态转移概率**



##### 马尔可夫性质

在St这个事件发生的情况下，又发生了St+1事件的概率等于在S1..St这些事件发生的情况下，St+1							发生的概率
$$
P(S_t+_1|S_t) = P(S_t+_1|S_1, ...,S_t)
$$
这种性质也可以称之为无后效性，也就是说，**当前的状态只由上一个状态所决定**，而不由之前的任何一个状态决定

由下图可以理解，**虽然当前状态不是由上一个状态所决定的，但当前状态一定会包含上个状态所具有的所有信息**

![1687668564826](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1687668564826.png)



##### 状态转移概率

![1687669197846](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1687669197846.png)

​                                           ⬆                                                                                                        ⬆

​								  转移状态表                                                                                     状态转移矩阵

状态转移概率指的是各种状态转移的概率，如上图中的例子可以看出，如果当前的天气是晴天，那么第二天的天气可能是晴天的可能性为0.8，以此类推，这就是状态转移概率

晴雨天气的变化就对应着状体的转移，而晴雨状态转换的可能性就是状态转移概率



——————————————————————————————



#### 隐马尔可夫模型























——————————————————————————————



#### torch.einsum



——————————————————————————————







## 机器学习

### 遗传算法

**算法概念：**

概念1：基因和染色体

在遗传算法中，我们首先需要将要解决的问题映射成一个数学问题，也就是所谓的“数学建模”，那么这个问题的一个可行解即被称为一条“染色体”。一个可行解一般由多个元素构成，那么这每一个元素就被称为染色体上的一个“基因”。

比如说，对于如下函数而言，[1,2,3]、[1,3,2]、[3,2,1]均是这个函数的可行解（代进去成立即为可行解），那么这些可行解在遗传算法中均被称为染色体。

> 3x+4y+5z<100

这些可行解一共有三个元素构成，那么在遗传算法中，每个元素就被称为组成染色体的一个基因。



概念2：适应度函数

在自然界中，似乎存在着一个上帝，它能够选择出每一代中比较优良的个体，而淘汰一些环境适应度较差的个人。那么在遗传算法中，如何衡量染色体的优劣呢？这就是由适应度函数完成的。适应度函数在遗传算法中扮演者这个“上帝”的角色。

遗传算法在运行的过程中会进行N次迭代，每次迭代都会生成若干条染色体。适应度函数会给本次迭代中生成的所有染色体打个分，来评判这些染色体的适应度，然后将适应度较低的染色体淘汰掉，只保留适应度较高的染色体，从而经过若干次迭代后染色体的质量将越来越优良。



概念3：交叉

遗传算法每一次迭代都会生成N条染色体，在遗传算法中，这每一次迭代就被称为一次“进化”。那么，每次进化新生成的染色体是如何而来的呢？——答案就是“交叉”，你可以把它理解为交配。

交叉的过程需要从上一代的染色体中寻找两条染色体，一条是爸爸，一条是妈妈。然后将这两条染色体的某一个位置切断，并拼接在一起，从而生成一条新的染色体。这条新染色体上即包含了一定数量的爸爸的基因，也包含了一定数量的妈妈的基因。

![img](https://pic1.zhimg.com/80/v2-fce070a5c04f4abf650dbf4cd03876f8_1440w.webp)

那么，如何从上一代染色体中选出爸爸和妈妈的基因呢？这不是随机选择的，一般是通过轮盘赌算法完成。

在每完成一次进化后，都要计算每一条染色体的适应度，然后采用如下公式计算每一条染色体的适应度概率。那么在进行交叉过程时，就需要根据这个概率来选择父母染色体。适应度比较大的染色体被选中的概率就越高。这也就是为什么遗传算法能保留优良基因的原因。

> 染色体i被选择的概率 = 染色体i的适应度 / 所有染色体的适应度之和

​	

概念4：变异

交叉能保证每次进化留下优良的基因，但它仅仅是对原有的结果集进行选择，基因还是那么几个，只不过交换了他们的组合顺序。这只能保证经过N次进化后，计算结果更接近于局部最优解，而永远没办法达到全局最优解，为了解决这一个问题，我们需要引入变异。

变异很好理解。当我们通过交叉生成了一条新的染色体后，需要在新染色体上随机选择若干个基因，然后随机修改基因的值，从而给现有的染色体引入了新的基因，突破了当前搜索的限制，更有利于算法寻找到全局最优解。



概念5：复制

每次进化中，为了保留上一代优良的染色体，需要将上一代中适应度最高的几条染色体直接原封不动地复制给下一代。

假设每次进化都需生成N条染色体，那么每次进化中，通过交叉方式需要生成N-M条染色体，剩余的M条染色体通过复制上一代适应度最高的M条染色体而来。



遗传算法的流程

- 在算法初始阶段，它会随机生成一组可行解，也就是第一代染色体。
- 然后通过**基因交换**或是**基因突变**来生成新的染色体
- 然后采用适应度函数分别计算每一条新生染色体的适应程度，并根据适应程度计算每一条染色体在下一次进化中被选中的概率(这个上面已经介绍，这里不再赘述)。

上面都是准备过程，下面正式进入“进化”过程。

- 通过“交叉”，生成N-M条染色体；
- 再对交叉后生成的N-M条染色体进行“变异”操作；
- 然后使用“复制”的方式生成M条染色体；

到此为止，N条染色体生成完毕！紧接着分别计算N条染色体的适应度和下次被选中的概率。

这/6就是一次进化的过程，紧接着进行新一轮的进化。

+

—+—————————————————————————————————+



### 决策树分类

决策树是一个预测模型，它代表的是对象属性与对象值之间的一种映射关系。树中每个节点表示某个对象，而每个分叉路径则代表某个可能的属性值，而每个叶节点则对应从根节点到该叶节点所经历的路径所表示的对象的值。

从数据产生决策树的机器学习技术叫做决策树学习，通俗说就是决策树。

一个决策树包含三种类型的节点：

1. 决策节点：通常用矩形框来表示
2. 机会节点：通常用圆圈来表示
3. 终结节点：通常用三角形来表示





————————————————————————————————————



### 树

树结构通常用来存储逻辑关系为 "一对多" 的数据。例如：

![img](http://data.biancheng.net/uploads/allimg/220724/102H33H1-0.png)
[图](http://data.biancheng.net/view/321.html) 1 树存储结构

图 1a) 的这些元素具有的就是 "一对多" 的逻辑关系，例如元素 A 同时和 B、C、D 有关系，元素 D 同时和 A、H、I、J 有关系等。 观察这些元素之间的逻辑关系会发现，它们整体上很像一棵倒着的树（将图 1b) 倒过来），这也是将存储它们的结构起名为“树”（或者 "树形"）的原因。

存储具有 "一对多" 逻辑关系的数据，数据结构推荐使用树存储结构。



**有关树的术语**

1）结点

与链表相似，树存储结构中也将存储的各个元素称为”结点“，例如上图中，A就是一个结点

对于树的某些特殊位置的结点，还可以进行更细致的划分，比如：

- **父节点、子节点、兄弟结点：**以图 1a) 中的结点 A、B、C、D 为例，A 是 B、C、D 结点的父结点（也称为“双亲结点”），而 B、C、D 都是 A 结点的孩子结点（也称“子结点”）。对于 B、C、D 来说，它们都有相同的父结点，所以它们互为兄弟结点；

- **树根结点（简称 "根结点" ）：**特指树中没有双亲（父亲）的结点，一棵树有且仅有一个根结点。例如图 1a) 中，结点 A 就是整棵树的根结点；
- **叶子结点（简称 "叶结点" ）**：特指树中没有孩子的结点，一棵树可以有多个叶子结点。例如图 1a) 中，结点 K、L、F、G、M、I、J 都是叶子结点。



##### 2) 子树

仍以图 1a) 的树为例，A 是整棵树的根结点。但如果单看结点 B、E、F、K、L 组成的部分来说，它们也组成了一棵树，结点 B 是这棵树的根结点。通常，我们将一棵树中几个结点构成的“小树”称为这棵树的“子树”。

知道了子树的概念后，

树也可以这样定义：树是由根结点和若干棵子树构成的

。例如，图 1a) 这棵树就是由结点 A 和分别以 B、C、D 为根节点的子树构成。

> 注意：单个结点也可以看作是一棵树，该结点即为根结点。例如图 1a) 中，结点 K、L、F 各自就可以看作是一棵树，只不过树中只有一个根节点而已。



##### 3) 结点的度

一个结点拥有子树的个数，就称为该结点的

度

（Degree）

。例如图 1a) 中，根结点 A 有 3 个子树，它们的根节点分别是 B、C、D，因此结点 A 的度为 3。

比较一棵树中所有结点的度，最大的度即为整棵树的度。比如图 1a) 中，所有结点中最大的度为 3，所以整棵树的度就是 3。



##### 4) 结点的层次

从一棵树的树根开始，树根所在层为第一层，根的孩子结点所在的层为第二层，依次类推。

对于图 1a) 这棵树来说，A 结点在第一层，B、C、D 为第二层，E、F、G、H、I、J 在第三层，K、L、M 在第四层。

树中结点层次的最大值，称为这棵树的深度或者高度。例如图 1a) 这棵树的深度为 4。

> 如果两个结点的父结点不同，但它们父结点的层次相同，那么这两个结点互为堂兄弟。例如图 1a) 中，结点 G 和 E、F、H、I、J 的父结点都在第二层，所以它们互为堂兄弟。



##### 5) 有序树和无序树

如果一棵树中，各个结点左子树和右子树的位置不能交换，那么这棵树就称为有序树。反之，如果树中结点的左、右子树可以互换，那么这棵树就是一棵无序树。

在有序树中，结点最左边的子树称为 "第一个孩子"，最右边的称为 "最后一个孩子"。拿图 1a) 这棵树来说，如果它是一棵有序树，那么以结点 B 为根结点的子树为整棵树的第一个孩子，以结点 D 为根结点的子树为整棵树的最后一个孩子。



##### 6) 森林

由 m（m >= 0）个互不相交的树组成的集合就称为森林。比如图 1a) 中除去 A 结点，那么分别以 B、C、D 为根结点的三棵子树就可以称为森林。

前面讲到，树可以理解为是由根结点和若干子树构成的，而这若干子树本身就是一个森林，因此树还可以理解为是由根结点和森林组成的。



##### 7) 空树（简单了解即可）

空树指的是没有任何结点的树，连根结点都没有。



**树的其它表示方法**

除了图 1a) 这样画一棵树之外，还有其它的方式可以表示一棵树。

![img](http://data.biancheng.net/uploads/allimg/220724/102H35E8-1.png)

图 2 树的表示形式

图 2 左侧是以嵌套集合的形式表示的

（集合之间绝不能相交，即任意两个圆圈不能有交集）

。

图 2 右侧使用的是

凹入表示法

，最长条为根结点，相同长度的表示在同一层次。例如 B、C、D 长度相同，都为 A 的子结点，E 和 F 长度相同，为 B 的子结点，K 和 L 长度相同，为 E 的子结点，依此类推。

还可以用广义表表示一棵树。例如图 1a) 用广义表表示为：

(A , ( B ( E ( K , L ) , F ) , C ( G ) , D ( H ( M ) , I , J ) ) )



**总结**

树是一种非线性存储结构，通常用来存储逻辑关系为 "一对多" 的数据。

使用树结构存储的各个结点，它们之间的关系类似于家谱中的成员关系，比如有父子关系、兄弟关系、表兄弟关系等。



——————————————————————————



#### 二叉树

简单的理解，满足以下两个条件的树就是二叉树

1. 本身是有序树
2. 树中包含的各个结点的度(子树个数)不能超过2，即只能是0、1或者是2；

例如，图1a）就是一棵二叉树，而图1b）则不是

![二叉树示意图](http://data.biancheng.net/uploads/allimg/181226/2-1Q226195I0M1.gif)



##### 二叉树的性质

经过总结，二叉树具有以下几个性质：

1. 二叉树中，第 i 层最多有 $\ 2^{i-1}$ 个结点。
2. 如果二叉树的深度为 K，那么此二叉树最多有 $ 2^K-1$ 个结点。
3. 二叉树中，终端结点数（叶子结点数）为 n0，度为 2 的结点数为 n2，则 n0=n2+1。

性质3的计算方法为：对于一个二叉树来说，除了度为0的叶子结点和度为2的结点，剩下的就是度为1的结点（设为$n_1）$,那么总结点$n=n_0 + n_1+n_2$.

同时，对于每一个结点来说都是由其父节点分支表示的，假设树中分支树为B，那么总结点数$n=B+1$。而分枝数可以通过$n_1$和$n_2$来表示，即$B = n_1+2*n_2$。所以，n用另一种方式表示为$n=n_1 + 2*n_2+1$。

两种方式得到的n值组成一个方程组，就可以得出$n_0=n_2+1$。



同时，二叉树还可以继续分类，衍生出**满二叉树**和**完全二叉树**



##### 满二叉树

如果二叉树中除了叶子结点，*<u>每个结点的度都为2</u>*，则此二叉树称为**满二叉树**

![满二叉树示意图](http://data.biancheng.net/uploads/allimg/181226/2-1Q226195949495.gif)图2 满二叉树示意图



满二叉树除了满足普通二叉树的性质，还具有以下性质：

1. 满二叉树中的第i层的结点数为$2^{i-1}$。
2. 深度为k的满二叉树必有$2^k-1$个结点，叶子数为$2^{k-1}$。
3. 满二叉树中不存在度为1的结点，每一个分支点中都有两棵深度相同的子树，且叶子结点都在最底层
4. 具有n个结点的满二叉树的深度为$log_2(n+1)$



##### 完全二叉树

如果二叉树中除去**最后一层结点为满二叉树，且最后一层的结点依次从左到右分布**，则此二叉树被称为完全二叉树

**![完全二叉树示意图](http://data.biancheng.net/uploads/allimg/181226/2-1Q22620003J18.gif)**图3 完全二叉树示意图

如图 3a) 所示是一棵完全二叉树，图 3b) 由于最后一层的节点没有按照从左向右分布，因此只能算作是普通的二叉树。

完全二叉树除了具有普通二叉树的性质，它自身也具有一些独特的性质，比如说，n 个结点的完全二叉树的深度为 ⌊$log_2n$⌋+1。

· ⌊$log_2n$⌋表示取小于$log_2n$的最大整数（向下取整）例如，⌊log24⌋ = 2，而 ⌊log25⌋ 结果也是 2。

对于任意一个完全二叉树来说，如果将含有的结点按照层次从左到右依次标号（如图 3a)），对于任意一个结点 i ，完全二叉树还有以下几个结论成立：

1. 当 i>1 时，父亲结点为结点 [i/2] 。（i=1 时，表示的是根结点，无父亲结点）
2. 如果 2\*i>n（总结点的个数） ，则结点 i 肯定没有左孩子（为叶子结点）；否则其左孩子是结点 2*i 。
3. 如果 2\*i+1>n ，则结点 i 肯定没有右孩子；否则右孩子是结点 2*i+1 。







##### 信息熵

信息熵就是不确定的一个度量，反映信息量的多少，信息量的多少与随机事件发生的概率有关，概率越大，不确定性越小，信息量也就越少，所以随机时间的信息量随其发生的概率递减，信息熵计算公式如下![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/ZZ2XQXo849WJOFMEzBX6IaPlibBZZFLKFvg68dKmAf5e7luJS5icR3seUG0G3MOB6dDy8ebVcjU2iaM1Fib3JtbDBw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其中$x_i$为随机变量X的取值，p为随机事件$x_i$发生的概率



##### 熵权法

根据信息熵的特性，可以用来衡量一个指标的离散程度，指标离散层度越大，该指标对综合评价的影响也就越大，权重也会越大，**熵权法是一种依赖于数据本身离散性的客观赋值法**，用于结合多种指标对样本进行综合打分，实现样本间比较

假定有n条样本，m个维度，用如下方式表示每个随机变量的取值：

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/ZZ2XQXo849WJOFMEzBX6IaPlibBZZFLKFSHKhCYY2Lw9VSKxSnslQwcEcibicCOsbicQs4OiaBD02T4x2V8JicchpiaOw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**step 1 : 标准化处理**

为避免量纲造成的影响，首先要对指标进行标准化处理。根据指标含义，可将指标分为正向指标（取值越大越好）和逆向指标（取值越小越好），分别通过如下方法进行标准化：

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/ZZ2XQXo849WJOFMEzBX6IaPlibBZZFLKFTDiceYUgpEebxtmmuLEKFKSW3PBiceqTM2ICLsIZRa1DOTN7sicrFedxA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/ZZ2XQXo849WJOFMEzBX6IaPlibBZZFLKFqic3eWsiaOYHuwiaWmTVG6GllF04H03FGlGviajBvyse0gXt8bl5RdonFQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**step 2 : 计算每个维度的熵**

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/ZZ2XQXo849WJOFMEzBX6IaPlibBZZFLKF4Pic7wHTgtnUXBnjicKDPaWtemIeBpLlsVRdXd2dL8sHujlOnBRrbNug/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其中，

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/ZZ2XQXo849WJOFMEzBX6IaPlibBZZFLKFSdKhtpPr5RwIDbVHCNhQ22jZliaFCh1icPUOx6OJzMSaGd39NNd0Lic4Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/ZZ2XQXo849WJOFMEzBX6IaPlibBZZFLKFicGMv8qAQ7QUKcZJI15d3CosVAK3zXxnS9Oa25TKfypeLFzXAC1kxbA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**step 3 : 计算冗余度（差异）**

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/ZZ2XQXo849WJOFMEzBX6IaPlibBZZFLKFibX7iaf9DmrZ2DkSp3lz2icfCuQtODccu4bZQX27kAwoGXDb2X6Lcob6w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**step 4 : 计算权重**

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/ZZ2XQXo849WJOFMEzBX6IaPlibBZZFLKFqFibKNLWRdfBIrnyGGibQzqGykfjHBCh5xMibfWRc4RsGMehC7icsnicmNw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**step 5 : 计算综合评分**

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/ZZ2XQXo849WJOFMEzBX6IaPlibBZZFLKFfFD2dGw7WSQppLvnKh6jjibz1lbBg1DZE7dWwaYzS9o919f3X8qlOicg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)





##### TOPSIS综合评价

**TOPSIS** （Technique for Order Preference by Similarity to an Ideal Solution ）模型中文叫做“逼近理想解排序方法”，是根据评价对象与理想化目标的接近程度进行排序的方法，是一种距离综合评价方法。基本思路是通过假定正、负理想解，测算各样本与正、负理想解的距离，得到其与理想方案的相对贴近度（即距离正理想解越近同时距离负理想解越远），进行各评价对象的优劣排序。**具体步骤及概念**如下：

**step 1： 指标同向化、标准化并得到权重。**这部分与熵权法结合，通过熵权法得到权重，避免主观因素影响，得到权重向量W及标准化矩阵P。具体内容可参照[综合评价之熵权法](https://link.zhihu.com/?target=http%3A//mp.weixin.qq.com/s%3F__biz%3DMzAwNTIyMDU3NA%3D%3D%26mid%3D2648493330%26idx%3D1%26sn%3Db35a47315b4dbf2229248baf4ac130b6%26chksm%3D83379ca3b44015b5c7ecdc2087e40e4652212d29ec92db0a6918529f3fc0e300773dab10242f%26scene%3D21%23wechat_redirect)，这里不再赘述。

**step 2** **： 得到加权后的规范化矩阵Z。**Z由P与W相乘后得到。

![img](https://pic2.zhimg.com/80/v2-2d8d419df8322bccc8b6b3ab72ff79c1_1440w.webp)

**step 3** **： 确定正、负理想解。**正理想解指各指标都达到样本中最好的值，负理想解指各指标都为样本中最差的值。

**step 4** **： 计算各样本距离正、负理想解的距离。**

![img](https://pic2.zhimg.com/80/v2-ea8f477b90f5a171a95eb84d405c721d_1440w.webp)

**step 5 ： 计算各评价对象与最优方案的贴近程度。**正其中

的取值范围为[0,1]，越接近1表明样本评分越好。

![img](https://pic2.zhimg.com/80/v2-68dea8e7c8c12c5e0f430a8ad0962029_1440w.webp)









# Transformer

![img](https://img-blog.csdnimg.cn/2021052223091261.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbnpodWppZTEyNDVjb20=,size_16,color_FFFFFF,t_70)





#### 霍夫变换算法

https://blog.csdn.net/u013631121/article/details/130298870



说到霍夫变换，首先就得说说坐标系的事情，虽然这都是初、高中的知识了，但经过大学几年的洗刷，不知道各位还能记住多少。为了使大家的远古记忆觉醒，我就领大家回忆回忆！

​    首先是直线的直角坐标系方程（以x，y为坐标轴），y=k*x+b，不知道还记不记得？k是斜率，b是直线与y轴的交点，x、y是变量，如图1所示：

![img](https://img-blog.csdnimg.cn/88195daa3e7b4ff991891c81d7f7aacb.png)

图1



​    如果我们已知图像上面任意两个点，系数k，b就能够确定，那么方程就可以写成图2的形式。

![img](https://img-blog.csdnimg.cn/49a53759e5624756811f215e7032b02f.png)

 图2



而当我们确定了k、b之后，我们可以将其作为一个点的位置，并将其画到另一个以k、b为坐标轴的直角坐标系主管那，我们就可以得到图3的**霍夫空间**

![img](https://img-blog.csdnimg.cn/b55f9f6984574850bb8a5a2544ff5cfa.png)

图三



假定霍夫空间中有一条线，它的方程为b=-x3*k+y3，也就是y3=k*x3+b。那么它对应的x，y直角坐标系就是一个点（x3，y3），如图4。反过来也可以说，直角坐标系中的一个点，就是霍夫空间中的一条直线。（简单点理解就是，我们可以将以霍夫空间中的直线看成原来的直角坐标系，在霍夫空间中，一条直线的斜率与偏置是固定的，因此我们换算过来直角坐标系中就是一个点，相当于作用互换，x、y变成了k（斜率）以及b（偏置），k、b变成了x（变量）、y（因变量））

![img](https://img-blog.csdnimg.cn/3c22195c5e9945c991821da3dd5be8fc.png)

图四





霍夫空间有一个定理：假定直角坐标系有N个点，如果这N个点能够在直角坐标系中连成一条直线，那么它们在霍夫空间中就会交于一点。

​    假如N=3，有三个点，分别是(1,2),(2,4),(3,6)，这三个点在直角坐标系中可以连成一条直线y=2*x，我们看图5，他们在霍夫空间中肯定会交于一点。



![img](https://img-blog.csdnimg.cn/e6a959751b1d4009b55060059149cfa7.png)

图5



但是在我们[计算机视觉](https://so.csdn.net/so/search?q=计算机视觉&spm=1001.2101.3001.7020)里面，很少有人使用直角坐标系来解决问题，而使用极坐标。

**极坐标**：**用角度和长度描述位置的坐标系**

* 以原点$O$为起点的射线作为参考系， 称$O$为**极点**， 这条射线为**极轴**
* 点$P$到原点的距离记为$OP=r(>=0)$，称之为**极径**
* 从参考系射线发出逆时针旋转到$OP$所经过的角度，称为**极角**



使用极坐标的原因是当直角坐标系的直线垂直于x轴时，k为无穷大。这很难在计算机中表示，使用极坐标就能够很好的解决这个问题。极坐标方程如图6所示，ρ代表长度，θ代表角度。这个怎么来的呢，假如我们有一点（x4，y4），它的极坐标求法看图7，一下就明白了。

![img](https://img-blog.csdnimg.cn/9c4d9268ba524f8f94a6bc14c48da5a4.png)

图6





![img](https://img-blog.csdnimg.cn/32fe4d4da1cf437fba323d2b6eed0c52.png)

 图7



直角坐标系的一点(x4,y4)，对应极坐标系下的一条正弦曲线ρ4=x4*cosθ4+y4*sinθ4，我们称这个极坐标系为“极坐标霍夫空间”，盗用别人一张图：

![img](https://img-blog.csdnimg.cn/378e83b2dd794a48a53df247220bbdbe.png)

图8

​       我们根据上面的原理，直角坐标系有N个点，如果这N个点能够在直角坐标系中连成一条直线，那么它们在霍夫空间中肯定会交于一点。在“极坐标霍夫空间”中也是一样，只是变为曲线交于一点，如图8所示。

​        这样，我们就把直角坐标系的点，变换到极坐标霍夫空间中了。









**transformer概览**

首先我们先将 Transformer 模型视为一个黑盒，如图 1.2 所示。在机器翻译任务中，将一种语言的一个句子作为输入，然后将其翻译成另一种语言的一个句子作为输出。

![img](https://img-blog.csdnimg.cn/20210522231501696.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbnpodWppZTEyNDVjb20=,size_16,color_FFFFFF,t_70)

Transformer 本质上是一个 Encoder-Decoder 架构。因此中间部分的 Transformer 可以分为两个部分：编码组件和解码组件。如图 1.3 所示：

![img](https://img-blog.csdnimg.cn/2021052223173542.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbnpodWppZTEyNDVjb20=,size_16,color_FFFFFF,t_70)



其中，编码组件由多层编码器（Encoder）组成（在论文中作者使用了 6 层编码器，在实际使用过程中你可以尝试其他层数）。解码组件也是由相同层数的解码器（Decoder）组成（在论文也使用了 6 层）。如图 1.4 所示：

![img](https://img-blog.csdnimg.cn/20210522231844885.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbnpodWppZTEyNDVjb20=,size_16,color_FFFFFF,t_70)

每个编码器由两个子层组成：[Self-Attention](https://so.csdn.net/so/search?q=Self-Attention&spm=1001.2101.3001.7020) 层（自注意力层）和 Position-wise Feed Forward Network（前馈网络，缩写为 FFN）如图 1.5 所示。每个编码器的结构都是相同的，但是它们使用不同的权重参数。

![img](https://img-blog.csdnimg.cn/20210522231904793.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbnpodWppZTEyNDVjb20=,size_16,color_FFFFFF,t_70)







# Mobilenet

[原文地址](https://zhuanlan.zhihu.com/p/666016268)

Mobilenet是一个专注于嵌入式设备或移动端的轻量级CNN网络，它在原有的CNN网络的基础下，减少了少许的准确度，但大大减少了模型参数与运算量，增加了运算速率。

同时它的亮点在于使用了Depthwise Convolution（卷积核）、并增加了超参数$a$（控制卷积层、核数量）、$β$（控制输入图像尺寸）



## Depthwise Separable卷积

这个卷积由两个部分组成

### DW卷积

这个卷积与普通的卷积操作的不同在于，**普通的卷积核**的channel是由输入特征的channel来决定的，而卷积过后输出的特征的数量则是由卷积核的数量来决定的，即：

![img](https://pic1.zhimg.com/80/v2-0233422cca52a4bab9d5d6e1c8fb44b8_720w.webp)

特点：![img](https://pic3.zhimg.com/80/v2-94b324769f724b73ba0a3b3d21fca962_720w.webp)



而**DW卷积**每个核都只有一个通道，然后每个1channel的卷积核负责一个输入特征图的一个channel的卷积，而输出特征图的channel依旧等于卷积核的个数，即：

![img](https://pic2.zhimg.com/80/v2-9c709d49dddac565fe1c617f0a9f80d9_720w.webp)

特点：![img](https://pic1.zhimg.com/80/v2-007136fd454eb0ba22217f13bfeda4f4_720w.webp)







### PW卷积

pw卷积与传统的卷积操作一样，都是用于将输入特征的channel数量增加或减少，即：

![img](https://pic4.zhimg.com/80/v2-a7821aedde9e4f24d46f987cb2fb3e8f_720w.webp)

![img](https://pic2.zhimg.com/80/v2-dee693997b59b73dc1a782cbe8443851_720w.webp)

从上面我们可以看到，一个不同的卷积操作就能使得mobilenet的卷积操作运算亮大幅减少



## MobileNet网络架构及超参数

![img](https://pic1.zhimg.com/80/v2-3ba5d24eadc15431a4e8c932667378ec_720w.webp)

其中每个卷积核的基本结构为：![img](https://pic1.zhimg.com/80/v2-d6dcf3374080ba04d05ad4547af8aef8_720w.webp)

两个超参数$a$(Width Multiplier)、$β$(Resolution Multiplier):

* $a$代表的是卷积核个数的倍率因子，控制卷积核的个数，即按比例减少通道数，输入与输出通道数变成$aM$和$aN$
* $β$代表的是分辨率的倍率因子，输入不同尺寸的图像会有不同的准确率，比如原来的输入的特征图的大小为224x224，经过倍率因子，我们可以缩放到192x192















