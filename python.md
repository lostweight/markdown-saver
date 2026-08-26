# 面向对象

什么是面向对象：**面向对象就是对面向过程编程的一个封装**

简单点来说就是：面向对象就是面向过程编程的时候实现的功能封装到一个抽象的类里面，当需要执行任务的时候我们只需要找这个抽象的类帮我们完成这些功能

面向对象的主要思想： 1. 划分任务具体的步骤

​				     2. 给步骤划分出具体需要实现的功能

​				     3. 将实现的功能划分给抽象的对象

​				     4. 按照抽象的对象实现功能的需要设计出实际的对象 

# 数据类型

## Number（数字）

Python3 支持 **int、float、bool、complex（复数）**。

在Python 3里，只有一种整数类型 int，表示为长整型，没有 python2 中的 Long。

像大多数语言一样，数值类型的赋值和计算都是很直观的。

内置的 type() 函数可以用来查询变量所指的对象类型。

```
>>> a, b, c, d = 20, 5.5, True, 4+3j
>>> print(type(a), type(b), type(c), type(d))
<class 'int'> <class 'float'> <class 'bool'> <class 'complex'>
```

此外还可以用 isinstance 来判断：

```
>>> a = 111
>>> isinstance(a, int)
True
>>>
```



isinstance 和 type 的区别在于：

- type()不会认为子类是一种父类类型。
- isinstance()会认为子类是一种父类类型。

例如：

```
>>> class A:
...     pass
... 
>>> class B(A):
...     pass
... 
>>> isinstance(A(), A)
True
>>> type(A()) == A 
True
>>> isinstance(B(), A)
True
>>> type(B()) == A
False

```

简单点理解就是，type() 认为子类与父类的类型并不一致，而isinstance()会认为子类与父类其实是一种类型



## String（字符串）

Python中的字符串用单引号 **'** 或双引号 **"** 括起来，同时使用反斜杠 **\** 转义特殊字符。

字符串的截取的语法格式如下：

```
变量[头下标:尾下标]
```

索引值以 0 为开始值，-1 为从末尾的开始位置。

![img](https://static.runoob.com/wp-content/uploads/123456-20200923-1.svg)



加号 **+** 是字符串的连接符， 星号 ***** 表示复制当前字符串，与之结合的数字为复制的次数。实例如下：

###### 实例

\#!/usr/bin/python3

str = 'Runoob'

**print** (str)          # 输出字符串
**print** (str[0:-1])    # 输出第一个到倒数第二个的所有字符
**print** (str[0])       # 输出字符串第一个字符
**print** (str[2:5])     # 输出从第三个开始到第五个的字符
**print** (str[2:])      # 输出从第三个开始的后的所有字符
**print** (str * 2)      # 输出字符串两次，也可以写成 print (2 * str)
**print** (str + "TEST") # 连接字符串

执行以上程序会输出如下结果：

```
Runoob
Runoo
R
noo
noob
RunoobRunoob
RunoobTEST
```



Python 使用反斜杠 **\** 转义特殊字符，如果你不想让反斜杠发生转义，可以在字符串前面添加一个 **r**，表示原始字符串：

###### 实例

\>>> **print**('Ru**\n**oob')
Ru
oob
\>>> **print**(r'Ru**\n**oob')
Ru\noob
\>>>

另外，反斜杠(\)可以作为续行符，表示下一行是上一行的延续。也可以使用 **"""..."""** 或者 **'''...'''** 跨越多行。

注意，Python 没有单独的字符类型，一个字符就是长度为1的字符串。



## 运算符

本章节主要说明 Python 的运算符。

举个简单的例子:

```
4 + 5 = 9
```

例子中，**4** 和 **5** 被称为**操作数**，**+** 称为**运算符**。

Python 语言支持以下类型的运算符:

- [算术运算符](https://www.runoob.com/python3/python3-basic-operators.html#ysf1)
- [比较（关系）运算符](https://www.runoob.com/python3/python3-basic-operators.html#ysf2)
- [赋值运算符](https://www.runoob.com/python3/python3-basic-operators.html#ysf3)
- [逻辑运算符](https://www.runoob.com/python3/python3-basic-operators.html#ysf4)
- [位运算符](https://www.runoob.com/python3/python3-basic-operators.html#ysf5)
- [成员运算符](https://www.runoob.com/python3/python3-basic-operators.html#ysf6)
- [身份运算符](https://www.runoob.com/python3/python3-basic-operators.html#ysf7)
- [运算符优先级](https://www.runoob.com/python3/python3-basic-operators.html#ysf8)

接下来让我们一个个来学习Python的运算符。



### 算术运算符

以下假设变量 **a=10**，变量 **b=21**：

| 运算符 | 描述                                            | 实例                      |
| :----- | :---------------------------------------------- | :------------------------ |
| +      | 加 - 两个对象相加                               | a + b 输出结果 31         |
| -      | 减 - 得到负数或是一个数减去另一个数             | a - b 输出结果 -11        |
| *      | 乘 - 两个数相乘或是返回一个被重复若干次的字符串 | a * b 输出结果 210        |
| /      | 除 - x 除以 y                                   | b / a 输出结果 2.1        |
| %      | 取模 - 返回除法的余数                           | b % a 输出结果 1          |
| **     | 幂 - 返回x的y次幂                               | a**b 为10的21次方         |
| //     | 取整除 - 往小的方向取整数                       | `>>> 9//2 4 >>> -9//2 -5` |



### 比较运算符

以下假设变量 a 为 10，变量 b 为20：

| 运算符 | 描述                                                         | 实例                  |
| :----- | :----------------------------------------------------------- | :-------------------- |
| ==     | 等于 - 比较对象是否相等                                      | (a == b) 返回 False。 |
| !=     | 不等于 - 比较两个对象是否不相等                              | (a != b) 返回 True。  |
| >      | 大于 - 返回x是否大于y                                        | (a > b) 返回 False。  |
| <      | 小于 - 返回x是否小于y。所有比较运算符返回1表示真，返回0表示假。这分别与特殊的变量True和False等价。注意，这些变量名的大写。 | (a < b) 返回 True。   |
| >=     | 大于等于 - 返回x是否大于等于y。                              | (a >= b) 返回 False。 |
| <=     | 小于等于 - 返回x是否小于等于y。                              | (a <= b) 返回 True。  |



## 赋值运算符

以下假设变量a为10，变量b为20：

| 运算符 | 描述                                                         | 实例                                                         |
| :----- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| =      | 简单的赋值运算符                                             | c = a + b 将 a + b 的运算结果赋值为 c                        |
| +=     | 加法赋值运算符                                               | c += a 等效于 c = c + a                                      |
| -=     | 减法赋值运算符                                               | c -= a 等效于 c = c - a                                      |
| *=     | 乘法赋值运算符                                               | c *= a 等效于 c = c * a                                      |
| /=     | 除法赋值运算符                                               | c /= a 等效于 c = c / a                                      |
| %=     | 取模赋值运算符                                               | c %= a 等效于 c = c % a                                      |
| **=    | 幂赋值运算符                                                 | c **= a 等效于 c = c ** a                                    |
| //=    | 取整除赋值运算符                                             | c //= a 等效于 c = c // a                                    |
| :=     | 海象运算符，可在表达式内部为变量赋值。**Python3.8 版本新增运算符**。 | 在这个示例中，赋值表达式可以避免调用 len() 两次:`if (n := len(a)) > 10:     print(f"List is too long ({n} elements, expected <= 10)")` |

海象运算符的语法是在表达式中使用 ":=" 来给变量赋值。它通常用于条件语句、循环语句和表达式中。以下是一些使用海象运算符的示例：

1. 在条件语句中使用海象运算符：

```
if (n := len(my_list)) > 10:
    print(f"List is too long ({n} elements, expected <= 10)")
```

1. 在循环语句中使用海象运算符：

```
while (line := input()) != "quit":
    print(f"You entered: {line}")
```

1. 在表达式中使用海象运算符：

```
result = (value := my_function()) + 10
```

使用海象运算符可以减少代码行数，使代码更简洁和易读。然而，需要注意的是，在某些情况下，滥用海象运算符可能会导致代码变得难以理解。



`注意`：在程序中表达式 **是可以被求值的代码**（这段代码不一定有=号，但是一定是关于数学求解的），而语句是一段 可执行代码 



### 位运算符

按位运算符是把数字看作二进制来进行计算的。Python中的按位运算法则如下：

下表中变量 a 为 60，b 为 13二进制格式如下：

```
a = 0011 1100

b = 0000 1101

-----------------

a&b = 0000 1100

a|b = 0011 1101

a^b = 0011 0001

~a  = 1100 0011
```

| 运算符 | 描述                                                         | 实例                                                         |
| :----- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| &      | 按位与运算符：参与运算的两个值,如果两个相应位都为1,则该位的结果为1,否则为0 | (a & b) 输出结果 12 ，二进制解释： 0000 1100                 |
| \|     | 按位或运算符：只要对应的二个二进位有一个为1时，结果位就为1。 | (a \| b) 输出结果 61 ，二进制解释： 0011 1101                |
| ^      | 按位异或运算符：当两对应的二进位相异时，结果为1              | (a ^ b) 输出结果 49 ，二进制解释： 0011 0001                 |
| ~      | 按位取反运算符：对数据的每个二进制位取反,即把1变为0,把0变为1。**~x** 类似于 **-x-1** | (~a ) 输出结果 -61 ，二进制解释： 1100 0011， 在一个有符号二进制数的补码形式。 |
| <<     | 左移动运算符：运算数的各二进位全部左移若干位，由"<<"右边的数指定移动的位数，高位丢弃，低位补0。 | a << 2 输出结果 240 ，二进制解释： 1111 0000                 |
| >>     | 右移动运算符：把">>"左边的运算数的各二进位全部右移若干位，">>"右边的数指定移动的位数 | a >> 2 输出结果 15 ，二进制解释： 0000 1111                  |

执行结果

```
a = 60            # 60 = 0011 1100 
b = 13            # 13 = 0000 1101 
c = 0
c = a << 2       # 240 = 1111 0000
print ("5 - c 的值为：", c)
 
c = a >> 2       # 15 = 0000 1111
print ("6 - c 的值为：", c)

>>>
	5 - c 的值为： 240
	6 - c 的值为： 15
```



### 逻辑运算符

Python语言支持逻辑运算符，以下假设变量 a 为 10, b为 20:

| 运算符 | 逻辑表达式 | 描述                                                         | 实例                    |
| :----- | :--------- | :----------------------------------------------------------- | :---------------------- |
| and    | x and y    | 布尔"与" - 如果 x 为 False，x and y 返回 x 的值，否则返回 y 的计算值。 | (a and b) 返回 20。     |
| or     | x or y     | 布尔"或" - 如果 x 是 True，它返回 x 的值，否则它返回 y 的计算值。 | (a or b) 返回 10。      |
| not    | not x      | 布尔"非" - 如果 x 为 True，返回 False 。如果 x 为 False，它返回 True。 | not(a and b) 返回 False |



### 成员运算符

除了以上的一些运算符之外，Python还支持成员运算符，测试实例中包含了一系列的成员，包括字符串，列表或元组。

| 运算符 | 描述                                                    | 实例                                              |
| :----- | :------------------------------------------------------ | :------------------------------------------------ |
| in     | 如果在指定的序列中找到值返回 True，否则返回 False。     | x 在 y 序列中 , 如果 x 在 y 序列中返回 True。     |
| not in | 如果在指定的序列中没有找到值返回 True，否则返回 False。 | x 不在 y 序列中 , 如果 x 不在 y 序列中返回 True。 |



### 身份运算符

身份运算符用于比较两个对象的存储单元

| 运算符 | 描述                                        | 实例                                                         |
| :----- | :------------------------------------------ | :----------------------------------------------------------- |
| is     | is 是判断两个标识符是不是引用自一个对象     | **x is y**, 类似 **id(x) == id(y)** , 如果引用的是同一个对象则返回 True，否则返回 False |
| is not | is not 是判断两个标识符是不是引用自不同对象 | **x is not y** ， 类似 **id(x) != id(y)**。如果引用的不是同一个对象则返回结果 True，否则返回 False。 |



### 运算符优先级

以下表格列出了从最高到最低优先级的所有运算符， 相同单元格内的运算符具有相同优先级。 运算符均指二元运算，除非特别指出。 相同单元格内的运算符从左至右分组（除了幂运算是从右至左分组）：

| 运算符                                                       | 描述                               |
| :----------------------------------------------------------- | :--------------------------------- |
| `(expressions...)`,`[expressions...]`, `{key: value...}`, `{expressions...}` | 圆括号的表达式                     |
| `x[index]`, `x[index:index]`, `x(arguments...)`, `x.attribute` | 读取，切片，调用，属性引用         |
| await x                                                      | await 表达式                       |
| `**`                                                         | 乘方(指数)                         |
| `+x`, `-x`, `~x`                                             | 正，负，按位非 NOT                 |
| `*`, `@`, `/`, `//`, `%`                                     | 乘，矩阵乘，除，整除，取余         |
| `+`, `-`                                                     | 加和减                             |
| `<<`, `>>`                                                   | 移位                               |
| `&`                                                          | 按位与 AND                         |
| `^`                                                          | 按位异或 XOR                       |
| `|`                                                          | 按位或 OR                          |
| `in,not in, is,is not, <, <=, >, >=, !=, ==`                 | 比较运算，包括成员检测和标识号检测 |
| `not x`                                                      | 逻辑非 NOT                         |
| `and`                                                        | 逻辑与 AND                         |
| `or`                                                         | 逻辑或 OR                          |
| `if -- else`                                                 | 条件表达式                         |
| `lambda`                                                     | lambda 表达式                      |
| `:=`                                                         | **赋值表达式**                     |

 	以下实例演示了Python所有运算符优先级的操作：

```
#!/usr/bin/python3
 
a = 20
b = 10
c = 15
d = 5
e = 0
 
e = (a + b) * c / d       #( 30 * 15 ) / 5
print ("(a + b) * c / d 运算结果为：",  e)
 
e = ((a + b) * c) / d     # (30 * 15 ) / 5
print ("((a + b) * c) / d 运算结果为：",  e)
 
e = (a + b) * (c / d)    # (30) * (15/5)
print ("(a + b) * (c / d) 运算结果为：",  e)
 
e = a + (b * c) / d      #  20 + (150/5)
print ("a + (b * c) / d 运算结果为：",  e)

>>>
	(a + b) * c / d 运算结果为： 90.0
	((a + b) * c) / d 运算结果为： 90.0
	(a + b) * (c / d) 运算结果为： 90.0
	a + (b * c) / d 运算结果为： 50.0

```



### 推导式

Python 推导式是一种独特的数据处理方式，可以从一个数据序列构建另一个新的数据序列的结构体。

Python 支持各种数据结构的推导式：

- 列表(list)推导式
- 字典(dict)推导式
- 集合(set)推导式
- 元组(tuple)推导式

#### 列表推导式

列表推导式格式为：

```
[表达式 for 变量 in 列表] 
[out_exp_res for out_exp in input_list]

或者 

[表达式 for 变量 in 列表 if 条件]
[out_exp_res for out_exp in input_list if condition]
```

- out_exp_res：列表生成元素表达式，可以是有返回值的函数。
- for out_exp in input_list：迭代 input_list 将 out_exp 传入到 out_exp_res 表达式中。
- if condition：条件语句，可以过滤列表中不符合条件的值。



过滤掉长度小于或等于3的字符串列表，并将剩下的转换成大写字母：

###### 实例

\>>> names = ['Bob','Tom','alice','Jerry','Wendy','Smith']
\>>> new_names = [name.upper()**for** name **in** names **if** len(name)>3]
\>>> **print**(new_names)
['ALICE', 'JERRY', 'WENDY', 'SMITH']



###### 实例

```
>>> multiples = [i for i in range(30) if i % 3 == 0]
>>> print(multiples)
[0, 3, 6, 9, 12, 15, 18, 21, 24, 27]
```



### 字典推导式

字典推导基本格式：

```
{ key_expr: value_expr for value in collection }

或

{ key_expr: value_expr for value in collection if condition }
```



使用字符串及其长度创建字典：

###### 实例

listdemo = ['Google','Runoob', 'Taobao']
\# 将列表中各字符串值为键，各字符串的长度为值，组成键值对
\>>> newdict = {key:len(key) **for** key **in** listdemo}
\>>> newdict
{'Google': 6, 'Runoob': 6, 'Taobao': 6}



提供三个数字，以三个数字为键，三个数字的平方为值来创建字典：

###### 实例

\>>> dic = {x: x**2 **for** x **in** (2, 4, 6)}
\>>> dic
{2: 4, 4: 16, 6: 36}
\>>> type(dic)
<**class** 'dict'>



### 集合推导式

集合推导式基本格式：

```
{ expression for item in Sequence }
或
{ expression for item in Sequence if conditional }
```



计算数字 1,2,3 的平方数：

###### 实例

\>>> setnew = {i**2 **for** i **in** (1,2,3)}
\>>> setnew
{1, 4, 9}



判断不是 abc 的字母并输出：

###### 实例

\>>> a = {x **for** x **in** 'abracadabra' **if** x **not** **in** 'abc'}
\>>> a
{'d', 'r'}
\>>> type(a)
<**class** 'set'>



### 元组推导式（生成器表达式）

元组推导式可以利用 range 区间、元组、列表、字典和集合等数据类型，快速生成一个满足指定需求的元组。

元组推导式基本格式：

```
(expression for item in Sequence )
或
(expression for item in Sequence if conditional )
```

元组推导式和列表推导式的用法也完全相同，只是元组推导式是用 **()** 圆括号将各部分括起来，而列表推导式用的是中括号 **[]**，另外元组推导式返回的结果是一个生成器对象。



例如，我们可以使用下面的代码生成一个包含数字 1~9 的元组：

###### 实例

\>>> a = (x **for** x **in** range(1,10))
\>>> a
<generator object <genexpr> at 0x7faf6ee20a50>  # 返回的是生成器对象

\>>> tuple(a)       # 使用 tuple() 函数，可以直接将生成器对象转换成元组
(1, 2, 3, 4, 5, 6, 7, 8, 9)





# 数据类型转换

有时候，我们需要对数据内置的类型进行转换，数据类型的转换，一般情况下你只需要将数据类型作为函数名即可。

Python 数据类型转换可以分为两种：

- 隐式类型转换 - 自动完成
- 显式类型转换 - 需要使用类型函数来转换

### 隐式类型转换

在隐式类型转换中，Python 会自动将一种数据类型转换为另一种数据类型，不需要我们去干预。

以下实例中，我们对两种不同类型的数据进行运算，较低数据类型（整数）就会转换为较高数据类型（浮点数）以避免数据丢失。



###### 实例

num_int = 123
num_flo = 1.23

num_new = num_int + num_flo

**print**("num_int 数据类型为:",type(num_int))
**print**("num_flo 数据类型为:",type(num_flo))

**print**("num_new 值为:",num_new)
**print**("num_new 数据类型为:",type(num_new))

以上实例输出结果为：

```
num_int 数据类型为: <class 'int'>
num_flo 数据类型为: <class 'float'>
num_new: 值为: 124.23
num_new 数据类型为: <class 'float'>
```

代码解析：

- 实例中我们对两个不同数据类型的变量 `num_int` 和 `num_flo` 进行相加运算，并存储在变量 `num_new` 中。
- 然后查看三个变量的数据类型。
- 在输出结果中，我们看到 `num_int` 是 `整型（integer）` ， `num_flo` 是 `浮点型（float）`。
- 同样，新的变量 `num_new` 是 `浮点型（float）`，这是因为 Python 会将较小的数据类型转换为较大的数据类型，以避免数据丢失。



我们再看一个实例，整型数据与字符串类型的数据进行相加：

###### 实例

num_int = 123
num_str = "456"

**print**("num_int 数据类型为:",type(num_int))
**print**("num_str 数据类型为:",type(num_str))

**print**(num_int+num_str)

以上实例输出结果为：

```
num_int 数据类型为: <class 'int'>
num_str 数据类型为: <class 'str'>
Traceback (most recent call last):
  File "/runoob-test/test.py", line 7, in <module>
    print(num_int+num_str)
TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

从输出中可以看出，整型和字符串类型运算结果会报错，输出 TypeError。 Python 在这种情况下无法使用隐式转换。

但是，Python 为这些类型的情况提供了一种解决方案，称为显式转换。



### 显式类型转换

在显式类型转换中，用户将对象的数据类型转换为所需的数据类型。 我们使用 int()、float()、str() 等预定义函数来执行显式类型转换。



**int()** 强制转换为整型：

###### 实例

x = int(1)   # x 输出结果为 1
y = int(2.8) # y 输出结果为 2
z = int("3") # z 输出结果为 3



**float()** 强制转换为浮点型：

###### 实例

x = float(1)     # x 输出结果为 1.0
y = float(2.8)   # y 输出结果为 2.8
z = float("3")   # z 输出结果为 3.0
w = float("4.2") # w 输出结果为 4.2



###### str()** 强制转换为字符串类型：

###### 实例

x = str("s1") # x 输出结果为 's1'
y = str(2)    # y 输出结果为 '2'
z = str(3.0)  # z 输出结果为 '3.0'



整型和字符串类型进行运算，就可以用强制类型转换来完成：

###### 实例

num_int = 123
num_str = "456"

**print**("num_int 数据类型为:",type(num_int))
**print**("类型转换前，num_str 数据类型为:",type(num_str))

num_str = int(num_str)    # 强制转换为整型
**print**("类型转换后，num_str 数据类型为:",type(num_str))

num_sum = num_int + num_str

**print**("num_int 与 num_str 相加结果为:",num_sum)
**print**("sum 数据类型为:",type(num_sum))

以上实例输出结果为：

```
num_int 数据类型为: <class 'int'>
类型转换前，num_str 数据类型为: <class 'str'>
类型转换后，num_str 数据类型为: <class 'int'>
num_int 与 num_str 相加结果为: 579
sum 数据类型为: <class 'int'>
```



以下几个内置的函数可以执行数据类型之间的转换。这些函数返回一个新的对象，表示转换的值。

| 函数                                                         | 描述                                                |
| :----------------------------------------------------------- | :-------------------------------------------------- |
| [int(x [,base\])](https://www.runoob.com/python3/python-func-int.html) | 将x转换为一个整数                                   |
| [float(x)](https://www.runoob.com/python3/python-func-float.html) | 将x转换到一个浮点数                                 |
| [complex(real [,imag\])](https://www.runoob.com/python3/python-func-complex.html) | 创建一个复数                                        |
| [str(x)](https://www.runoob.com/python3/python-func-str.html) | 将对象 x 转换为字符串                               |
| [repr(x)](https://www.runoob.com/python3/python-func-repr.html) | 将对象 x 转换为表达式字符串，即供解释器读取的形式   |
| [eval(str)](https://www.runoob.com/python3/python-func-eval.html) | 用来计算在字符串中的有效Python表达式,并返回一个对象 |
| [tuple(s)](https://www.runoob.com/python3/python3-func-tuple.html) | 将序列 s 转换为一个元组                             |
| [list(s)](https://www.runoob.com/python3/python3-att-list-list.html) | 将序列 s 转换为一个列表                             |
| [set(s)](https://www.runoob.com/python3/python-func-set.html) | 转换为可变集合                                      |
| [dict(d)](https://www.runoob.com/python3/python-func-dict.html) | 创建一个字典。d 必须是一个 (key, value)元组序列。   |
| [frozenset(s)](https://www.runoob.com/python3/python-func-frozenset.html) | 转换为不可变集合                                    |
| [chr(x)](https://www.runoob.com/python3/python-func-chr.html) | 将一个整数转换为一个字符                            |
| [ord(x)](https://www.runoob.com/python3/python-func-ord.html) | 将一个字符转换为它的整数值                          |
| [hex(x)](https://www.runoob.com/python3/python-func-hex.html) | 将一个整数转换为一个十六进制字符串                  |
| [oct(x)](https://www.runoob.com/python3/python-func-oct.html) | 将一个整数转换为一个八进制字符串                    |

例如：

```
a = 1
print(type(repr(a)))

>>> <class 'str'>   # 返回的是一个对象的string形式
```



# 迭代器与生成器

------

## 迭代器

迭代是 Python 最强大的功能之一，是访问集合元素的一种方式。

迭代器是一个可以记住遍历的位置的对象。

迭代器对象从集合的第一个元素开始访问，直到所有的元素被访问完结束。迭代器只能往前不会后退。

迭代器有两个基本的方法：**iter()** 和 **next()**。

字符串，列表或元组对象都可用于创建迭代器：

```
a = list(i for i in range(9) if (i % 2) == 0)
a = iter(a)
print(next(a))
# print(*a)    ## 这里使用*号也可以展开整个a
# print([j for j in a])     ## 这里print函数中传入的是一个迭代器表达式，而print函数需要传入的参数为
for j in a:
    print(j)
```



### 创建一个迭代器

把一个类作为一个迭代器使用需要在类中实现两个方法 __iter__() 与 __next__() 。

如果你已经了解的面向对象编程，就知道类都有一个构造函数，Python 的构造函数为 __init__(), 它会在对象初始化的时候执行。

更多内容查阅：[Python3 面向对象](https://www.runoob.com/python3/python3-class.html)

__iter__() 方法返回一个特殊的迭代器对象， 这个迭代器对象实现了 __next__() 方法并通过 StopIteration 异常标识迭代的完成。

__next__() 方法（Python 2 里是 next()）会返回下一个迭代器对象。

创建一个返回数字的迭代器，初始值为 1，逐步递增 1：

```
import time
class MyNumbers:
    def __init__(self):
        self.a = 0
    def __iter__(self):
        return self
    def __next__(self):
        x = self.a
        self.a += 1
        return x

myiter = MyNumbers()
myiter = iter(myiter)
print(next(myiter))
for i in myiter:
    if i == 20:
        raise StopIteration
    print(i)
    time.sleep(1)
    
>>>
0
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
```



## 生成器

在 Python 中，使用了 **yield** 的函数被称为生成器（generator）。

**yield** 是一个关键字，用于定义生成器函数，生成器函数是一种特殊的函数，可以在迭代过程中逐步产生值，而不是一次性返回所有结果。

跟普通函数不同的是，生成器是一个返回迭代器的函数，只能用于迭代操作，更简单点理解生成器就是一个迭代器。

当在生成器函数中使用 **yield** 语句时，函数的执行将会暂停，并将 **yield** 后面的表达式作为当前迭代的值返回。

然后，每次调用生成器的 **next()** 方法或使用 **for** 循环进行迭代时，函数会从上次暂停的地方继续执行，直到再次遇到 **yield** 语句。这样，生成器函数可以逐步产生值，而不需要一次性计算并返回所有结果。

调用一个生成器函数，返回的是一个迭代器对象。

```
import sys
import random

def get_random_value():
    value = random.randint(0, 10)
    yield value

if __name__ == "__main__":
    try:
        while True:
            b = input("需要随机数请输入1不需要输入0:\t")
            c = 1 if b != '0' else 0
            if c:
                print(next(get_random_value()))
            else:
                raise StopIteration
    except Exception as e:
        print("程序结束")
```





# 函数

函数是组织好的，可重复使用的，用来实现单一，或相关联功能的代码段。

函数能提高应用的模块性，和代码的重复利用率。你已经知道Python提供了许多内建函数，比如print()。但你也可以自己创建函数，这被叫做用户自定义函数。

------

## 定义一个函数

你可以定义一个由自己想要功能的函数，以下是简单的规则：

- 函数代码块以 **def** 关键词开头，后接函数标识符名称和圆括号 **()**。
- 任何传入参数和自变量必须放在圆括号中间，圆括号之间可以用于定义参数。
- 函数的第一行语句可以选择性地使用文档字符串—用于存放函数说明。
- 函数内容以冒号 **:** 起始，并且缩进。
- **return [表达式]** 结束函数，选择性地返回一个值给调用方，不带表达式的 return 相当于返回 None。

![img](https://www.runoob.com/wp-content/uploads/2014/05/py-tup-10-26-1.png)

------

### 语法

Python 定义函数使用 def 关键字，一般格式如下：

```
def 函数名（参数列表）:
    函数体
```

默认情况下，参数值和参数名称是按函数声明中定义的顺序匹配起来的。



## 匿名函数

Python 使用 **lambda** 来创建匿名函数。

所谓匿名，意即不再使用 **def** 语句这样标准的形式定义一个函数。

- **lambda** 只是一个表达式，函数体比 **def** 简单很多。
- lambda 的主体是一个表达式，而不是一个代码块。仅仅能在 lambda 表达式中封装有限的逻辑进去。
- lambda 函数拥有自己的命名空间，且不能访问自己参数列表之外或全局命名空间里的参数。
- 虽然 lambda 函数看起来只能写一行，却不等同于 C 或 C++ 的内联函数，内联函数的目的是调用小函数时不占用栈内存从而减少函数调用的开销，提高代码的执行速度。

### 语法

lambda 函数的语法只包含一个语句，如下：

```
lambda [arg1 [,arg2,.....argn]]:expression
```



![1696683414782](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1696683414782.png)

lambda匿名函数应用：

```python
y = 0   # 初始化y的值
add_func = lambda x, y : x + y  # 定义匿名函数

# func2 = add_two(lambda x, y : x + y)
while y < 100: 
    y = add_func(1, y)  # 实例化函数并且传入参数，再将计算过后的值赋给y
    print(y)
```



###### 匿名函数应用在闭包中

```python
def add(n):               #闭包操作，先定义一个函数
    return lambda x:x+n   #闭包操作，再定义一个函数并且返回一个值

add2 = add(5)
print(add2(15))	

#这种应用就相等于：

def add(n):
    def second_add(x):
        return x + n
    return second_add
add1 = add(5)
print(add1(15))
```

闭包就是函数之间嵌套，即一个函数内部可以继续定义其他函数，将外部函数作为其嵌套内部函数的引用环境，并且在内部函数处理期间外部函数的引用环境一直保持不变



## return 语句

**return [表达式]** 语句用于退出函数，选择性地向调用方返回一个表达式。不带参数值的 return 语句返回 None。之前的例子都没有示范如何返回数值，以下实例演示了 return 语句的用法：

###### 实例(Python 3.0+)

```
#!/usr/bin/python3
 
# 可写函数说明
def sum( arg1, arg2 ):
   # 返回2个参数的和."
   total = arg1 + arg2
   print ("函数内 : ", total)
   return total
 
# 调用sum函数
total = sum( 10, 20 )
print ("函数外 : ", total)
```

以上实例输出结果：

```
函数内 :  30
函数外 :  30
```



## 强制位置参数

Python3.8 新增了一个函数形参语法 / 用来指明函数形参必须使用指定位置参数，不能使用关键字参数的形式。

在以下的例子中，形参 a 和 b 必须使用指定位置参数，c 或 d 可以是位置形参或关键字形参，而 e 和 f 要求为关键字形参:

```
def f(a, b, /, c, d, *, e, f):
    print(a, b, c, d, e, f)
```

以下使用方法是正确的:

```
f(10, 20, 30, d=40, e=50, f=60)
```

以下使用方法会发生错误:

```
f(10, b=20, c=30, d=40, e=50, f=60)   # b 不能使用关键字参数的形式
f(10, 20, 30, 40, 50, f=60)           # e 必须使用关键字参数的形式
```



## 函数类型

[python中的类型提示(定义函数时加入箭�?>)_python中一个函数用一个箭头指向一个变�?CSDN博客](https://blog.csdn.net/leviopku/article/details/105236840) <

主要用于提示传入的参数的数据类型以及输出的数据类型，单纯能使得代码的可阅读性增强，输入数据的类型不同并不会影响程序的正常执行

具体语法形式：

```python
def add(a:int, b:int) -> int:
    return a+b
```

![img](E:\Markdown\markdown\python.assets\6daeaf66c9ec34e448ddf6aff312f373.png)

# 数据结构

本章节我们主要结合前面所学的知识点来介绍Python数据结构。

------

## 列表

Python中列表是可变的，这是它区别于字符串和元组的最重要的特点，一句话概括即：列表可以修改，而字符串和元组不能。

以下是 Python 中列表的方法：

| 方法              | 描述                                                         |
| :---------------- | :----------------------------------------------------------- |
| list.append(x)    | 把一个元素添加到列表的结尾，相当于 a[len(a):] = [x]。        |
| list.extend(L)    | 通过添加指定列表的所有元素来扩充列表，相当于 a[len(a):] = L。 |
| list.insert(i, x) | 在指定位置插入一个元素。第一个参数是准备插入到其前面的那个元素的索引，例如 a.insert(0, x) 会插入到整个列表之前，而 a.insert(len(a), x) 相当于 a.append(x) 。 |
| list.remove(x)    | 删除列表中值为 x 的第一个元素。如果没有这样的元素，就会返回一个错误。 |
| list.pop([i])     | 从列表的指定位置移除元素，并将其返回。如果没有指定索引，a.pop()返回最后一个元素。元素随即从列表中被移除。（方法中 i 两边的方括号表示这个参数是可选的，而不是要求你输入一对方括号，你会经常在 Python 库参考手册中遇到这样的标记。） |
| list.clear()      | 移除列表中的所有项，等于del a[:]。                           |
| list.index(x)     | 返回列表中第一个值为 x 的元素的索引。如果没有匹配的元素就会返回一个错误。 |
| list.count(x)     | 返回 x 在列表中出现的次数。                                  |
| list.sort()       | 对列表中的元素进行排序。(原地操作)                           |
| list.reverse()    | 倒排列表中的元素。                                           |
| list.copy()       | 返回列表的浅复制，等于a[:]。                                 |

例子

```python
import random
a = list(i for i in range(3))
a.append(11)
print("apend过后的结果：",a)

b = list(i for i in range(2))
a.extend(b)
print("extend过后的结果", a)

a.insert(random.randint(0, 10), -1)    ## insert（插入的数据， 插入数据的位置）
print("insert过后的结果：", a)

a.remove(1)
print("remove列表中的第一个1的结果：", a)

a.pop(-3)  ## 从列表的指定位置移除元素，并将其返回。如果没有指定索引，a.pop()返回最后一个元素。元素随即从列表中被移除。
print("pop倒数第三个元素的结果：", a)

b.clear()
print("clear清除b的所有元素的结果：", b)

index_3 = a.index(2)
print("index索引数字三的结果：", index_3)

count_3 = a.count(2)
print("count数3出现的次数：", count_3)

a.sort()  ## 列表原地排序操作
print("原地排序操作的结果：", a)

a.reverse()
print("翻转列表的结果：", a)

c = a.copy()
c[1] = 99
print("拷贝过后的a：", a)
print("拷贝过后的c：", c)
print("足以证明copy函数是浅拷贝")

>>>
apend过后的结果： [0, 1, 2, 11]
extend过后的结果 [0, 1, 2, 11, 0, 1]
insert过后的结果： [0, 1, -1, 2, 11, 0, 1]
remove列表中的第一个1的结果： [0, -1, 2, 11, 0, 1]
pop倒数第三个元素的结果： [0, -1, 2, 0, 1]
clear清除b的所有元素的结果： []
index索引数字三的结果： 2
count数3出现的次数： 1
原地排序操作的结果： [-1, 0, 0, 1, 2]
翻转列表的结果： [2, 1, 0, 0, -1]
拷贝过后的a： [2, 1, 0, 0, -1]
拷贝过后的c： [2, 99, 0, 0, -1]
```





## 将列表当做堆栈使用

列表方法使得列表可以很方便的作为一个堆栈来使用，堆栈作为特定的数据结构，最先进入的元素最后一个被释放（后进先出）。用 append() 方法可以把一个元素添加到堆栈顶。用不指定索引的 pop() 方法可以把一个元素从堆栈顶释放出来。例如：

###### 实例

>>> stack = [3, 4, 5]
>>> stack.append(6)
>>> stack.append(7)
>>> stack
[3, 4, 5, 6, 7]
>>> stack.pop()
7
>>> stack
[3, 4, 5, 6]
>>> stack.pop()
6
>>> stack.pop()
5
>>> stack
[3, 4]



## 将列表当作队列使用

也可以把列表当做队列**(先进先出)**用，只是在队列里第一加入的元素，第一个取出来；但是拿列表用作这样的目的效率不高。在列表的最后添加或者弹出元素速度快，然而在列表里插入或者从头部弹出速度却不快（因为所有其他的元素都得一个一个地移动）。

###### 实例

>>> from collections import deque
>>> queue = deque(["Eric", "John", "Michael"])
>>> queue.append("Terry")           # Terry arrives
>>> queue.append("Graham")          # Graham arrives
>>> queue.popleft()                 # The first to arrive now leaves
'Eric'
>>> queue.popleft()                 # The second to arrive now leaves
'John'
>>> queue                           # Remaining queue in order of arrival
deque(['Michael', 'Terry', 'Graham'])



## 列表推导式

列表推导式提供了从序列创建列表的简单途径。通常应用程序将一些操作应用于某个序列的每个元素，用其获得的结果作为生成新列表的元素，或者根据确定的判定条件创建子序列。

每个列表推导式都在 for 之后跟一个表达式，然后有零到多个 for 或 if 子句。返回结果是一个根据表达从其后的 for 和 if 上下文环境中生成出来的列表。如果希望表达式推导出一个元组，就必须使用括号。

这里我们将列表中每个数值乘三，获得一个新的列表：

```
>>> vec = [2, 4, 6]
>>> [3*x **for** x **in** vec]
[6, 12, 18]
```

现在我们玩一点小花样：

```
>>> [[x, x**2] **for** x **in** vec]
[[2, 4], [4, 16], [6, 36]]
```

这里我们对序列里每一个元素逐个调用某方法：

###### 实例



```
>>> freshfruit = ['  banana', '  loganberry ', 'passion fruit  ']
>>> [weapon.strip() **for** weapon **in** freshfruit]
['banana', 'loganberry', 'passion fruit']
```

我们可以用 if 子句作为过滤器：

```
>>> [3*x **for** x **in** vec **if** x > 3]
[12, 18]
>>> [3*x **for** x **in** vec **if** x < 2]
[]


```

以下是一些关于循环和其它技巧的演示：

```
import numpy as np
count = 9
array_1 = np.empty((count, count))
result = [x * y for x in range(1, 10) for y in range(1, 10)]
iter_list = iter(result)
for i in range(count):
    for j in range(count):
        array_1[i][j] = next(iter_list)
print(array_1)

>>>
[[ 1.  2.  3.  4.  5.  6.  7.  8.  9.]
 [ 2.  4.  6.  8. 10. 12. 14. 16. 18.]
 [ 3.  6.  9. 12. 15. 18. 21. 24. 27.]
 [ 4.  8. 12. 16. 20. 24. 28. 32. 36.]
 [ 5. 10. 15. 20. 25. 30. 35. 40. 45.]
 [ 6. 12. 18. 24. 30. 36. 42. 48. 54.]
 [ 7. 14. 21. 28. 35. 42. 49. 56. 63.]
 [ 8. 16. 24. 32. 40. 48. 56. 64. 72.]
 [ 9. 18. 27. 36. 45. 54. 63. 72. 81.]]
 
```

或者这样 

## 嵌套列表表达式

```
count = 9
result = [x * y for x in range(1, 10) for y in range(1, 10)]
list_2 = [[i for i in result[j * 9-9: j*9]]for j in range(1, 10)]
print(list_2)

```



列表推导式可以使用复杂表达式或嵌套函数：

```
>>> [str(round(355/113, i)) **for** i **in** range(1, 6)]
['3.1', '3.14', '3.142', '3.1416', '3.14159']
```



## 遍历技巧

在字典中遍历时，关键字和对应的值可以使用 items() 方法同时解读出来：

```
>>> knights = {'gallahad': 'the pure', 'robin': 'the brave'}
>>> **for** k, v **in** knights.items():
...     **print**(k, v)
...
gallahad the pure
robin the brave

在序列中遍历时，索引
```

位置和对应值可以使用 enumerate() 函数同时得到：

```
>>> **for** i, v **in** enumerate(['tic', 'tac', 'toe']):
...     **print**(i, v)
...
0 tic
1 tac
2 toe
```

同时遍历两个或更多的序列，可以使用 zip() 组合：



```
>>> questions = ['name', 'quest', 'favorite color']
>>> answers = ['lancelot', 'the holy grail', 'blue']
>>> **for** q, a **in** zip(questions, answers):
...     **print**('What is your {0}?  It is {1}.'.format(q, a))
...

What **is** your name?  It **is** lancelot.
What **is** your quest?  It **is** the holy grail.
What **is** your favorite color?  It **is** blue.
```



## 参阅文档

- [Python3 列表](https://www.runoob.com/python3/python3-list.html)
- [Python3 元组](https://www.runoob.com/python3/python3-tuple.html)
- [Python3 字典](https://www.runoob.com/python3/python3-dictionary.html)



# 输入和输出

在前面几个章节中，我们其实已经接触了 Python 的输入输出的功能。本章节我们将具体介绍 Python 的输入输出。

## 

## 输出格式美化

Python两种输出值的方式: 表达式语句和 print() 函数。

第三种方式是使用文件对象的 write() 方法，标准输出文件可以用 sys.stdout 引用。



如果你希望输出的形式更加多样，可以使用 str.format() 函数来格式化输出值。

如果你希望将输出的值转成字符串，可以使用 repr() 或 str() 函数来实现。

- **str()：** 函数返回一个用户易读的表达形式。
- **repr()：** 产生一个解释器易读的表达形式。



###### 例如

>>> s = 'Hello, Runoob'
>>> str(s)
>>>'Hello, Runoob'
>>> repr(s)
>>>"'Hello, Runoob'"
>>> str(1/7)
>>>'0.14285714285714285'
>>> x = 10 * 3.25
>>> y = 200 * 200
>>> s = 'x 的值为： ' + repr(x) + ',  y 的值为：' + repr(y) + '...'
>>> print(s)
>>>x 的值为： 32.5,  y 的值为：40000...
>>>
>>> #  repr() 函数可以转义字符串中的特殊字符
>>>... hello = 'hello, runoob\n'
>>> hellos = repr(hello)
>>> print(hellos)
>>>'hello, runoob\n'
>>> # repr() 的参数可以是 Python 的任何对象
>>>... repr((x, y, ('Google', 'Runoob')))
>>>"(32.5, 40000, ('Google', 'Runoob'))"

这里有两种方式输出一个平方与立方的表:

```
>>> **for** x **in** range(1, 11):
...     **print**(repr(x).rjust(2), repr(x*x).rjust(3), end=' ')
...     # 注意前一行 'end' 的使用
...     **print**(repr(x*x*x).rjust(4))
...
 1   1    1
 2   4    8
 3   9   27
 4  16   64
 5  25  125
 6  36  216
 7  49  343
 8  64  512
 9  81  729
10 100 1000
```



```
>>> **for** x **in** range(1, 11):
...     **print**('{0:2d} {1:3d} {2:4d}'.format(x, x*x, x*x*x))
...
 1   1    1
 2   4    8
 3   9   27
 4  16   64
 5  25  125
 6  36  216
 7  49  343
 8  64  512
 9  81  729
10 100 1000
```

**注意：**在第一个例子中, 每列间的空格由 print() 添加。

这个例子展示了字符串对象的 **rjust() 方法, 它可以将字符串靠右, 并在左边填充空格**。

还有类似的方法, 如 ljust() 和 center()。 这些方法并不会写任何东西, 它们仅仅返回新的字符串。

另一个方法 zfill(), 它会在数字的左边填充 0，如下所示：

```
>>> '12'.zfill(5)
'00012'
>>> '-3.14'.zfill(7)
'-003.14'
>>> '3.14159265359'.zfill(5)
'3.14159265359'
```

str.format() 的基本使用如下:

\>>> **print**('{}网址： "{}!"'.format('菜鸟教程', 'www.runoob.com'))
菜鸟教程网址： "www.runoob.com!"

括号及其里面的字符 (称作格式化字段) 将会被 format() 中的参数替换。

在括号中的数字用于指向传入对象在 format() 中的位置，如下所示：

\>>> **print**('{0} 和 {1}'.format('Google', 'Runoob'))
Google 和 Runoob
\>>> **print**('{1} 和 {0}'.format('Google', 'Runoob'))
Runoob 和 Google

如果在 format() 中使用了关键字参数, 那么它们的值会指向使用该名字的参数。



\>>> **print**('{name}网址： {site}'.format(name='菜鸟教程', site='www.runoob.com'))
菜鸟教程网址： www.runoob.com

位置及关键字参数可以任意的结合:

\>>> **print**('站点列表 {0}, {1}, 和 {other}。'.format('Google', 'Runoob', other='Taobao'))
站点列表 Google, Runoob, 和 Taobao。

**!a** (使用 **ascii()**), **!s** (使用 **str()**) 和 **!r** (使用 **repr()**) 可以用于在格式化某个值之前对其进行转化:

\>>> **import** math
\>>> **print**('常量 PI 的值近似为： {}。'.format(math.pi))
常量 PI 的值近似为： 3.141592653589793。
\>>> **print**('常量 PI 的值近似为： {!r}。'.format(math.pi))
常量 PI 的值近似为： 3.141592653589793。



可选项 **:** 和格式标识符可以跟着字段名。 这就允许对值进行更好的格式化。 下面的例子将 Pi 保留到小数点后三位：

\>>> **import** math
\>>> **print**('常量 PI 的值近似为 {0:.3f}。'.format(math.pi))
常量 PI 的值近似为 3.142。

在 **:** 后传入一个整数, 可以保证该域至少有这么多的宽度。 用于美化表格时很有用。

\>>> table = {'Google': 1, 'Runoob': 2, 'Taobao': 3}
\>>> **for** name, number **in** table.items():
...     **print**('{0:10} ==> {1:10d}'.format(name, number))
...
Google     ==>          1
Runoob     ==>          2
Taobao     ==>          3

如果你有一个很长的格式化字符串, 而你不想将它们分开, 那么在格式化时通过变量名而非位置会是很好的事情。

最简单的就是传入一个字典, 然后使用方括号 **[]** 来访问键值 :

\>>> table = {'Google': 1, 'Runoob': 2, 'Taobao': 3}
\>>> **print**('Runoob: {0[Runoob]:d}; Google: {0[Google]:d}; Taobao: {0[Taobao]:d}'.format(table))
Runoob: 2; Google: 1; Taobao: 3

也可以通过在 table 变量前使用 ***\*** 来实现相同的功能：

\>>> table = {'Google': 1, 'Runoob': 2, 'Taobao': 3}
\>>> **print**('Runoob: {Runoob:d}; Google: {Google:d}; Taobao: {Taobao:d}'.format(**table))
Runoob: 2; Google: 1; Taobao: 3

## pickle 模块

python的pickle模块实现了基本的数据序列和反序列化。（序列化指的将数据转换为课传输的字节序列过程）

通过pickle模块的序列化操作我们能够将程序中运行的对象信息保存到文件中去，永久存储。

通过pickle模块的反序列化操作，我们能够从文件中创建上一次程序保存的对象。

基本接口：

```
pickle.dump(obj, file, [,protocol])
```

有了 pickle 这个对象, 就能对 file 以读取的形式打开:

```
x = pickle.load(file)
```

**注解：**从 file 中读取一个字符串，并将它重构为原来的python对象。

**file:** 类文件对象，有read()和readline()接口。



###### 实例 1

\#!/usr/bin/python3
**import** pickle

\# 使用pickle模块将数据对象保存到文件

```
data1 = {'a': [1, 2.0, 3, 4+6j],
         'b': ('string', u'Unicode string'),
         'c': None}

selfref_list = [1, 2, 3]
selfref_list.append(selfref_list)

output = open('data.pkl', 'wb')

# Pickle dictionary using protocol 0.
pickle.dump(data1, output)

# Pickle the list using the highest protocol available.
pickle.dump(selfref_list, output, -1)

output.close()

## 
```

###### 实例 2

```
import pickle
import pprint
count = 9
result = [x * y for x in range(1, 10) for y in range(1, 10)]
list_2 = [[i for i in result[j * 9-9: j*9]]for j in range(1, 10)]

file = open(r"D:\\GZR_practice\\list_2.txt", 'wb+')

pickle.dump(list_2, file)    ## 将list_2列表对象的数据序列化写入文件中，同时要注意，open打开文件的时候必须要以二进制的格式写入，因为dump函数序列化写入数据的时候是二进制数据，因此必须这样做
file.seek(0, 0)          ## 由于我们刚才写入了数据，此时指针的位置落在了文件的结尾，因此如果我们这时候读取它，将会什么都读不到，seek（指针移动字符数，指针起始位置）
data2 = pickle.load(file)   ## 从序列化文件中读取数据
pprint.pprint(data2)        ## 美化输出

file.close()

```



## OS文件/目录方法

[Python3 OS 文件/目录方法 | 菜鸟教程 (runoob.com)](https://www.runoob.com/python3/python3-os-file-methods.html)





## 错误与异常

在刚学习 Python 编程时，经常会看到一些报错信息，在前面我们没有提及，这章节我们会专门介绍。

Python 有两种错误很容易辨认：语法错误和异常。

**Python assert（断言）用于判断一个表达式，在表达式条件为 false 的时候触发异常。**

![img](https://static.runoob.com/images/mix/assets-py.webp)



### 语法错误

python的语法错误就是规则或约定错误，具体含义就是语句以及代码违反语言规则，导致编译器或解释器无法正确解析代码。 常见的语法错误包括拼写错误、缺少分号或括号、使用错误的关键词等等。

如下实例

> > > **while** True **print**('Hello world')
> >   File "<stdin>", line 1, **in** ?
> >     **while** True **print**('Hello world')
> >                    ^
> > SyntaxError: invalid syntax

这个例子中，函数 print() 被检查到有错误，是它前面缺少了一个冒号 **:** 。

语法分析器指出了出错的一行，并且在最先找到的错误的位置标记了一个小小的箭头。



### 异常

即使python程序的语法是正确的，在运行它的时候，也有可能发生错误，这种运行期间检测到的错误被称为异常。（简单点来说就是代码逻辑错误）

###### 实例

> > 10 * (1/0)             # 0 不能作为除数，触发异常
> Traceback (most recent call last):
>   File "<stdin>", line 1, **in** ?
> ZeroDivisionError: division by zero
>
> > >> 4 + spam*3             # spam 未定义，触发异常
> > Traceback (most recent call last):
> >   File "<stdin>", line 1, **in** ?
> > NameError: name 'spam' **is** **not** defined
> >
> > > >> '2' + 2               # int 不能与 str 相加，触发异常
> > > Traceback (most recent call last):
> > >   File "<stdin>", line 1, **in** <module>
> > > TypeError: can only concatenate str (**not** "int") to str

异常以不同的类型出现，这些类型都作为信息的一部分打印出来: 例子中的类型有 ZeroDivisionError，NameError 和 TypeError。

错误信息的前面部分显示了异常发生的上下文，并以调用栈的形式显示具体信息。



### 异常处理

#### try/except

异常捕捉可以使用 **try/except** 语句。

![img](https://www.runoob.com/wp-content/uploads/2019/07/try_except.png)

以下例子中，让用户输入一个合法的整数，但是允许用户中断这个程序（使用 Control-C 或者操作系统提供的方法）。用户中断的信息会引发一个 KeyboardInterrupt 异常。

```
while True:
    try:
        x = int(input("请输入一个数字: "))
        break
    except ValueError:
        print("您输入的不是数字，请再次尝试输入！")
```

try 语句按照如下方式工作；

- 首先，执行 try 子句（在关键字 try 和关键字 except 之间的语句）。
- 如果没有异常发生，忽略 except 子句，try 子句执行后结束。
- 如果在执行 try 子句的过程中发生了异常，那么 try 子句余下的部分将被忽略。如果异常的类型和 except 之后的名称相符，那么对应的 except 子句将被执行。
- 如果一个异常没有与任何的 except 匹配，那么这个异常将会传递给上层的 try 中。

一个 try 语句可能包含多个except子句，分别来处理不同的特定的异常。最多只有一个分支会被执行。

处理程序将只针对对应的 try 子句中的异常进行处理，而不是其他的 try 的处理程序中的异常。

一个except子句可以同时处理多个异常，这些异常将被放在一个括号里成为一个元组，例如:

```
except (RuntimeError, TypeError, NameError):
    pass
```

最后一个except子句可以忽略异常的名称，它将被当作通配符使用。你可以使用这种方法打印一个错误信息，然后再次把异常抛出。

```
import sys

try:
    f = open('myfile.txt')
    s = f.readline()
    i = int(s.strip())
except OSError as err:
    print("OS error: {0}".format(err))
except ValueError:
    print("Could not convert data to an integer.")
except:
    print("Unexpected error:", sys.exc_info()[0])
    raise
```

#### try/except...else

**try**:
    f = open('myfile.txt')
    s = f.readline()
    i = int(s.strip())
**except** OSError **as** err:
    **print**("OS error: {0}".format(err))
**except** ValueError:
    **print**("Could not convert data to an integer.")
**except**:
    **print**("Unexpected error:", sys.exc_info()[0])
    **raise**

### try/except...else

**try/except** 语句还有一个可选的 **else** 子句，如果使用这个子句，那么必须放在所有的 except 子句之后。

else 子句将在 try 子句没有发生任何异常的时候执行。

![img](https://www.runoob.com/wp-content/uploads/2019/07/try_except_else.png)

以下实例在 try 语句中判断文件是否可以打开，如果打开文件时正常的没有发生异常则执行 else 部分的语句，读取文件内容：

```
for arg in sys.argv[1:]:
    try:
        f = open(arg, 'r')
    except IOError:
        print('cannot open', arg)
    else:
        print(arg, 'has', len(f.readlines()), 'lines')
        f.close()
```

使用 else 子句比把所有的语句都放在 try 子句里面要好，这样可以避免一些意想不到，而 except 又无法捕获的异常。

异常处理并不仅仅处理那些直接发生在 try 子句中的异常，而且还能处理子句中调用的函数（甚至间接调用的函数）里抛出的异常。例如:

> > > **def** this_fails():
> >         x = 1/0
> >
> > \>>> **try**:
> >         this_fails()
> >     **except** ZeroDivisionError **as** err:
> >         **print**('Handling run-time error:', err)
> >
> > Handling run-time error: int division **or** modulo by zero

### try-finally 语句

try-finally 语句无论是否发生异常都将执行最后的代码。

![img](https://www.runoob.com/wp-content/uploads/2019/07/try_except_else_finally.png)

以下实例中 finally 语句无论异常是否发生都会执行：

###### 实例

```
try:
    runoob()
except AssertionError as error:
    print(error)
else:
    try:
        with open('file.log') as file:
            read_data = file.read()
    except FileNotFoundError as fnf_error:
        print(fnf_error)
finally:
    print('这句话，无论异常是否发生都会执行。')
```



### 抛出异常

python使用raise语句抛出一个指定的异常

raise的语法如下：

```
raise [Exception [, args [, traceback]]]
```

以下实例如果 x 大于 5 就触发异常:

```
x = 10
if x > 5:
    raise Exception('x 不能大于 5。x 的值为: {}'.format(x))
```

执行以上代码会触发异常：

```
Traceback (most recent call last):
  File "test.py", line 3, in <module>
    raise Exception('x 不能大于 5。x 的值为: {}'.format(x))
Exception: x 不能大于 5。x 的值为: 10
```

raise 唯一的一个参数指定了要被抛出的异常。它必须是一个异常的实例或者是异常的类（也就是 Exception 的子类）。

如果你只想知道这是否抛出了一个异常，并不想去处理它，那么一个简单的 raise 语句就可以再次把它抛出。



### 用户自定义异常

你可以通过创建一个新的异常类来拥有自己的异常

```
from datetime import datetime
import traceback
import cv2
class MyError(Exception):    # 制作MyError异常类对象
    def __init__(self):
        self.return_value = datetime.now()
    def __str__(self):       # 返回对象的描述信息
        return repr(self.return_value)  ## 如果使用repr

try:
    raise MyError
except Exception as e:
    print(e)
    print(traceback.print_exc())   # traceback.print_exc用于追踪异常返回信息，并保存起来
    # 这里将追踪到的异常信息显示出来，但是并不会像出现异常一样停止程序，只是将异常输出打印出来

    print("""fasdfasdfqwe
    12312312
    653246345""")
    print(cv2.imread.__annotations__)
raise MyError            # 由于直接抛出异常所以程序会在检测到这个异常的时候立即停止程序
print("""fasdfasdfqwe
    12312312
    653246345""")
```



### 定义清理行为

try 语句还有另外一个可选的子句，它定义了无论在任何情况下都会执行的清理行为。 例如:

```
>>> try:
...     raise KeyboardInterrupt
... finally:
...     print('Goodbye, world!')
... 
Goodbye, world!
Traceback (most recent call last):
  File "<stdin>", line 2, in <module>
KeyboardInterrupt
```

以上例子不管 try 子句里面有没有发生异常，finally 子句都会执行。

如果一个异常在 try 子句里（或者在 except 和 else 子句里）被抛出，而又没有任何的 except 把它截住，那么这个异常会在 finally 子句执行后被抛出。

下面是一个更加复杂的例子（在同一个 try 语句里包含 except 和 finally 子句）:

```
>>> def divide(x, y):
        try:
            result = x / y
        except ZeroDivisionError:
            print("division by zero!")
        else:
            print("result is", result)
        finally:
            print("executing finally clause")
   
>>> divide(2, 1)
result is 2.0
executing finally clause
>>> divide(2, 0)
division by zero!
executing finally clause
>>> divide("2", "1")
executing finally clause
Traceback (most recent call last):
  File "<stdin>", line 1, in ?
  File "<stdin>", line 3, in divide
TypeError: unsupported operand type(s) for /: 'str' and 'str'
```



### 预定义的清理行为（指try中的finally）

一些对象定义了标准的清理行为，无论系统是否成功的使用了它，一旦不需要它了，那么这个标准的清理行为就会执行。也就是说类似于[with](https://blog.csdn.net/sazass/article/details/116668755)操作，当不需要的时候自动关闭

```
for line in open("myfile.txt"):
    print(line, end="")
```

以上这段代码的问题是，当执行完毕后，文件会保持打开状态，并没有被关闭。

关键词 with 语句就可以保证诸如文件之类的对象在使用完之后一定会正确的执行他的清理方法:

```
with open("myfile.txt") as f:
    for line in f:
        print(line, end="")
```



# 面向对象

## 面向对象技术简介

- **类(Class):** 用来描述具有相同的属性和方法的对象的集合。它定义了该集合中每个对象所共有的属性和方法。对象是类的实例。
- **方法：**类中定义的函数。
- **类变量：**类变量在整个实例化的对象中是公用的。类变量定义在类中且在函数体之外。类变量通常不作为实例变量使用。
- **数据成员：**类变量或者实例变量用于处理类及其实例对象的相关的数据。
- **方法重写：**如果从父类继承的方法不能满足子类的需求，可以对其进行改写，这个过程叫方法的覆盖（override），也称为方法的重写。
- **局部变量：**定义在方法中的变量，只作用于当前实例的类。
- **实例变量：**在类的声明中，属性是用变量来表示的，这种变量就称为实例变量，实例变量就是一个用 self 修饰的变量。
- **继承：**即一个派生类（derived class）继承基类（base class）的字段和方法。继承也允许把一个派生类的对象作为一个基类对象对待。例如，有这样一个设计：一个Dog类型的对象派生自Animal类，这是模拟"是一个（is-a）"关系（例图，Dog是一个Animal）。
- **实例化：**创建一个类的实例，类的具体对象。
- **对象：**通过类定义的数据结构实例。对象包括两个数据成员（类变量和实例变量）和方法。

和其它编程语言相比，Python 在尽可能不增加新的语法和语义的情况下加入了类机制。

Python中的类提供了面向对象编程的所有基本功能：类的继承机制允许多个基类，派生类可以覆盖基类中的任何方法，方法中可以调用基类中的同名方法。

对象可以包含任意数量和类型的数据。



## 类定义

语法格式：

```
class ClassName:
    <statement-1>
    .
    .
    .
    <statement-N>
```



## 类对象

类对象支持两种操作：属性引用和实例化。

属性引用使用和 Python 中所有的属性引用一样的标准语法：**obj.name**。

类对象创建后，类命名空间中所有的命名都是有效属性名。所以如果类定义是这样:

```
#!/usr/bin/python3
 
class MyClass:
    """一个简单的类实例"""
    i = 12345
    def f(self):
        return 'hello world'
 
# 实例化类
x = MyClass()
 
# 访问类的属性和方法
print("MyClass 类的属性 i 为：", x.i)
print("MyClass 类的方法 f 输出为：", x.f())
```



类有一个名为 __init__() 的特殊方法（**构造方法**），该方法在类实例化时会自动调用，像下面这样：

类定义了 __init__() 方法，类的实例化操作会自动调用 __init__() 方法。如下实例化类 MyClass，对应的 __init__() 方法就会被调用

当然， __init__() 方法可以有参数，参数通过 __init__() 传递到类的实例化操作上。例如:

```
#!/usr/bin/python3
 
class Complex:
    def __init__(self, realpart, imagpart):
        self.r = realpart
        self.i = imagpart
x = Complex(3.0, -4.5)
print(x.r, x.i)   # 输出结果：3.0 -4.5
```



### self代表类的实例，而非类

类的方法与普通的函数只有一个特别的区别——它们必须有一个额外的**第一个参数名称**, 按照惯例它的名称是 self。

```
class Test:
    def prt(self):
        print(self)
        print(self.__class__)   # 查看类对象所属类别
 
t = Test()
t.prt()

>>>
<__main__.Test instance at 0x100771878>   # 指明了类实例的所属类以及内存地址
__main__.Test
```



## 类的方法

在类的内部，使用 **def** 关键字来定义一个方法，与一般函数定义不同，类方法必须包含参数 self, 且为第一个参数，self 代表的是类的实例。





## 继承

Python 同样支持类的继承，如果一种语言不支持继承，类就没有什么意义。派生类的定义如下所示:

```
class DerivedClassName(BaseClassName):
    <statement-1>
    .
    .
    .
    <statement-N>
```

子类（派生类 DerivedClassName）会**继承父类（基类 BaseClassName）的属性和方法。**

BaseClassName（实例中的基类名）必须与派生类定义在一个作用域内。除了类，还可以用表达式，基类定义在另一个模块中时这一点非常有用:

```
class DerivedClassName(modname.BaseClassName):
```



### 多继承

Python同样有限的支持多继承形式。多继承的类定义形如下例:

```
class DerivedClassName(Base1, Base2, Base3):
    <statement-1>
    .
    .
    .
    <statement-N>
```

需要注意圆括号中父类的顺序，若是父类中有相同的方法名，而在子类使用时未指定，python从左至右搜索 即方法在子类中未找到时，从左到右查找父类中是否包含方法。



### 方法重写

如果你的父类方法的功能不能满足你的需求，你可以在子类重写你父类的方法，实例如下：

```
#!/usr/bin/python3
 
class Parent:        # 定义父类
   def myMethod(self):
      print ('调用父类方法')
 
class Child(Parent): # 定义子类
   def myMethod(self):
      print ('调用子类方法')
 
c = Child()          # 子类实例
c.myMethod()         # 子类调用重写方法
super(Child,c).myMethod() #用子类对象调用父类已被覆盖的方法

>>>
调用子类方法
调用父类方法
```



### 子类继承父类构造函数说明

如果在子类中需要父类的构造方法就需要显式地调用父类的构造方法，或者不重写父类的构造方法。

子类不重写 **__init__**，实例化子类时，会自动调用父类定义的 **__init__**。

简单总结就是：

情况一：**子类需要自动调用父类的方法：**子类不重写__init__()方法，实例化子类后，会自动调用父类的__init__()的方法。

情况二：**子类不需要自动调用父类的方法：**子类重写__init__()方法，实例化子类后，将不会自动调用父类的__init__()的方法。

情况三：**子类重写__init__()方法又需要调用父类的方法：**使用super关键词：





### 调用父类方法

在Python中，`super(type[, object-or-type])`是调用父类方法的函数

* type：指定从哪个类开始查找父类的方法，在python3中默认会是当前创建的cls
* object-or-type： 绑定类，一般默认为self， 让执行父类的函数的时候知道父类处理的值将会保存到哪个类中

```python
class grandfather(object):
    def __init__(self):
        print("hello, i am grandfater")

class father(grandfather):
    def __init__(self):
        print("hi, i am father")
        super(father, self).__init__()


class son(father):
    def __init__(self):
        super(son, self).__init__()      # 从son类开始查找父类函数
        super(father, self).__init__()   # 从father类中查找父类的函数
        print("hello, i am son")

if __name__ == "__main__":
    son1 = son()
```



### 私有变量/私有方法

```
#!/usr/bin/python3
 
class Site:
    def __init__(self, name, url):
        self.name = name       # public
        self.__url = url   # private
 
    def who(self):
        print('name  : ', self.name)
        print('url : ', self.__url)
 
    def __foo(self):          # 私有方法
        print('这是私有方法')
 
    def foo(self):            # 公共方法
        print('这是公共方法')
        self.__foo()
 
x = Site('菜鸟教程', 'www.runoob.com')
x.who()        # 正常输出
x.foo()        # 正常输出
x.__foo()      # 报错
```

![img](https://www.runoob.com/wp-content/uploads/2014/05/F5C2A308-3A88-42B4-B575-C719EB8F1CC4.jpg)

#### 类的专有方法：

- **__init__ :** 构造函数，在生成对象时调用
- **__del__ :** 析构函数，释放对象时使用
- **__repr__ :** 打印，转换
- **__setitem__ :** 按照索引赋值
- **__getitem__:** 按照索引获取值
- **__len__:** 获得长度
- **__cmp__:** 比较运算
- **__call__:** 函数调用
- **__add__:** 加运算
- **__sub__:** 减运算
- **__mul__:** 乘运算
- **__truediv__:** 除运算
- **__mod__:** 求余运算
- **__pow__:** 乘方



### 运算符重载

重载（Overloading）是指在同一个作用域内，可以有多个同名函数或方法，但它们的参数列表必须不同。通过重载，可以根据不同的参数类型或参数个数来调用不同的函数或方法。

```
#!/usr/bin/python3
 
class Vector:
   def __init__(self, a, b):
      self.a = a
      self.b = b
 
   def __str__(self):    __str__方法用于指定类的实例对象在被打印时的输出方式，并且__str__方法返回一个字符串，用于描述对象的信息 
      return 'Vector (%d, %d)' % (self.a, self.b)
      
# 运算符重载，意味者在某个类的方法中拦截内置的操作，当类的实例出现在内置操作中时，python将自动调用你的方法，并使用方法的返回值进行相应操作的结果。
   def __add__(self,other):  
   # 比如这里的操作就是当对象的属性进行相加操作的时候，将传入的加数与原来的属性递归重新使用
      return Vector(self.a + other.a, self.b + other.b)
 
v1 = Vector(2,10)
v2 = Vector(5,-2)
print (v1 + v2)   # 这里的print方法在实例化调用了两个实例，并且按照运算符重载将加法做成了将两个实例的元素递归相加，并且在print打印两个对象的运算成果的时候，使用了__str__方法中的信息

>>>
Vector(7,8)

```

运算符重载，意味着在某个类的方法中拦截内置的操作，当类的实例出现在内置操作中时，Python会自动调用你的方法，并且你的方法的返回值会作为相应操作的结果，

1）运算符重载让类拦截常规的Python操作

2）类可重载所有Python表达式运算符

3）类也可重载打印、函数调用、属性访问等内置运算

4）重载使类实例的行为更接近内置类型

5）重载是通过在一个类中提供特殊名称的方法来实现的

我们通过一个简单的例子来看下构造函数（__init__）和表达式（__sub__）的运算符重载，来理解上面的内容，具体代码如下：

![img](https://pic3.zhimg.com/80/v2-df770956ad9c8a54a735506e7bb48fee_720w.webp)



### **索引和分片：__getitem__和__setitem__**

我们先来看索引和分片的运算符重载，当实例X出现在X[i]这样的索引运算中时，Python会调用这个实例继承的__getitem__方法，把X作为第一位参数传入，并且将方括号内的索引值传递给第二个参数，具体代码如下：



![img](https://pic3.zhimg.com/80/v2-18514f378e752fbd7fa3729df516bdaa_720w.webp)



__getitem__是查看类属性的值，可以通过索引，而__setitem__是更新类属性的值，主要是针对有键值对的，具体代码实例如下：

![img](https://pic2.zhimg.com/80/v2-2d9103034d76e3cd24a72ff69500d359_720w.webp)

### **索引迭代：__getitem__**

也就是说，如果有该方法存在，那该类的对象，是可迭代的，例如，承接上面的例子，可以通过list（）函数直接查看实例X中的内容

![img](https://pic3.zhimg.com/80/v2-5bec80a6a57d058f54c4db481749310e_720w.webp)

在这里是一个概念或者说技巧，后续在使用中可考虑



### **可迭代对象：__iter__和__next__**

虽然上面说的__getitem__可用，但是Python中所有的迭代上下文都会先尝试__iter__方法，再尝试__getitem__,也就是说我们应该优先调整__iter__方法

通过__iter__和__next__方法的结合使用，可以实现类实例的迭代，具体代码如下：

![img](https://pic4.zhimg.com/80/v2-47a5bcd549a079e2c4e24920b4fde937_720w.webp)

以上是创建了一个类，接下来通过实例来使用迭代功能

![img](https://pic4.zhimg.com/80/v2-9e9bc0d50e451b7bf4aa23c054662ddf_720w.webp)



[Python小白高阶： 运算符重载 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/162931696)



### **属性访问：__getattr__和__setattr__**

__getattr__是访问属性，__setattr__是修改属性

先创建一个简单的类，如果要访问不存在的属性，系统会出现提示信息，具体代码如下：

![img](https://pic1.zhimg.com/80/v2-29bfb5e3a58f5ed5368c7874fc163cb8_720w.webp)

对于类，如果你直接添加属性和值是可以的，但是可以通过__setattr__来屏蔽，还是承接上面代码的实例，代码调整如下：

![img](https://pic4.zhimg.com/80/v2-45604d4eb4c806e66e4b3ba586b38063_720w.webp)

对于以上代码，运行结果如下：

![img](https://pic3.zhimg.com/80/v2-aa40998aad12d22d580b0546ca7ee4ea_720w.webp)



### **字符串显示：__repr__和__str__**

关于字符串显示，前面章节中有说明，也有用到__repr__来设计打印类的结果，那与__str__有什么区别呢？

**__str__：**会首先被打印操作和str内置函数尝试（print运行的内部等价形式），它通常应当返回一个用户友好的显示

**__repr__：**用于所有其他的场景，如果没有定义__str__则打印操作也会使用__repr__，也就是说可以用于任何地方

通过以下代码，会更好的说明这一点：

首先，看下，如果没有定义__str__和__repr__的情况下会是什么情况

![img](https://pic4.zhimg.com/80/v2-77595d56ce425f4516aa3c4a7cc3202f_720w.webp)

你会发现，直接调用实例或者打印实例，都是显示一串代码，它是说明该实例的内存地址

如果先定义__repr__，看下结果：

![img](https://pic3.zhimg.com/80/v2-a94e01c340eb8454c9df7020fe06e6d6_720w.webp)

再定义__str__看下结果：

![img](https://pic1.zhimg.com/80/v2-8ad9c911c278602e4aaaa44a92cc5de4_720w.webp)



### **调用表达式：__call__**

通过定义__call__可以实现实例不同的调用，具体代码如下：

![img](https://pic3.zhimg.com/80/v2-c1399e39ee6dbacd17d40422a7a30e8a_720w.webp)









# 命名空间和作用域 

## 命名空间

命名空间是从名称到对象的映射，大部分的命名空间都是通过python的字典来实现的

命名空间提供了在项目中避免名字冲突的一种方法。各个命名空间是独立的，没有任何关系的，所以一个命名空间中不能有重名，但不同的命名空间是可以重名而没有任何影响。

我们举一个计算机系统中的例子，一个文件夹(目录)中可以包含多个文件夹，每个文件夹中不能有相同的文件名，但不同文件夹中的文件可以重名。

![img](https://www.runoob.com/wp-content/uploads/2019/09/0129A8E9-30FE-431D-8C48-399EA4841E9D.jpg)



一般有三种命名空间：

- **内置名称（built-in names**）， Python 语言内置的名称，比如函数名 abs、char 和异常名称 BaseException、Exception 等等。
- **全局名称（global names）**，模块中定义的名称，记录了模块的变量，包括函数、类、其它导入的模块、模块级的变量和常量。
- **局部名称（local names）**，函数中定义的名称，记录了函数的变量，包括函数的参数和局部定义的变量。（类中定义的也是）

![img](https://www.runoob.com/wp-content/uploads/2014/05/types_namespace-1.png)

### 命名空间查找顺序:

假设我们要使用变量 runoob，则 Python 的查找顺序为：**局部的命名空间 -> 全局命名空间 -> 内置命名空间**。

如果找不到变量 runoob，它将放弃查找并引发一个 NameError 异常

### 命名空间的生命周期：

命名空间的生命周期取决于对象的作用域，如果对象执行完成，则该命名空间的生命周期就结束。

因此，我们无法从外部命名空间访问内部命名空间的对象。



## 作用域

作用域就是一个 Python 程序可以直接访问命名空间的正文区域。

在一个 python 程序中，直接访问一个变量，会从内到外依次访问所有的作用域直到找到，否则会报未定义的错误。

Python 中，程序的变量并不是在哪个位置都可以访问的，访问权限决定于这个变量是在哪里赋值的。

变量的作用域决定了在哪一部分程序可以访问哪个特定的变量名称。Python 的作用域一共有4种，分别是：

有四种作用域：

- **L（Local）**：最内层，包含局部变量，比如一个函数/方法内部。
- **E（Enclosing）**：嵌套作用域，包含了非局部(non-local)也非全局(non-global)的变量。比如两个嵌套函数，一个函数（或类） A 里面又包含了一个函数 B ，那么对于 B 中的名称来说 A 中的作用域就为 nonlocal。
- **G（Global）**：当前脚本的最外层，比如当前模块的全局变量。
- **B（Built-in）**： 包含了内建的变量/关键字等，最后被搜索。
- 内置作用域（B）是python事先定义的内置模块，例如built-in 模块内的变量，程序启动之后由python虚拟机自动加载，在程序的任何地方都可以使用，例如print函数，随着解释器存在或消亡。

规则顺序： **L –> E –> G –> B**。

在局部找不到，便会去局部外的局部找（例如闭包），再找不到就会去全局找，再者去内置中找。

![img](https://www.runoob.com/wp-content/uploads/2014/05/1418490-20180906153626089-1835444372.png)

```
Copy`# 1.函数嵌套：
def myfun(i):
    a = [1, 2, 3] #  a 所在范围为嵌套作用域
    def add():
        a.append(i)
        return a
    return add

test = myfun(4)
print(test())

输出结果：[1, 2, 3, 4]`
```



### 全局变量和局部变量

定义在函数内部的变量拥有一个局部作用域，定义在函数外的拥有全局作用域。

局部变量只能在其被声明的函数内部访问，而全局变量可以在整个程序范围内访问。调用函数时，所有在函数内声明的变量名称都将被加入到作用域中。如下实例：

```
#!/usr/bin/python3
 
total = 0 # 这是一个全局变量
# 可写函数说明
def sum( arg1, arg2 ):
    #返回2个参数的和."
    total = arg1 + arg2 # total在这里是局部变量.
    print ("函数内是局部变量 : ", total)
    return total
 
#调用sum函数
sum( 10, 20 )
print ("函数外是全局变量 : ", total)

>>>
函数内是局部变量 :  30
函数外是全局变量 :  0
```



### global 和 nonlocal关键字

当内部作用域想修改外部作用域的变量时，就要用到 global 和 nonlocal 关键字了。

以下实例修改全局变量 num：

```
#!/usr/bin/python3
 
num = 1
def fun1():
    global num  # 需要使用 global 关键字声明
    print(num) 
    num = 123
    print(num)
fun1()
print(num)

>>>
1
123
123

```

以下实例修改嵌套作用域变量：

```
def a():
    num = 10
    def b():
        nonlocal num  # 对嵌套环境的变量num进行修改，这里的nonlocal是声明num变量的作用域为嵌套环境
        num = 200
        print(num)
        num = 300
    print(num)
    b()
    print(num)

a()

>>>
10
200
300
```



# 标准库概览

[Python3 标准库概览 | 菜鸟教程 (runoob.com)](https://www.runoob.com/python3/python3-stdlib.html)



## 命令行参数

通用工具脚本经常调用命令行参数。这些命令行参数以链表形式存储于 sys 模块的 argv 变量。例如在命令行中执行 "python demo.py one two three" 后可以得到以下输出结果:

```
# 使用终端来传入参数
import sys
class myClass(object):
    def __init__(self, a, b):
        self.a = int(a)
        self.b = int(b)

    def print(self, num):
        if int(num) >= 1:
            print(f"{self.a} * {self.b} = {self.a * self.b}")
        else:
            print(self.a)

value = sys.argv[1:]    # 读取执行程序时使用的参数，生成列表，第一个为文件名
obj = myClass(value[0], value[1])
obj.print(value[2])
```



## 访问 互联网

Python urllib 库用于操作网页 URL，并对网页的内容进行抓取处理。

本文主要介绍 Python3 的 urllib。

urllib 包 包含以下几个模块：

- **urllib.request** - 打开和读取 URL。
- **urllib.error** - 包含 urllib.request 抛出的异常。
- **urllib.parse** - 解析 URL。
- **urllib.robotparser** - 解析 robots.txt 文件。



urllib.request 定义了一些打开 URL 的函数和类，包含授权验证、重定向、浏览器 cookies等。

urllib.request 可以模拟浏览器的一个请求发起过程。

我们可以使用 urllib.request 的 urlopen 方法来打开一个 URL，语法格式如下：

```
urllib.request.urlopen(url, data=None, [timeout, ]*, cafile=None, capath=None, cadefault=False, context=None)
```

**url**：url 地址。

**data**：发送到服务器的其他数据对象，默认为 None。

**timeout**：设置访问超时时间。

**cafile 和 capath**：cafile 为 CA 证书， capath 为 CA 证书的路径，使用 HTTPS 需要用到。

**cadefault**：已经被弃用。

**context**：ssl.SSLContext类型，用来指定 SSL 设置。

```
from urllib.request import urlopen
import pprint
pprint.pprint(urlopen("http://www.baidu.com").read())    # 实例化URL网站对象，并使用read函数读取对象的HTML实体代码
```

read() 是读取整个网页内容，我们可以指定读取的长度

除了 read() 函数外，还包含以下两个读取网页内容的函数：

- **readline()** - 读取文件的一行内容

```
from urllib.request import urlopen

myURL = urlopen("https://www.runoob.com/")
print(myURL.readline()) #读取一行内容
```

- **readlines()** - 读取文件的全部内容，它会把读取的内容赋值给一个列表变量。

```
from urllib.request import urlopen

myURL = urlopen("https://www.runoob.com/")
lines = myURL.readlines()
for line in lines:
    print(line) 
```



我们在对网页进行抓取时，经常需要判断网页是否可以正常访问，这里我们就可以使用 getcode() 函数获取网页状态码，返回 200 说明网页正常，返回 404 说明网页不存在:

```
import urllib.request

myURL1 = urllib.request.urlopen("https://www.runoob.com/")
print(myURL1.getcode())   # 200

try:
    myURL2 = urllib.request.urlopen("https://www.runoob.com/no.html")
except urllib.error.HTTPError as e:
    if e.code == 404:
        print(404)   # 404
```

更多网页状态码可以查阅：<https://www.runoob.com/http/http-status-codes.html>。



URL 的编码与解码可以使用 **urllib.request.quote()** 与 **urllib.request.unquote()** 方法：

```
import urllib.request 

encode_url = urllib.request.quote("https://www.runoob.com/")  # 编码
print(encode_url)

unencode_url = urllib.request.unquote(encode_url)    # 解码
print(unencode_url)

>>>
https%3A//www.runoob.com/
https://www.runoob.com/
```



### 模拟头部信息

我们抓取网页一般需要对 headers（网页头信息）进行模拟，这时候需要使用到 urllib.request.Request 类：

```
class urllib.request.Request(url, data=None, headers={}, origin_req_host=None, unverifiable=False, method=None)
```

- **url**：url 地址。
- **data**：发送到服务器的其他数据对象，默认为 None。
- **headers**：HTTP 请求的头部信息，字典格式。
- **origin_req_host**：请求的主机地址，IP 或域名。
- **unverifiable**：很少用整个参数，用于设置网页是否需要验证，默认是False。。
- **method**：请求方法， 如 GET、POST、DELETE、PUT等。

```
import urllib.request
import urllib.parse

url = "http://www.baidu.com"
headers = {'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/110.0.0.0 Safari/537.36 Edg/110.0.1587.63'}
request = urllib.request.Request(url=url, headers=headers)
# urlopen() 方法可以实现最基本的请求发起，但这几个简单的参数并不足以构建一个完整的请求，如果请求中需要加入 headers 等信息，我们就可以利用更强大的 Request 类来构建一个请求。
response = urllib.request.urlopen(request)
print(response.read())
```



表单 POST 传递数据，我们先创建一个表单，代码如下，我这里使用了 PHP 代码来获取表单的数据：

```
import urllib.request
import urllib.parse

url = 'https://www.runoob.com/try/py3/py3_urllib_test.php'  # 提交到表单页面
data = {'name':'RUNOOB', 'tag' : '菜鸟教程'}   # 提交数据
header = {
    'User-Agent':'Mozilla/5.0 (X11; Fedora; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36'
}   #头部信息
data = urllib.parse.urlencode(data).encode('utf8')  # 对参数进行编码，解码使用 urllib.parse.urldecode
request=urllib.request.Request(url, data, header)   # 请求处理
reponse=urllib.request.urlopen(request).read()      # 读取结果

fh = open("./urllib_test_post_runoob.html","wb")    # 将文件写入到当前目录中
fh.write(reponse)
fh.close()
```

urlparse() 函数可以将 URL 解析成 ParseResult 对象。对象中包含了六个元素，分别为：

```
协议（scheme） 
域名（netloc） 
路径（path） 
路径参数（params） 
查询参数（query） 
片段（fragment）
```



## SMTP发送邮件

有几个模块用于访问互联网以及处理网络通信协议。其中最简单的两个是用于处理从 urls 接收的数据的 urllib.request 以及用于发送电子邮件的 smtplib:

```python
import smtplib
from email.mime.text import MIMEText
from email.header import Header

from_email = "2971209213@qq.com"
to_email = "2975602606@qq.com"
pass_word = "ixqywlvcxqwmddci"
smtp_server = "smtp.qq.com"
try:
    msg = MIMEText("""        # 实例化发送邮件的文本对象
    Beware the Ides of March.hello I am best.\n
    You have more important should to do !
    """)
    msg["From"] = Header("M0PVHS <2971209213@qq.com>")   # 按照qq邮箱的协议书写规则必须在文本对象中加上From（发送人）、To（接收人）、Subject （邮件主题）
    msg["To"] = Header("SHADOW <2975602606@qq.com>")
    msg["Subject"] = Header("For your suggest")
    smtp = smtplib.SMTP_SSL(smtp_server)   # 实例化对象并连接QQ邮箱服务端
    smtp.set_debuglevel(1)                 # 打印和服务器的交互信息
    smtp.login(from_email, pass_word)   # ixqywlvcxqwmddci
    smtp.sendmail(from_email, to_email, msg.as_string())
    smtp.quit()

except Exception as e:
    print(e)
```



### 一、smtplib模块：

主要通过SMTP类与邮件系统进行交互。使用方法如下：

#### 1.实例化一个SMTP对象：

　　s = smtplib.SMTP(邮件服务地址，端口号)

　　s = smtplib.SMTP_SSL(邮件服务地址，端口号)

#### 2.登陆邮件，权限验证：

　　s.login(用户名，密码)

#### 3.发送邮件：

　　s.sendmail(发件人邮箱，收件人邮箱，发送内容)

#### 4.断开连接：

　　s.close()



### 二、email模块：

　　email模块：支持发送的邮件内容为纯文本、HTML内容、图片、附件。email模块中有几大类来针对不同的邮件内容形式，常用如下：

　　MIMEText：（MIME媒体类型）内容形式为纯文本、HTML页面。

　　MIMEImage：内容形式为图片。

　　MIMEMultupart：多形式组合，可包含文本和附件。

 

#### 每一类对应的导入方式：

　　from email.mime.text import MIMEText

　　from email.mime.image import MIMEImage

　　from email.mime.multipart import MIMEMultipart

 

### 三、MIMEText:

　　MIMEText(msg,type,chartset)

　　msg：文本内容

　　type：文本类型默认为plain（纯文本）

　　 发送HTML格式的时候，修改为html，但同时要求msg的内容也是html的格式。

　　chartset：文本编码，中文为“utf-8”

　　# 构造TEXT格式的消息

　　msg = MIMEText("hello.text","plain","utf-8")

　　msg["Subject"] = "xxxxx"

　　msg["From"] = "xxxx"

　　msg["To"] = "xxxx"

　　#发送以上构造的邮件内容要使用as_string将构造的邮件内容转换为string形式。

　　s.sendmail("xxx","xxx",msg.as_string)

 

## re正则表达式

[正则表达式学习笔记（超级详细！！！）| 有用的小知识_正则表达式?!_LLLLQZ的博客-CSDN博客](https://blog.csdn.net/LLLLQZ/article/details/118278287)

[正则表达式 – 教程 | 菜鸟教程 (runoob.com)](https://www.runoob.com/regexp/regexp-tutorial.html)





# python简单项目

[Python3 实例 | 菜鸟教程 (runoob.com)](https://www.runoob.com/python3/python3-examples.html) 







# 正则表达式

[Python3 正则表达式 | 菜鸟教程 (runoob.com)](https://www.runoob.com/python3/python3-reg-expressions.html#flags)



## re.match函数

re.match 尝试从字符串的起始位置匹配一个模式，如果不是起始位置匹配成功的话，match()就返回none。

**函数语法**：

```
re.match(pattern, string, flags=0)
```

函数参数说明：

| 参数    | 描述                                                         |
| :------ | :----------------------------------------------------------- |
| pattern | 匹配的正则表达式                                             |
| string  | 要匹配的字符串。                                             |
| flags   | 标志位，用于控制正则表达式的匹配方式，如：是否区分大小写，多行匹配等等。参见：[正则表达式修饰符 - 可选标志](https://www.runoob.com/python3/python3-reg-expressions.html#flags) |

实例：

```
import re
print(re.match(r"baidu", "www.baidu.com"))  # re.match是从字符串的开头进行匹配，如果在开头就不匹配，那就是不匹配，返回的是None，然而前面匹配到了后，后边多出来的字符就不管了
print(re.findall(r"baidu", "www.baidu.com"))  # 全文匹配，并且返回匹配的字符串的列表
print(re.match(r"baidu", "www.baidu.com").span())  # re.match返回匹配到的对象，.span方法返回匹配到的对象在原句中的开始以及结束位置	

>>>
None
['baidu']
(4, 9)
```

我们可以使用group(num) 或 groups() 匹配对象函数来获取匹配表达式。

| 匹配对象方法 | 描述                                                         |
| :----------- | :----------------------------------------------------------- |
| group(num=0) | 匹配的整个表达式的字符串，group() 可以一次输入多个组号，在这种情况下它将返回一个包含那些组所对应值的元组。 |
| groups()     | 返回一个包含所有小组字符串的元组，从 1 到 所含的小组号。     |

```
print(re.match(r"^(\w*)\sand\s(\w*)", "hello and word good").group())

# 获取匹配到的字符串分组，这里的1指的就是匹配到的第一个分组  （分组指的是小括号中的字符串）
print(re.match(r"^(\w*)\sand\s(\w*)", "hello and word good").group(1))

# 这里的2指的就是匹配到的第二个分组
print(re.match(r"^(\w*)\sand\s(\w*)", "hello and word good").group(2))

>>>
hello and word
hello
word
```







## re.search方法

re.search 扫描整个字符串并返回第一个成功的匹配。

函数语法：

```
re.search(pattern, string, flags=0)
```

函数参数说明：

| 参数    | 描述                                                         |
| :------ | :----------------------------------------------------------- |
| pattern | 匹配的正则表达式                                             |
| string  | 要匹配的字符串。                                             |
| flags   | 标志位，用于控制正则表达式的匹配方式，如：是否区分大小写，多行匹配等等。参见：[正则表达式修饰符 - 可选标志](https://www.runoob.com/python3/python3-reg-expressions.html#flags) |

匹配成功re.search方法返回一个匹配的对象，否则返回None。

我们可以使用group(num) 或 groups() 匹配对象函数来获取匹配表达式。



```
print(re.search(r"^(\w*)\sand\s(\w*)", "hello and word good").group())
print(re.search(r"^(\w*)\sand\s(\w*)", "hello and word good").group(1))
print(re.search(r"^(\w*)\sand\s(\w*)", "hello and word good").group(2))

>>>
hello and word
hello
word
```



## re.match与re.search的区别

re.match 只匹配字符串的开始，如果字符串开始不符合正则表达式，则匹配失败，函数返回 None，而 re.search 匹配整个字符串，直到找到一个匹配。

```
#!/usr/bin/python3
 
import re
 
line = "Cats are smarter than dogs"
 
matchObj = re.match( r'dogs', line, re.M|re.I)
if matchObj:
   print ("match --> matchObj.group() : ", matchObj.group())
else:
   print ("No match!!")
 
matchObj = re.search( r'dogs', line, re.M|re.I)
if matchObj:
   print ("search --> matchObj.group() : ", matchObj.group())
else:
   print ("No match!!")
   
>>>
No match!!
search --> matchObj.group() :  dogs

```





## 检索和替换

Python 的re模块提供了re.sub用于替换字符串中的匹配项。

语法：

```
re.sub(pattern, repl, string, count=0, flags=0)
```

参数：

- pattern : 正则中的模式字符串。
- repl : 替换的字符串，也可为一个函数。
- string : 要被查找替换的原始字符串。
- count : 模式匹配后替换的最大次数，默认 0 表示替换所有的匹配。
- flags : 编译时用的匹配模式，数字形式。

```
import re
sub = re.sub(r"(\w+) \1", r'\1', "hello hello word good")
print(sub)

>>>hello word good
```

`这里的\1指代的是第一个匹配的分组`

```
#!/usr/bin/python
 
import re
 
# 将匹配的数字乘以 2
def double(matched):
    value = int(matched.group('value'))
    return str(value * 2)
 
s = 'A23G4HFD567'
print(re.sub('(?P<value>\d+)', double, s))

# 这里的正则表达式的?P<name>指的是将匹配到的分组命名为name

>>>A46G8HFD1134

```



## compile 函数

compile 函数用于编译正则表达式，生成一个正则表达式（ Pattern ）对象，供 match() 和 search() 这两个函数使用。

语法格式为：

```
re.compile(pattern[, flags])
```

参数：

- pattern : 一个字符串形式的正则表达式
- flags 可选，表示匹配模式，比如忽略大小写，多行模式等，具体参数为：
- - re.I 忽略大小写

    - re.L 表示特殊字符集 \w, \W, \b, \B, \s, \S 依赖于当前环境
    - re.M 多行模式
    - re.S 即为' . '并且包括换行符在内的任意字符（' . '不包括换行符）
    - re.U 表示特殊字符集 \w, \W, \b, \B, \d, \D, \s, \S 依赖于 Unicode 字符属性数据库
    - re.X 为了增加可读性，忽略空格和' # '后面的注释

```
import re
s = 'A23G4HFD567'
m = re.compile("(?P<value>\d+)"， re.l)   # 编译正则表达式，并生成正则对象
def two_price(match_value):
    value = int(match_value.group("value"))
    return str(value ** 2)

value = m.sub(two_price, s)
group_value = m.findall(s)
print(group_value)
print(value)
```





## findall

在字符串中找到正则表达式所匹配的所有子串，并返回一个列表，如果有多个匹配模式，则返回元组列表，如果没有找到匹配的，则返回空列表。

**注意：** match 和 search 是匹配一次 findall 匹配所有。

```
import re
s = 'A23G4HFD567'
m = re.compile("(?P<value>\d+)")   # 编译正则表达式，并生成正则对象，并将匹配的分组命名为name
def two_price(match_value):
    value = int(match_value.group("value"))
    return str(value ** 2)

value = m.sub(two_price, s)    # 这里的m.sub替代匹配的字符，并返回match对象，match对象才能使用group、span等方法
group_value = m.findall(s)  # findall函数找到所有匹配的字符，并且以列表的方式返回
match_value = m.search(s)   # match函数和search函数都是匹配一次的findall则是匹配所有
print(group_value)
print(value)
print(match_value)

>>>
['23', '4', '567']
A529G16HFD321489
<re.Match object; span=(1, 3), match='23'>

```

语法格式为：

```
re.findall(pattern, string, flags=0)
或
pattern.findall(string[, pos[, endpos]])
```

参数：

- **pattern** 匹配模式。
- **string** 待匹配的字符串。
- **pos** 可选参数，指定字符串的起始位置，默认为 0。
- **endpos** 可选参数，指定字符串的结束位置，默认为字符串的长度。

查找字符串中的所有数字：

```
import re
 
result1 = re.findall(r'\d+','runoob 123 google 456')
 
pattern = re.compile(r'\d+')   # 查找数字
result2 = pattern.findall('runoob 123 google 456')
result3 = pattern.findall('run88oob123google456', 0, 10)
 
print(result1)
print(result2)
print(result3)

>>>
['123', '456']
['123', '456']
['88', '12']
```



多个匹配模式，返回元组列表：

```
import re

result = re.findall(r'(\w+)=(\d+)', 'set width=20 and height=10')
print(result)

>>>
[('width', '20'), ('height', '10')]
```





## re.finditer

和 findall 类似，在字符串中找到正则表达式所匹配的所有子串，并把它们作为一个迭代器返回。

```
re.finditer(pattern, string, flags=0)
```

参数：

| 参数    | 描述                                                         |
| :------ | :----------------------------------------------------------- |
| pattern | 匹配的正则表达式                                             |
| string  | 要匹配的字符串。                                             |
| flags   | 标志位，用于控制正则表达式的匹配方式，如：是否区分大小写，多行匹配等等。参见：[正则表达式修饰符 - 可选标志](https://www.runoob.com/python3/python3-reg-expressions.html#flags) |

```
import re
 
it = re.finditer(r"\d+","12a32bc43jf3") 
for match in it: 
    print (match.group() )
    
>>>
12 
32 
43 
3
```





## re.split

split 方法按照能够匹配的子串将字符串分割后返回列表，它的使用形式如下：

```
re.split(pattern, string[, maxsplit=0, flags=0])
```

参数：

| 参数     | 描述                                                         |
| :------- | :----------------------------------------------------------- |
| pattern  | 匹配的正则表达式                                             |
| string   | 要匹配的字符串。                                             |
| maxsplit | 分割次数，maxsplit=1 分割一次，默认为 0，不限制次数。        |
| flags    | 标志位，用于控制正则表达式的匹配方式，如：是否区分大小写，多行匹配等等。参见：[正则表达式修饰符 - 可选标志](https://www.runoob.com/python3/python3-reg-expressions.html#flags) |

```
import re
# compile_obj = re.compile("([a-zA-Z]+)")
compile_obj = re.compile("(\w+)")

str1 = "boj bojb bjoa bajser bajo"
matched = re.split(compile_obj, str1)
print([i for i in matched if i not in [" ", '']])


>>>
['boj', 'bojb', 'bjoa', 'bajser', 'bajo']
```



# CGI编程

------

## 什么是CGI

CGI 目前由NCSA维护，NCSA定义CGI如下：

CGI(Common Gateway Interface),通用网关接口,它是一段程序,运行在服务器上如：HTTP服务器，提供同客户端HTML页面的接口。

------

## 网页浏览

为了更好的了解CGI是如何工作的，我们可以从在网页上点击一个链接或URL的流程：

- 1、使用你的浏览器访问URL并连接到HTTP web 服务器。
- 2、Web服务器接收到请求信息后会解析URL，并查找访问的文件在服务器上是否存在，如果存在返回文件的内容，否则返回错误信息。
- 3、浏览器从服务器上接收信息，并显示接收的文件或者错误信息。

CGI程序可以是Python脚本，PERL脚本，SHELL脚本，C或者C++程序等。

------

## CGI架构图

![cgiarch](https://www.runoob.com/wp-content/uploads/2013/11/Cgi01.png)



​	



# mysql.connector

**MySQL 是最流行的关系型数据库管理系统， 而mysql-connector** 是 **MySQL** 官方提供的驱动器。



### 创建数据库连接

可以使用下列的代码进行连接

```
mydb = mysql.connector.connect(   # 与数据库建立连接
    host='localhost',
    user='root',
    passwd='153120',
    port=3306
)
```

其中host、user、passwd都是必须的



### 创建数据库

创建数据库可以分为4步：

1.连接数据库

2.实例化游标

3.使用游标的execute方法将sql命令写入

4.使用数据库连接对象的commit方法来提交sql命令，从而实现执行命令

```
import  mysql.connector

mydb = mysql.connector.connect(   # 与数据库建立连接
    host='localhost',
    user='root',
    passwd='153120',
    port=3306
)
mycursor = mydb.cursor()   # 实例化游标对象
sql = "create database mysql_connector"  # 编辑创建数据库的sql命令

mycursor.execute(sql)   
# 执行sql命令，返回命令的影响数据库的行数，即操作返回的结果个数为int类型
# 而真正的返回值存储到了cursor对象中，需要使用fetchone等方法才能获得
# 执行sql命令，但这种操作是临时的，如果没用commit方法提交所有命令操作，那么所有的sql操作都是无效的，当程序执行完后sql操作会失效

mydb.commit()    
# 提交事务，当是使用execute方法执行完sql命令过后，如果想要让sql命令对数据库的操作永久保存，就需要使用commit命令

mycursor.close()
mydb.close()

```



#### 游标

![img](https://img.jbzj.com/file_images/article/202001/20201691807311.png?20200691816)

一张图讲述游标的功能：

![img](https://img.jbzj.com/file_images/article/202001/20201691822657.png?20200691831)

图示说明：

![img](https://img.jbzj.com/file_images/article/202001/20201691858620.png?2020069197)

**使用游标的好处？**

如果不使用游标功能，直接使用select查询，会一次性将结果集打印到屏幕上，你无法针对结果集做第二次编程。使用游标功能后，我们可以将得到的结果先保存起来，然后可以随意进行自己的编程，得到我们最终想要的结果集。

```
import  mysql.connector
import pprint

mydb = mysql.connector.connect(   # 与数据库建立连接
        host='localhost',
        user='root',
        passwd='153120',
        port=3306
    )
mycursor = mydb.cursor()   # 实例化游标对象
    # sql = "create database mysql_connector"
try:
    sql = "use word_etc;"
    mycursor.execute(sql)
    sql = "select * from enwords limit 5;"
    mycursor.execute(sql)       # 当这个函数执行过后python就会将执行过后的结果存储到cursor的结果集中，当时用for来遍历这个对象的时候，其实就是在遍历游标的结果集
    print(mycursor.rowcount)    # 受影响的数据行数, 当需要更改数据的时候，这个函数能够获取受影响的数据行数
    pprint.pprint(mycursor.fetchall())   # 使用fetchall函数来获取结果的时候将会返回的是一个列表
    for i in mycursor:        ## 当使用了上面的fetchall方法来获取结果过后，游标就已经到了结果的下面，因此再使用for来遍历就会没有结果
        print(i)              # 返回元组，其实就相当于遍历了fetchall方法返回的列表
    mydb.commit()
except Exception as e:
    print(e)
    mydb.rollback()    # 回滚操作
finally:
    mycursor.close()
    mydb.close()


>>>
0      # 数据库受影响的行数
[('a',
  "n.(A)As 或 A's  安(ampere);(a) art.一;n.字母A /[军] Analog.Digital,模拟/数字 "
  '/(=account of) 帐上'),
 ('aaal', 'American Academy of Arts and Letters 美国艺术和文学学会'),
 ('aachen', ' 亚琛[德意志联邦共和国西部城市]'),
 ('aacs', 'Airways and Air Communications Service (美国)航路与航空通讯联络处'),
 ('aah',
  ' [军]Armored Artillery Howitzer,装甲榴弹炮;[军]Advanced Attack Helicopter,先进攻击直升机')]

```



[Python MySQL – mysql-connector 驱动 | 菜鸟教程 (runoob.com)](https://www.runoob.com/python3/python-mysql-connector.html)

后面的操作就与前面没什么区别了，但是要执行的命令不同罢了都是sql命令，sql命令可以使用python的字符串的处理方式



# pymysql

[Python3 MySQL 数据库连接 – PyMySQL 驱动 | 菜鸟教程 (runoob.com)](https://www.runoob.com/python3/python3-mysql.html)

## 执行事务

事务机制可以确保数据一致性。

事务应该具有4个属性：原子性、一致性、隔离性、持久性。这四个属性通常称为ACID特性。

- 原子性（atomicity）。一个事务是一个不可分割的工作单位，事务中包括的诸操作要么都做，要么都不做。
- 一致性（consistency）。事务必须是使数据库从一个一致性状态变到另一个一致性状态。一致性与原子性是密切相关的。
- 隔离性（isolation）。一个事务的执行不能被其他事务干扰。即一个事务内部的操作及使用的数据对并发的其他事务是隔离的，并发执行的各个事务之间不能互相干扰。
- 持久性（durability）。持续性也称永久性（permanence），指一个事务一旦提交，它对数据库中数据的改变就应该是永久性的。接下来的其他操作或故障不应该对其有任何影响。

Python DB API 2.0 的事务提供了两个方法 commit 或 rollback。

实例

实例(Python 3.0+)

>  SQL删除记录语句 sql = "DELETE FROM EMPLOYEE WHERE AGE > %s" % (20) try:    # 执行SQL语句    cursor.execute(sql)    # 向数据库提交    db.commit() except:    # 发生错误时回滚    db.rollback()

> 对于支持事务的数据库， 在Python数据库编程中，当游标建立之时，就自动开始了一个隐形的数据库事务。

> commit()方法游标的所有更新操作，rollback（）方法回滚当前游标的所有操作。每一个方法都开始了一个新的事务。





## 错误处理

DB API中定义了一些数据库操作的错误及异常，下表列出了这些错误和异常:

| 异常              | 描述                                                         |
| :---------------- | :----------------------------------------------------------- |
| Warning           | 当有严重警告时触发，例如插入数据是被截断等等。必须是 StandardError 的子类。 |
| Error             | 警告以外所有其他错误类。必须是 StandardError 的子类。        |
| InterfaceError    | 当有数据库接口模块本身的错误（而不是数据库的错误）发生时触发。 必须是Error的子类。 |
| DatabaseError     | 和数据库有关的错误发生时触发。 必须是Error的子类。           |
| DataError         | 当有数据处理时的错误发生时触发，例如：除零错误，数据超范围等等。 必须是DatabaseError的子类。 |
| OperationalError  | 指非用户控制的，而是操作数据库时发生的错误。例如：连接意外断开、 数据库名未找到、事务处理失败、内存分配错误等等操作数据库是发生的错误。 必须是DatabaseError的子类。 |
| IntegrityError    | 完整性相关的错误，例如外键检查失败等。必须是DatabaseError子类。 |
| InternalError     | 数据库的内部错误，例如游标（cursor）失效了、事务同步失败等等。 必须是DatabaseError子类。 |
| ProgrammingError  | 程序错误，例如数据表（table）没找到或已存在、SQL语句语法错误、 参数数量错误等等。必须是DatabaseError的子类。 |
| NotSupportedError | 不支持错误，指使用了数据库不支持的函数或API等。例如在连接对象上 使用.rollback()函数，然而数据库并不支持事务或者事务已关闭。 必须是DatabaseError的子类。 |

以下为异常的继承结构：

```
Exception
|__Warning
|__Error
   |__InterfaceError
   |__DatabaseError
      |__DataError
      |__OperationalError
      |__IntegrityError
      |__InternalError
      |__ProgrammingError
      |__NotSupportedError
```





# 	网络编程

## 什么是 Socket?

Socket又称"套接字"，应用程序通常通过"套接字"向网络发出请求或者应答网络请求，使主机间或者一台计算机上的进程间可以通讯。

------

## socket()函数

Python 中，我们用 socket() 函数来创建套接字，语法格式如下：

```
socket.socket([family[, type[, proto]]])
```

### 参数

- family: 套接字家族可以是 AF_UNIX 或者 AF_INET
- type: 套接字类型可以根据是面向连接的还是非连接分为`SOCK_STREAM`或`SOCK_DGRAM`
- proto: 一般不填默认为0.



## Socket 对象(内建)方法

| 函数                                 | 描述                                                         |
| :----------------------------------- | :----------------------------------------------------------- |
| 服务器端套接字                       |                                                              |
| s.bind()                             | 绑定地址（host,port）到套接字， 在AF_INET下,以元组（host,port）的形式表示地址。 |
| s.listen()                           | 开始TCP监听。backlog指定在拒绝连接之前，操作系统可以挂起的最大连接数量。该值至少为1，大部分应用程序设为5就可以了。 |
| s.accept()                           | 被动接受TCP客户端连接,(阻塞式)等待连接的到来                 |
| 客户端套接字                         |                                                              |
| s.connect()                          | 主动初始化TCP服务器连接，。一般address的格式为元组（hostname,port），如果连接出错，返回socket.error错误。 |
| s.connect_ex()                       | connect()函数的扩展版本,出错时返回出错码,而不是抛出异常      |
| 公共用途的套接字函数                 |                                                              |
| s.recv()                             | 接收TCP数据，数据以字符串形式返回，bufsize指定要接收的最大数据量。flag提供有关消息的其他信息，通常可以忽略。 |
| s.send()                             | 发送TCP数据，将string中的数据发送到连接的套接字。返回值是要发送的字节数量，该数量可能小于string的字节大小。 |
| s.sendall()                          | 完整发送TCP数据。将string中的数据发送到连接的套接字，但在返回之前会尝试发送所有数据。成功返回None，失败则抛出异常。 |
| s.recvfrom()                         | 接收UDP数据，与recv()类似，但返回值是（data,address）。其中data是包含接收数据的字符串，address是发送数据的套接字地址。 |
| s.sendto()                           | 发送UDP数据，将数据发送到套接字，address是形式为（ipaddr，port）的元组，指定远程地址。返回值是发送的字节数。 |
| s.close()                            | 关闭套接字                                                   |
| s.getpeername()                      | 返回连接套接字的远程地址。返回值通常是元组（ipaddr,port）。  |
| s.getsockname()                      | 返回套接字自己的地址。通常是一个元组(ipaddr,port)            |
| s.setsockopt(level,optname,value)    | 设置给定套接字选项的值。                                     |
| s.getsockopt(level,optname[.buflen]) | 返回套接字选项的值。                                         |
| s.settimeout(timeout)                | 设置套接字操作的超时期，timeout是一个浮点数，单位是秒。值为None表示没有超时期。一般，超时期应该在刚创建套接字时设置，因为它们可能用于连接的操作（如connect()） |
| s.gettimeout()                       | 返回当前超时期的值，单位是秒，如果没有设置超时期，则返回None。 |
| s.fileno()                           | 返回套接字的文件描述符。                                     |
| s.setblocking(flag)                  | 如果 flag 为 False，则将套接字设为非阻塞模式，否则将套接字设为阻塞模式（默认值）。非阻塞模式下，如果调用 recv() 没有发现任何数据，或 send() 调用无法立即发送数据，那么将引起 socket.error 异常。 |
| s.makefile()                         | 创建一个与该套接字相关连的文件                               |



### 服务端

我们使用 socket 模块的 **socket** 函数来创建一个 socket 对象。socket 对象可以通过调用其他函数来设置一个 socket 服务。

现在我们可以通过调用 **bind(hostname, port)** 函数来指定服务的 *port(端口)*。

接着，我们调用 socket 对象的 *accept* 方法。该方法等待客户端的连接，并返回 *connection* 对象，表示已连接到客户端。

写法一：

```
import socket
import time

class Socket:
    def __init__(self, host, port):
        self.host = host
        self.port = port

    def connect_client(self):
        # 给本机服务端建立socket接口，socket.AF_INET指使用IPV4地址，socket.SOCK_STREAM指使用TCP中的socket类型，该协议被用来网络中传输信息
        sock_server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

        sock_server.bind((self.host, self.port))   # 接口绑定ip地址以及端口号

        sock_server.listen()  # 阻塞式监听连接请求，listen还有一个参数，用于限定最大连接数，超过时需要进行排队

        conn, addr = sock_server.accept()  # 接收监听到的连接请求, 同意连接，并且创建一个已经建立连接的socket对象，后面的操作都使用这个对象

        sock_server.close()   # 由于主机的socket只是用来监听客户端连接的，因此此时可以不再监听连接，后面的发送等操作就要使用与服务端连接的socket

        print(f"client socket ip:{addr[0]}, port:{addr[1]}")
        while True:
            recv_data = conn.recv(1024)     # 接收客户端发送的数据，并存储到recv_data中
            if not recv_data:
                break
            print(recv_data)
            conn.sendall(recv_data)   # 将接收到的数据，重新发送给客户端

if __name__ == "__main__":
    host = "127.0.0.1"
    port = 65432
    socket_server = Socket(host, port)
    socket_server.connect_client()
```



写法二：

```
# 导入 socket、sys 模块
import socket
import sys

# 创建 socket 对象
serversocket = socket.socket(
            socket.AF_INET, socket.SOCK_STREAM)

# 获取本地主机名
host = socket.gethostname()

port = 9999

# 绑定端口号
serversocket.bind((host, port))

# 设置最大连接数，超过后排队
serversocket.listen(5)

while True:
    # 建立客户端连接
    clientsocket,addr = serversocket.accept()      

    print("连接地址: %s" % str(addr))
   
    msg='欢迎访问菜鸟教程！'+ "\r\n"
    clientsocket.send(msg.encode('utf-8'))
    clientsocket.close()
```





### 客户端

接下来我们写一个简单的客户端实例连接到以上创建的服务。端口号为 9999。

**socket.connect(hostname, port )** 方法打开一个 TCP 连接到主机为 *hostname* 端口为 *port* 的服务商。连接后我们就可以从服务端获取数据，记住，操作完成后需要关闭连接。

完整代码如下：

```
import socket

data = None
class Client:
    def __init__(self, host, port):
        self.host = host
        self.port = port

    def connect_server(self):
        global data
        socket_client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)  # 创建客户端的socket对象
        socket_client.connect((self.host, self.port))    # 直接使用客户端socket对象连接服务端
        socket_client.sendall(b"hello server, are you ok?")   # 由于这里客户端建立的socket对象并不是需要用于监听，因此我们可以直接使用该socket对象来发送信息给服务端
        data = socket_client.recv(1024)
        print(data)

if __name__ == "__main__":
    host = "127.0.0.1"
    port = 65432
    client = Client(host, port)
    client.connect_server()

```



## Python Internet 模块

以下列出了 Python 网络编程的一些重要模块：

| 协议   | 功能用处                         | 端口号 | Python 模块                |
| :----- | :------------------------------- | :----- | :------------------------- |
| HTTP   | 网页访问                         | 80     | httplib, urllib, xmlrpclib |
| NNTP   | 阅读和张贴新闻文章，俗称为"帖子" | 119    | nntplib                    |
| FTP    | 文件传输                         | 20     | ftplib, urllib             |
| SMTP   | 发送邮件                         | 25     | smtplib                    |
| POP3   | 接收邮件                         | 110    | poplib                     |
| IMAP4  | 获取邮件                         | 143    | imaplib                    |
| Telnet | 命令行                           | 23     | telnetlib                  |
| Gopher | 信息查找                         | 70     | gopherlib, urllib          |

更多内容可以参阅官网的 [Python Socket Library and Modules](https://docs.python.org/3.0/library/socket.html)。



# SMTP发送邮件

SMTP（Simple Mail Transfer Protocol）即简单邮件传输协议,它是一组用于由源地址到目的地址传送邮件的规则，由它来控制信件的中转方式。

python的smtplib提供了一种很方便的途径发送电子邮件。它对smtp协议进行了简单的封装。

Python创建 SMTP 对象语法如下：

```
import smtplib

smtpObj = smtplib.SMTP( [host [, port [, local_hostname]]] )
```

参数说明：

- host: SMTP 服务器主机。 你可以指定主机的ip地址或者域名如:runoob.com，这个是可选参数。
- port: 如果你提供了 host 参数, 你需要指定 SMTP 服务使用的端口号，一般情况下SMTP端口号为25。
- local_hostname: 如果SMTP在你的本机上，你只需要指定服务器地址为 localhost 即可。

Python SMTP对象使用sendmail方法发送邮件，语法如下：

```
SMTP.sendmail(from_addr, to_addrs, msg[, mail_options, rcpt_options]
```

参数说明：

- from_addr: 邮件发送者地址。
- to_addrs: 字符串列表，邮件发送地址。
- msg: 发送消息

这里要注意一下第三个参数，msg是字符串，表示邮件。我们知道邮件一般由标题，发信人，收件人，邮件内容，附件等构成，发送邮件的时候，要注意msg的格式。这个格式就是smtp协议中定义的格式。



### 发送普通邮件

```
import smtplib
from email.mime.text import MIMEText
from email.header import Header

from_email = "2971209213@qq.com"
to_email = "2975602606@qq.com"
pass_word = "ixqywlvcxqwmddci"
smtp_server = "smtp.qq.com"
try:
    msg = MIMEText("""        # 实例化发送邮件的文本对象
    Beware the Ides of March.hello I am best.\n
    You have more important should to do !
    """)
    msg["From"] = Header("M0PVHS <2971209213@qq.com>")   # 按照qq邮箱的协议书写规则必须在文本对象中加上From（发送人）、To（接收人）、Subject （邮件主题）
    msg["To"] = Header("SHADOW <2975602606@qq.com>")
    msg["Subject"] = Header("For your suggest")
    smtp = smtplib.SMTP_SSL(smtp_server)   # 实例化对象并连接QQ邮箱服务端
    smtp.set_debuglevel(1)                 # 打印和服务器的交互信息
    smtp.login(from_email, pass_word)      # ixqywlvcxqwmddci  登录QQ邮箱
    smtp.sendmail(from_email, to_email, msg.as_string())   # 发送邮件
    smtp.quit()

except Exception as e:
    print(e)
```



### 发送内容为html的邮件

发送html内容的邮件与发送普通邮件的方式差不多，不过是需要在MIMEText编辑发送邮件的内容处指明内容的类型

```
import smtplib
from email.mime.text import MIMEText       # #引入mail.mime的MIMEText 类来实现支持HTML格式的邮件（email.mime是smtplib模块邮件内容主体的扩展）
from email.header import Header

class Smtp_sendto_QQmail():
    def __init__(self, from_where, to, subject, content):
        self.from_where = from_where
        self.to = to
        self.subject = subject
        self.content = content
        self.smtp = "smtp.qq.com"
        self.smtp_passwd = "ixqywlvcxqwmddci"
        
    def sent(self):
        # 编辑要发送的信息的内容
        send_content = MIMEText(self.content, 'html', 'utf-8')   # 传入的参数有：邮件正文内容，邮件正文内容的类型，邮件内容的编码方式
        send_content['From'] = Header(f"M0PVHS <{self.from_where}>")
        send_content['To'] = Header(f"shadow <{self.to}>")
        send_content['Subject'] = Header(f"{self.subject}")

        # 发送
        try:
            smtp = smtplib.SMTP(self.smtp)
            smtp.login(self.from_where, self.smtp_passwd)  # 登录QQ邮箱
            smtp.sendmail(self.from_where, self.to, send_content.as_string())
            print(send_content.as_string())
            print("发送成功")
        except Exception as e:
            print("发送失败")
            print(e)
if __name__ == "__main__":
    from_where = "2971209213@qq.com"
    to = "2975602606@qq.com"
    subject = "html content"
    content = """
    <p>这是一个标题</p>\n
    <a href='www.baidu.com'>baidu</a>
    """
    smtp = Smtp_sendto_QQmail(from_where, to, subject, content)
    smtp.sent()

```



### 发送带附件的邮件

其实smtp发送多附件的邮件也是与发送纯文本的邮件思路相同，不过是多加了发送的内容的编辑函数以及内容

Python发送多附件邮件的基本思路，首先就是用MIMEMultipart()方法来表示这个邮件由多个部分组成。然后再通过attach()方法将各部分内容分别加入到MIMEMultipart容器中。MIMEMultipart有attach()方法，而MIMENouMultipart没有，只能被attach。
python中MIME各对象的继承关系如下：
![img](https://img2020.cnblogs.com/blog/1140295/202111/1140295-20211123151246909-2045123800.png)
MIME有很多种类型，如果附件是文本格式，就是MIMEText;如果是图片格式就行MIMEImage；如果是音频格式就用MIMEAudio，如果是其他类型的格式例如pad，word、Excel等类型的，就很难确定用那种MIME了，此时可以使用MIMEApplication（）方法。MIMEApplication默认子类型是application/octet-stream，表明“这是个二进制，不知道文件的下载类型”，客户端收到这个声明后，根据文件后的扩展名进行处理。

实例：

```
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from email.header import Header
import traceback

class Smtp_send_multipart_to_QQmail:
    def __init__(self, from_where, to, subject, content, file=None, file2=None):
        self.from_where = from_where
        self.to = to
        self.subject = subject
        self.passwd = "ixqywlvcxqwmddci"
        self.content = content
        self.file1 = file
        self.file2 = file2
        self.login_path = 'smtp.qq.com'

    # 发送带附件的邮件的思路就是创建一个多模块的容器，然后将要发送的内容全都编辑过后实例化并加入到这个容器中，但是这个容器的from、to、subject等信息同样是必须的
    def send(self):
        message = MIMEMultipart()   # 创建一个邮件的多模块容器
        message['From'] = Header(f"M0PVHS {self.from_where}")
        message['Subject'] = Header(f"{self.subject}")
        if type(self.to) == 'str':
            message['To'] = Header(f"shadow {self.to}")
        # 如果发送邮件的为多个人时，需要将列表中的值以逗号分隔地组合成一条字符串
        elif type(self.to) == type(list()):
            message['To'] = Header(f"shadow {','.join(self.to)}")

            # 编辑邮件的正文内容
        text = MIMEText(self.content)
        message.attach(text)     # 将正文内容添加到多模块容器中

        # 添加附件1
        if self.file1 is not None:
            file_text = MIMEText(open(self.file1, 'rb').read(), 'base64', 'uft8')
            
# file_text["Content-Type"]='application/octet-stream'指明了响应体体中的数据类型
# 这里指示的是其数据类型为二进制流类型
            file_text["Content-Type"] = 'application/octet-stream'

# file_text['Content-Disposition']='attachment; filename="kefmendian.txt"'设置了响应体的头部字段，该字段用于指示客户端如何处理响应体中的数据，
# 这里的attachment表示将响应体中的数据作为附件进行下载
# filename表示下载的附件的名称			
            file_text['Content-Disposition'] = 'attachment; filename="kfcmendian.txt"'
            message.attach(file_text)
# 通过这两个头部字段，服务器可以告诉客户端	如何处理响应体中的数据

        # 添加附件2
        if self.file2 is not None:
            file2_text = MIMEText(open(self.file2, 'rb').read(), 'base64', 'uft8')
            file2_text["Content-Type"] = 'application/octet-stream'

            file2_text['Content-Disposition'] = 'attachment; filename="file2.txt"'
            message.attach(file2_text)


    # 发送邮件
        try:
            smtp = smtplib.SMTP(self.login_path)
            smtp.login(self.from_where, self.passwd)
            smtp.sendmail(self.from_where, self.to, message.as_string())
            print("发送成功")
            smtp.close()
        except Exception as e:
            print("发送失败")
            print(traceback.print_exc())

if __name__ == "__main__":
    from_where = "2971209213@qq.com"
    to = ['2975602606@qq.com', '2971209213@qq.com']
    subject = "multipart file"
    content = '''
    疯狂星期四，是兄弟就来店里砍我，我在附件这些地址中【doge】
    '''
    file = "D:/GZR_practice/txt/深圳的kfc门店信息.txt"
    smtp = Smtp_send_multipart_to_QQmail(from_where, to, subject, content, file)
    smtp.send()
```

**file_text["Content-Type"]='application/octet-stream'**指明了响应体体中的数据类型
这里指示的是其数据类型为二进制流类型

**file_text['Content-Disposition']='attachment; filename="kefmendian.txt"'**设置了响应体的头部字段，该字段用于指示客户端如何处理响应体中的数据，
这里的attachment表示将响应体中的数据作为附件进行下载

filename表示下载的附件的名称

**通过这两个头部字段，服务器可以告诉客户端	如何处理响应体中的数据**



## 给多个邮箱发送邮件

具体在以上的案例

```
 # 如果发送邮件的为多个人时，需要将列表中的值以逗号分隔地组合成一条字符串
        elif type(self.to) == type(list()):
            message['To'] = Header(f"shadow {','.join(self.to)}")

```



#### MIMEMultipart类型

MIME邮件中各种不同类型的内容是分段存储的，各个段的排列方式、位置信息都通过Content-Type域的multipart类型来定义。multipart类型主要有三种子类型：mixed、alternative、related。
（1） MIMEMultipart类型基本格式
● MIMEMultipart（‘mixed’）类型
如果一封邮件中含有附件，那邮件的中必须定义multipart/mixed类型，邮件通过multipart/mixed类型中定义的boundary标识将附件内容同邮件其它内容分成不同的段。基本格式如下：
msg=MIMEMultipart(‘mixed’)

● MIMEMultipart(‘alternative’)类型
MIME邮件可以传送超文本内容，但出于兼容性的考虑，一般在发送超文本格式内容的同时会同时发送一个纯文本内容的副本，如果邮件中同时存在纯文本和超文本内容，则邮件需要在Content-Type域中定义multipart/alternative类型，邮件通过其boundary中的分段标识将纯文本、超文本和邮件的其它内容分成不同的段。基本格式如下：
msg=MIMEMultipart(‘alternative’)

● MIMEMultipart(‘related’)类型
MIME邮件中除了可以携带各种附件外，还可以将其它内容以内嵌资源的方式存储在邮件中。比如我们在发送html格式的邮件内容时，可能使用图像作为 html的背景，html文本会被存储在alternative段中，而作为背景的图像则会存储在multipart/related类型定义的段中。基本格式如下：
msg=MIMEMultipart(‘related’)



# 多线程

线程是cpu处理器任务调度和执行的基本单位，线程之间的内存是共享的

一个进程是由多个或一个线程组成的，而进程的内存都是独立的

线程可以分为:

- **内核线程：**由操作系统内核创建和撤销。
- **用户线程：**不需要内核支持而在用户程序中实现的线程。



Python中使用线程有两种方式：函数或者用类来包装线程对象。

函数式：调用 _thread 模块中的start_new_thread()函数来产生新线程。语法如下:

```
_thread.start_new_thread ( function, args[, kwargs] )
```

参数说明:

- function - 线程函数。
- args - 传递给线程函数的参数,他必须是个tuple类型。
- kwargs - 可选参数。

示例：

```
import threading
import time
import traceback
import _thread

def print_something(threading_id, delay):
    count = 0
    while count < 5:
        time.sleep(delay)
        print(f"using threading is {threading_id}, current_time is {time.ctime(time.time())}")
        count += 1
try:
    _thread.start_new_thread(print_something, ('Thread-1', 2))
    _thread.start_new_thread(print_something, ('Thread-2', 5))
    # thread1 = threading.Thread(target=print_something, args=('Thread-1', 2))
    # thread2 = threading.Thread(target=print_something, args=('Thread-2', 5))
    # thread1.start()
    # thread2.start()
    # thread1.join()
    # thread2.join()
except Exception as e:
    print("线程启动失败，", e)

while 1:       # 由于程序并不会等待_thread模块创建的进程执行完毕才结束，因此如果不使用while 1来让程序一直执行，就会没有任何结果
    pass
    
>>>
using threading is Thread-1, current_time is Sun Oct 15 16:01:20 2023
using threading is Thread-1, current_time is Sun Oct 15 16:01:22 2023
using threading is Thread-2, current_time is Sun Oct 15 16:01:23 2023
using threading is Thread-1, current_time is Sun Oct 15 16:01:24 2023
using threading is Thread-1, current_time is Sun Oct 15 16:01:26 2023
using threading is Thread-2, current_time is Sun Oct 15 16:01:28 2023
using threading is Thread-1, current_time is Sun Oct 15 16:01:28 2023
using threading is Thread-2, current_time is Sun Oct 15 16:01:33 2023
using threading is Thread-2, current_time is Sun Oct 15 16:01:38 2023
using threading is Thread-2, current_time is Sun Oct 15 16:01:43 2023
```



## 线程模块

Python3 通过两个标准库 _thread 和 threading 提供对线程的支持。

_thread 提供了低级别的、原始的线程以及一个简单的锁，它相比于 threading 模块的功能还是比较有限的。

threading 模块除了包含 _thread 模块中的所有方法外，还提供的其他方法：

- threading.currentThread(): 返回当前的线程变量。
- threading.enumerate(): 返回一个包含正在运行的线程的list。正在运行指线程启动后、结束前，不包括启动前和终止后的线程。
- threading.activeCount(): 返回正在运行的线程数量，与len(threading.enumerate())有相同的结果。

除了使用方法外，线程模块同样提供了Thread类来处理线程，Thread类提供了以下方法:

- **run():** 用以表示线程活动的方法。

- start():

    启动线程活动。

    

- **join([time]):** 等待至线程中止。这阻塞调用线程直至线程的join() 方法被调用中止-正常退出或者抛出未处理的异常-或者是可选的超时发生。

- **isAlive():** 返回线程是否活动的。

- **getName():** 返回线程名。

- **setName():** 设置线程名。

### 使用threading模块创建线程

我们可以通过直接从 threading.Thread 继承创建一个新的子类，并实例化后调用 start() 方法启动新线程，即它调用了线程的 run() 方法：

```
import threading
import time
class myThread(threading.Thread):
    def __init__(self, threadID, delay):
        super().__init__()   # 显式地调用父类地构造函数
        self.threadID = threadID
        self.delay = delay

    def run(self):    # 重写threading.Thread这个父类的run方法， 当使用start函数执行线程的时候就会调用该方法
        count = 0
        while count < 5:
            time.sleep(self.delay)
            print(f"{self.threadID}, {time.ctime(time.time())}")  # time.time返回当前的时间戳，time.ctime将当前的时间戳转换为可读的形式
            count += 1

if __name__ == "__main__":
    mythread = myThread("Thread-1", 2)   # 实例化线程类，当实例化该类的时候，就相当于实例化了一个线程类，但这个线程类并不会立刻执行
    mythread2 = myThread("Thread-2", 5)
    mythread.start()
    mythread2.start()
    mythread.join()
    mythread2.join()
```





## 线程同步

如果多个线程共同对某个数据修改，则可能出现不可预料的结果，为了保证数据的正确性，需要对多个线程进行同步。

使用 Thread 对象的 Lock 和 Rlock 可以实现简单的线程同步，这两个对象都有 acquire 方法和 release 方法，对于那些需要每次只允许一个线程操作的数据，可以将其操作放到 acquire 和 release 方法之间。如下：

多线程的优势在于可以同时运行多个任务（至少感觉起来是这样）。但是当线程需要共享数据时，可能存在数据不同步的问题。

考虑这样一种情况：一个列表里所有元素都是0，线程"set"从后向前把所有元素改成1，而线程"print"负责从前往后读取列表并打印。

那么，可能线程"set"开始改的时候，线程"print"便来打印列表了，输出就成了一半0一半1，这就是数据的不同步。为了避免这种情况，引入了锁的概念。

锁有两种状态——锁定和未锁定。每当一个线程比如"set"要访问共享数据时，必须先获得锁定；如果已经有别的线程比如"print"获得锁定了，那么就让线程"set"暂停，也就是同步阻塞；等到线程"print"访问完毕，释放锁以后，再让线程"set"继续。

经过这样的处理，打印列表时要么全部输出0，要么全部输出1，不会再出现一半0一半1的尴尬场面。



示例：

```
import threading
import time
num = 100
lock = threading.Lock()
def print_thing(sub_num, delay, count):
    global num, lock
    with lock:             # 线程开始时，由于有锁的存在，则num的值将锁定为100，然后开始循环执行自减操作，此时另一个线程无法更改num的值
        while count:
            time.sleep(delay)
            num -= sub_num
            print(f"{num}, {time.ctime(time.time())}")
            count -= 1
    print(f"结束")
if __name__ == "__main__":
    try:
        print(num)
        lock = threading.Lock()
        thread1 = threading.Thread(target=print_thing, args=(1, 2, 5))
        thread2 = threading.Thread(target=print_thing, args=(2, 4, 5))
        thread1.start()
        thread2.start()
        # thread1.join()
        # thread2.join()
    except Exception as e:
        print(e)
        
>>>
100
99, Sun Oct 15 17:37:41 2023
98, Sun Oct 15 17:37:43 2023
97, Sun Oct 15 17:37:45 2023
96, Sun Oct 15 17:37:47 2023
95, Sun Oct 15 17:37:49 2023
结束
93, Sun Oct 15 17:37:53 2023
91, Sun Oct 15 17:37:57 2023
89, Sun Oct 15 17:38:01 2023
87, Sun Oct 15 17:38:05 2023
85, Sun Oct 15 17:38:09 2023
结束
```







## 线程优先级队列（ Queue）

Python 的 Queue 模块中提供了同步的、线程安全的队列类，包括FIFO（先入先出)队列Queue，LIFO（后入先出）队列LifoQueue，和优先级队列 PriorityQueue。

这些队列都实现了锁原语，能够在多线程中直接使用，可以使用队列来实现线程间的同步。

Queue 模块中的常用方法:



- Queue.qsize() 返回队列的大小
- Queue.empty() 如果队列为空，返回True,反之False
- Queue.full() 如果队列满了，返回True,反之False
- Queue.full 与 maxsize 大小对应
- Queue.get([block[, timeout]])获取队列，timeout等待时间
- Queue.get_nowait() 相当Queue.get(False)
- Queue.put(item) 写入队列，timeout等待时间
- Queue.put_nowait(item) 相当Queue.put(item, False)
- Queue.task_done() 在完成一项工作之后，Queue.task_done()函数向任务已经完成的队列发送一个信号
- Queue.join() 实际上意味着等到队列为空，再执行别的操作



 Queue作用：主要就是为多线程生产值、消费者之间线程通信提供服务，具有先进先出的数据结构。
1、首先我们组要明白为什么要使用队列，队列的性质，
  多线程并发编程的重点，是线程之间共享数据的访问问题和线程之间的通信问题，为了解决线程之间数据共享问题,
  PYTHON 提供了一个数据类型【队列】可以用于在多线程并发模式下，安全的访问数据而不会造成数据共享冲突。
  正常请求的多线程，如果是消费之和生产者，通过列表实现，多线程会对列表中的数据取值，会出现同时访问列表数据
  的情况，这时候就需要对线程进行加锁或者是线程等待，手动进行解决，过于麻烦，但是队列会通过先进先出或者先进
  后出的模式，保证了单个数据不会进行同时被多个线程进行访问。


#### 1.1 FIFO

```
 Queue.Queue(maxsize=0)
```

 FIFO即First in First Out,先进先出。Queue提供了一个基本的FIFO容器，使用方法很简单,maxsize是个整数，指明了队     
 列中能存放的数据个数的上限。一旦达到上限，插入会导致阻塞，直到队列中的数据被消费掉。如果maxsize小于或者  
 等于0，队列大小没有限制。	

#### 1.2 LIFO

```
 Queue.LifoQueue(maxsize=0)
```


 LIFO即Last in First Out,后进先出。与栈的类似，使用也很简单,maxsize用法同上

 

```
priority
 class Queue.PriorityQueue(maxsize=0)
```

 构造一个优先队列。maxsize用法同上。



示例：

#### 多线程：

```
import threading
import time
import queue

def show_value(name, num_list):
    while not glo_num:
        lock.acquire()   # 锁定
        if not num_list.empty():
            print(f"{name}, {num_list.get()}, {time.ctime()}")
            lock.release()
        else:
            lock.release()
            pass
        time.sleep(1)       # 每个进程在获得锁的时候，执行都会非常的快，为了防止因为某一个线程执行得太快而全执行，我们让线程慢一点
glo_num = 0
counts = 1
name_list = ["Thread-1", "Thread-2", "Thread-3"]
num_list = ["one", "two", "three", "four", "five", "six", "seven", "eight"]
lock = threading.Lock()
que = queue.Queue(10)   # 创建容量为10的队列
threads_list = list()

# 将所有线程启动
for i in name_list:
    threads = threading.Thread(target=show_value, args=(i, que))
    threads_list.append(threads)
    threads.start()
    print(f"{i} is start")

# 锁定，将所有数据写入队列中
with lock:
    for i in num_list:
        que.put(i)

# 为了防止程序执行过快而导致线程还未执行完毕就已经结束了，我们需要等待队列被消化完才结束
while not que.empty():
    pass

glo_num = 1

# 等待线程完成，防止线程未执行完毕就已经停止程序
for i in threads_list:
    i.join()

print("over")

>>>
Thread-1 is start
Thread-2 is start
Thread-3 is start
Thread-1, one, Sun Oct 15 20:42:07 2023
Thread-2, two, Sun Oct 15 20:42:07 2023
Thread-3, three, Sun Oct 15 20:42:07 2023
Thread-3, four, Sun Oct 15 20:42:08 2023
Thread-1, five, Sun Oct 15 20:42:08 2023
Thread-2, six, Sun Oct 15 20:42:08 2023
Thread-2, seven, Sun Oct 15 20:42:09 2023
Thread-3, eight, Sun Oct 15 20:42:10 2023
over

注意：具体线程得执行情况是不清楚的，因为每个线程的状态都不一样，获取锁的顺序也不一样
```





#### 生产者/消费者

生产者与消费者也是使用了队列的概念，将队列想象成一个仓库，生产者负责往队列里面塞数据，消费者负责消费掉队列中的数据

```
import threading
import time
from queue import Queue
import random
from threading import Lock

run_state = 1
def producer(q):
    while count!=0:
        print(count)
        # print("run_state:" + str(run_state))
        lock.acquire()
        if q.empty():
            random_value = random.randint(1, 100)
            q.put(random_value)
            print(f"生产者生产一个数据：{random_value}")
            # print(count)
            lock.release()
        else:
            time.sleep(1)
            lock.release()
            pass

def consumer(name, q):
    global count
    while count!=0 :
        lock.acquire()
        if not q.empty():
            random_value = q.get()
            print(f"消费者{name}消费一个数据：{random_value}")
            count -= 1
            print("count:" + str(count))
            lock.release()
        else:
            lock.release()
            pass
        time.sleep(1)  # 让消费者不要消费这么快，模拟显示情况

que = Queue(1)
lock = Lock()
count = 10
thread_list = list()
thread1 = threading.Thread(target=producer, args=(que,))
thread2 = threading.Thread(target=consumer, args=("consumer1", que))
thread3 = threading.Thread(target=consumer, args=("consumer2", que))
thread_list.append(thread1)
thread_list.append(thread2)
thread_list.append(thread3)
thread1.start()
thread2.start()
thread3.start()

while count > 0:
    pass
else:
    run_state = 0

for i in thread_list:
    i.join()
print("over")

```



# json

## JSON 语法规则

JSON 语法是 JavaScript 对象表示语法的子集。

- 数据在**名称/值**对中
- 数据由逗号 **,** 分隔
- 使用斜杆 **\** 来转义字符
- 大括号 **{}** 保存对象
- 中括号 **[]** 保存数组，数组可以包含多个对象

**JSON 的两种结构：**

**1、对象：**大括号 **{}** 保存的对象是一个无序的**名称/值**对集合。一个对象以左括号 **{** 开始， 右括号 **}** 结束。每个"键"后跟一个冒号 **:**，**名称/值**对使用逗号 **,** 分隔。

![img](E:\Markdown\markdown\assets\object.png)

**2、数组：**中括号 **[]** 保存的数组是值（value）的有序集合。一个数组以左中括号 **[** 开始， 右中括号 **]** 结束，值之间使用逗号 **,** 分隔。

![img](https://www.runoob.com/wp-content/uploads/2013/09/array.png)

值（value）可以是双引号括起来的字符串（string）、数值(number)、true、false、 null、对象（object）或者数组（array），它们是可以嵌套。

![img](E:\Markdown\markdown\assets\value.png)

------

## JSON 名称/值对

JSON 数据的书写格式是：

```
key : value
```

名称/值对包括字段名称（在双引号中），后面写一个冒号，然后是值：

"name" : "菜鸟教程"

这很容易理解，等价于这条 JavaScript 语句：

name = "菜鸟教程"

------

## JSON 值

JSON 值可以是：

- 数字（整数或浮点数）
- 字符串（在双引号中）
- 逻辑值（true 或 false）
- 数组（在中括号中）
- 对象（在大括号中）
- null

------

## JSON 数字

JSON 数字可以是整型或者浮点型：

{ "age":30 }

------

## JSON 对象

JSON 对象在大括号 **{}** 中书写：

```
{key1 : value1, key2 : value2, ... keyN : valueN }
```

对象可以包含多个名称/值对：

{ "name":"菜鸟教程" , "url":"www.runoob.com" }

这一点也容易理解，与这条 JavaScript 语句等价：

> name = "菜鸟教程" url = "www.runoob.com"

------

## JSON 数组

JSON 数组在中括号 **[]** 中书写：

数组可包含多个对象：

```
[
    { key1 : value1-1 , key2:value1-2 }, 
    { key1 : value2-1 , key2:value2-2 }, 
    { key1 : value3-1 , key2:value3-2 }, 
    ...
    { key1 : valueN-1 , key2:valueN-2 }, 
]
```

```
{     "sites": [         { "name":"菜鸟教程" , "url":"www.runoob.com" },          { "name":"google" , "url":"www.google.com" },          { "name":"微博" , "url":"www.weibo.com" }     ] }
```

在上面的例子中，对象 **sites** 是包含三个对象的数组。每个对象代表一条关于某个网站（name、url）的记录。

------

## JSON 布尔值

JSON 布尔值可以是 true 或者 false：

```
{ "flag":true }
```



------

## JSON null

JSON 可以设置 null 值：

```
{ "runoob":null }
```



------

## JSON 使用 JavaScript 语法

因为 JSON 使用 JavaScript 语法，所以无需额外的软件就能处理 JavaScript 中的 JSON。

通过 JavaScript，您可以创建一个对象数组，并像这样进行赋值：

#### 实例

```
var sites = [     { "name":"runoob" , "url":"www.runoob.com" },      { "name":"google" , "url":"www.google.com" },      { "name":"微博" , "url":"www.weibo.com" } ];
```

可以像这样访问 JavaScript 对象数组中的第一项（索引从 0 开始）：

```
sites[0].name;
```

返回的内容是：

```
runoob
```





## 对象语法

#### 实例

{ "name":"runoob", "alexa":10000, "site":null }

JSON 对象使用在大括号 **{...}** 中书写。

对象可以包含多个 **key/value（键/值）**对。

key 必须是字符串，value 可以是合法的 JSON 数据类型（字符串, 数字, 对象, 数组, 布尔值或 null）。

key 和 value 中使用冒号 **:** 分割。

每个 key/value 对使用逗号 **,** 分割。

![img](https://www.runoob.com/wp-content/uploads/2013/09/object.png)

------

## 访问对象值

你可以使用点号 **.** 来访问对象的值：

#### 实例

var myObj, x; myObj = { "name":"runoob", "alexa":10000, "site":null }; x = myObj.name;







# python	日期与时间

[Python3 日期和时间 | 菜鸟教程 (runoob.com)](https://www.runoob.com/python3/python3-date-time.html)





# python  request

[Python requests 模块 | 菜鸟教程 (runoob.com)](https://www.runoob.com/python3/python-requests.html)









# python装饰器

[python装饰器详细](https://blog.csdn.net/S_o_l_o_n/article/details/100025608)



装饰器，装饰器常用的功能就是给原有的函数添加功能，从而让定义函数的时候不需要进行多次的重写某一些代码，而使用装饰器则可以直接轻易的解决这些问题，同时装饰器其实也是一个函数，这个函数也可以传入参数，这些参数不仅可以在装饰器函数中使用，还能在被装饰的函数中使用



## 闭包

闭包是装饰器的一个重要的概念，可以说闭包其实就相当于python装饰器

装饰器的一般格式为：

```python
def func1(x):
	def func2(y):
		# func2的内容
	return func2
```

```python
def outer(x):
	def inner(y):
		return x+y
	return inner

outer(5)(6)

>>>
11
```

从上面的代码中我们其实可以知道，闭包就是在一个函数中再嵌套一个函数，并被嵌套的函数引用了外部函数的变量，并记录到“单元格”中，这样引用的变量的声生命周期就不会随外部函数的生命周期而被销毁，也就是说装饰器定义的函数我们也可以看成上面的这种形式

例如：

```python
# 装饰器
def logging(func):
    def wrapper(*arg, **kwargs):
        print(f"be use func name is: {func.__name__}\n")
        func(*arg, **kwargs)
    return wrapper

@logging            # 这里的装饰器相当于func = logging(func), 将func函数作为参数传递给logging函数，并执行logging函数中的定义
def func(a, b):
    print(f"the result is: {a+b}\n")

if __name__ == "__main__":
    func(5, 6) 
    
>>>
11
```

通过上面的装饰器实例，我们可以看出，装饰器的基本用法: 就是将装饰的函数运行在装饰器函数中，整体的装饰器结果将会为*func函数=logging(func)*，因此在执行func函数的时候实际上我们运行的是装饰器函数，这实现了无需添加多次重复的代码就可以添加其他附加的功能。





## 带参数的装饰器

上面的例子中我们说过装饰器其实就是一个函数，这个函数中包含另一个函数，但是是函数就可以传入参数，因此装饰器也可以传入参数

```python
def logging(INFO):
	def outwrapper(func):
		def wrapper(*arg, **kwargs):
			print(f"the func logging's config is: {INFO}, \nand use funcname is {func.__name__}\n")
			func(*arg, **kwargs)
		return wrapper
	return outwrapper

@logging(INFO="hello Decorator !")
def func(a, b):
    print(f"func's result is : {a * b}")
    
if __name__ == "__main__":
    func(5, 6)
    
>>>
the func logging's config is: 'hello Decorator !', 
and use funcname is 'func'

func's result is : '30'
```



## 类装饰器

装饰器不一定要使用函数来写，使用类来写也是一样的，只不过是将装饰函数换成了装饰类，并且具体在类似于装饰函数返回被装饰函数时需要使用到call魔法方法

```python
class logging(object):					# 继承基类
    def __init__(self, func1):			# 由于装饰器是直接执行装饰类以及函数的，因此需要使用构造函数直接将被装饰的函数作为参数传入到类成员变量中
        self.func = func1

    def __call__(self, *arg, **kwargs):	 # 这个函数是将类的实例化对象变成一个可以调用的对象，即将类作为函数一样去使用
        print(f"[Decorator]: enter funcname is : {self.func.__name__}")
        return self.func(*arg, **kwargs)  # 像上面的装饰函数一样，将被装饰的函数返回回去
    
@logging
def func(a, b):
    print(f"the func result is : {a * b}")
    
if __name__ == "__main__":
    func(5, 6)
    
>>>
[Decorator]: enter funcname is : func
the func result is : 30
```







## 类装饰器（传入参数）

当然既然可以将类看作一个可调用的对象，那么我们也可以为其传入参数

```python
# 装饰类传入参数
class logging(object):					# 继承基类
    def __init__(self, level):			# 由于装饰器是直接执行装饰类以及函数的，因此需要使用构造函数直接将被装饰的函数作为参数传入到类成员变量中
        self.level = level

    def __call__(self, func):
        def wrapper(*arg, **kwargs):
            print(f"[Decorator]: enter funcname is : {func.__name__}, \n and the enter args is: {self.level}")
            return func(*arg, **kwargs)  # 像上面的装饰函数一样，将被装饰的函数返回回去
        return wrapper

    
@logging(level="hello Decorator")
def func(a, b):							# 这里装饰过后的将会变成func = logging(func)
    print(f"the func result is : {a * b}")
    
if __name__ == "__main__":
    func(5, 6)
    
>>>
[Decorator]: enter funcname is : func, 
 and the enter args is: hello Decorator
the func result is : 30
```

关于为什么我们要在类中定义\_\_call\_\_函请看下一小节



## 类装饰器中的\_\_call\_\_函数

[类中的\_\_call\_\_函数](https://developer.aliyun.com/article/1166530)

其实类中并没有\_\_call\_\_函数，\_\_call\_\_函数是在函数中实现的，而我们在类中定义\_\_call\_\_函数就是为了将类作为一个可以调用的对象才使用的，这是因为上面的装饰函数即：

```python
@logging(level="hello Decorator")
def func()
```

最后变成的格式将会变成与上面装饰函数的形式一样，即

```python
func = logging(func)
```

可以看到我们将类像是函数一样调用，因此我们就需要定义\_\_call\_\_函数，从而实现了类似与装饰函数一样的效果



## 嵌套装饰器

```python
#第十一步：多层装饰器的嵌套
#装饰器1
def kuozhan1(func):
    #定义装饰之后的函数
    def neweat1():
        # 扩展功能1
        print('1-----饭前洗手')
        # 调用基本函数
        func()
        # 扩展功能2
        print('1-----饭后散步')
    return neweat1
#装饰器2
def kuozhan2(func):
    #定义装饰之后的函数
    def neweat2():
        # 扩展功能1
        print('2-----饭前洗手')
        # 调用基本函数
        func()
        # 扩展功能2
        print('2-----饭后散步')
    return neweat2
#基本函数, 
# 这里的装饰器嵌套的具体步骤应该是，先运行kuozhan2函数，然后运行到func过后调用下面被装饰的函数，
# 而被装饰的函数又被kuozhan1装饰，因此函数在被kuozhan1装饰过后才传给函数kuozhan2
@kuozhan2   # 第二步：eat = kuozhan2(eat) = neweat2
@kuozhan1   # 第一步：eat = kuozhan1(eat)  = neweat1
def eat():
    print('吃饭')
#调用函数
eat()

>>>>
2-----饭前洗手
1-----饭前洗手
吃饭
1-----饭后散步
2-----饭后散步
```

这里我们可以知道，<u>装饰器函数会首先被运行，然后才会将被装饰的函数当作参数传入到装饰器函数中继续运行</u>，这就是多层嵌套装饰器函数



## 特殊的装饰器

### @staticmethod

这个装饰器用于定义类的静态方法，静态方法是一个仅仅提供功能函数，而不涉及任何实例或者类的状态，例如：

```Python
class MathUtils:
	@staticmethod
	def add(a, b):
		return a + b
print(MathUtils.add(5, 3))
```

在这里我们制作这个类仅仅是为了将数学工具函数汇总到一个类中，方便管理，并且add函数并不使用这个MathUtils类中的任何状态以及实例，因此这里我们可以使用@staticmethod来将他独立出来



### @classmethod

classmethod（类方法），这种方法是特殊的方法，它可以在不创建类实例的情况下调用类中定义的方法

这种方法与静态方法类似，但有所不同，类方法装饰的函数第一个参数是类本身，我们用cls来做占位符，类方法可以通过cls（类名）参数访问类的属性（类属性：即仅仅属于类，而不是类的实例，所有的实例都共享一个类属性）与方法，也可以通过cls（类名）来调用其他的类方法

其具体的作用有：

要定义类方法，需要使用`@classmethod`装饰器。这样的方法可以在不创建类的实例的情况下直接调用。

```python
class MyClass:
    @classmethod
    def my_class_method(cls, arg1, arg2):
        # 类方法的实现
        pass
```

在上面的示例中，`my_class_method`就是一个类方法，可以通过`MyClass.my_class_method()`直接调用。



#### 1.代替构造函数

类方法常常被用作替代构造函数，可以用来创建类的实例。（这样我们就可以在创建类之前做更多的前处理）

```python
class Person:
	def __init__(self, name, age):
        self.name = name
        self.age = age
    @classmethod
    def from_birth_year(cls, name, birth_year):
        age = 2024 - birth_year
        return cls(name, age)

person = Person.from_birth_year("jack", 1997) # 通过这个类方法，让用户输入自己的出生年，就能自动计算他到底到现在为止多少岁了，并创建类实例
print(person.age)
```

#### 2.工厂模式

类方法还常用于实现工厂模式，根据参数的不同进而返回不同的类实例

```python
class Shape:
	@classmethod
	def create_shape(cls, shape_type):
		if shape_type == "circle":
			return Circle()
		elif shape_type == "rectangle":
			return Rectangle()
class Circle:
	pass

class Rectangle:
	pass
circle = Shape.create_shape("circle")
rectangle = Shape.create_shape("rectangle")
```



#### 3. 单例模式

类方法还可以用于实现单例模式，确保类只有一个实例。

```python
class Singleton:
    _instance = None
    
    @classmethod
    def get_instance(cls):
        if cls._instance is None:
            cls._instance = cls()
        return cls._instance

singleton1 = Singleton.get_instance()
singleton2 = Singleton.get_instance()

print(singleton1 is singleton2)  # 输出：True

```



### @property

@property装饰器用于将可执行的方法转为一个只读的变量，通过通过这个变量我们能获取类中的隐私变量，保护了内部变量，同时能在返回的时候进行其他操作

**但是property装饰器不能用在普通的函数中，那样的函数只会被转换为property对象，而不是一个只读的变量**

```python
# @property
# def func():
#     return 11

# if __name__ == "__main__":
#     print(func)               >>> <property object at 0x0000021FE51C4D60>

class Func:
    name = "Tom"                    # 在__init__构造函数中定义的变量是类变量，这个类变量是整个类都拥有的变量，并不是某个实例的变量
    def __init__(self, val):
        self._val = val
    
    @staticmethod
    def create_func1(val):
        return Func(val)

 
    @classmethod
    def create_func(cls, val):
        print(cls.name)             # classmethod装饰的类方法能够通过cls.类变量的方法来访问类变量，这样能够实现动态绑定，让不同的类变量绑定不同的类对象
        return cls(val)
    
    @property
    def func_val(self):
        return self._val * 2
    
if __name__ == "__main__":
    func = Func.create_func(44)
    func1 = Func.create_func1(16)
    print(func is func1)
    print(func)
    print(func1)
    print("My new instance val is : {}".format(func.func_val))

>>>
Tom
False
<__main__.Func object at 0x0000019C93337A30>
<__main__.Func object at 0x0000019C93337A90>
My new instance val is : 88
```

最后注意：

注：*类方法*的意义在于，其能够**封装**实例化前的操作，并确保所有相似的类对象的实例化的一致性，同时能够将类变量进行动态绑定，当子类同样**继承**类变量并将类变量复写的时候，直接使用cls.类变量名进行访问类变量的时候能够自动访问到子类的类变量而不是父类的

而property装饰的方法，优势则是通过直接访问属性的方式进行访问、修改实例属性，同时能够优雅地加上各种预操作，而不需要显式地去调用setter与getter方法

由下面的例子可以看出这个优势：

```python
class Circle:
	def __init__(self, radius):
		self._radius = radius
	
	def get_radius(self):
		return self._radius
	
	def set_radius(self, val):
		self._radius = val
	
	@property
	def radius(self):
		return self._radius
	
	@radius.setter  # 这里的装饰就是将"radius=" = radius.setter(val)，即将这个属性幅值的操作转换为这个被转化为属性的方法的设置器，当对这个被转换为属性的方法进行属性赋值形式的操作，则会自动调用这个被装饰的方法，这样我们就能够在赋值的时候做一些预操作
	def radius(self, val):
		if value > 0:
			self._radius = val
		else:
			raise ValueError("Radius must be positive")

# 两种访问实例属性的方法对比
# 1. 显式访问
c = Circle(1)
print(c.get_radius())
c.set_radius(16)
print(c.get_radius())

# 2. 属性式访问
c = Circle(5)
print(c.radius)
c.radius = 44
print(c.radius)
```



# 嘎嘎嘎









---

###### 递归

函数递归调用是一种特殊的函数调用形式，整体来说就是定义完一个函数过后，通过编写程序让函数自己调用自己

*例子*

```python
x = input("请输入一个值：")
y = input("请输入一个值：")
def sum1(x,y):
    if x == 1 and y == 1:
            return 1
    while int(y) >= int(x):
       return int(y) + sum1(int(x),int(y)-1)
print(sum1(x,y))

#也可以这么用：

x = input('请输入一个值：')
def sum_num(x):
    if x == 1:
        return 1
    return int(x) + sum_num(int(x)-1)
print(sum_num(x))
```



***



###### *函数之间的相互调用*

```python
def say_hello():                      #定义一个函数用于print一句话
    print("Hello Yootk Hello jack")
def get_info():                       #定义一个方法用于获取say_hello（）的内容
    say_hello()
    return "goodbye, see you again"
return_data = get_info()              #将get_info()方法的返回值赋给return_data，由于在赋值的时候需要调用get_info（）方法所以需要执行get_info（）方法，所以会先执行say_hello（）方法中的打印
print(return_data)                    #将return_data的值打印出来，，，，因为如果单独打印say_hello函数的值就会有None但是get_info方法还返回了了一句话所以不会出现None
```

在python中如果函数中没有return值，那么函数将会自动返回一个return 0 的值即None

**注**：在函数调用中一个函数被另一个函数调用用的话，就一定会在return之前将函数中要执行的函数先执行，然后再返回值。

* 比如上面的代码，get_info（）函数在赋给变量return_data的时候将会执行这个get_info函数并且在执行的时候先将say_hello（）方法的打印先执行，然后再返回一个值给变量return_data，最后再用print（）函数将变量return_data的值给打印出来。

  

  ***round()是python自带的一个函数，用于数字的四舍五入。***
  round(number,digits)
  参数：

digits>0，四舍五入到指定的小数位
digits=0, 四舍五入到最接近的整数
digits<0 ，在小数点左侧进行四舍五入
如果round()函数只有number这个参数，等同于digits=0
四舍五入规则：

要求保留位数的后一位<=4，则进位，如round(5.214,2)保留小数点后两位，结果是 5.21
要求保留位数的后一位“=5”，且该位数后面没有数字，则不进位，如round(5.215,2)，结果为5.21
要求保留位数的后一位“=5”，且该位数后面有数字，则进位，如round(5.2151,2)，结果为5.22
要求保留位数的后一位“>=6”，则进位。如round(5.216,2)，结果为5.22







——————————————————————————————————————————









































# 并发编程

**用法**：`计算居多的使用进程，i/o数据交换居多的使用线程`

在操作系统每次运行一个的时候，系统都会分配一个进程，进程是指具有独立功能的，关于某个数据集合的一次活动

操作系统中的每一个进程都是独立的

一个进程包含三个组成部分：程序、数据、进程控制块（PCB）

***PCB：***

每当启动一个进程时，操作系统都会自动为其开辟一个**<u>专用的存储区</u>**，用以记录它在系统中的动态特性

PCB一般包含：

》标识信息：进程名

》说明信息：进程状态、进程存放位置

》现场信息：通用寄存器内存、控制寄存器内存、断点地址

》管理信息：进程优先级、队列指针



——————————————————————————————————



python中的多进程编程可以使用**multiprocessing模块**实现，该模块中提供有专门的进程处理类**Process**

#### Process类-



process类常用方法及属性：

![1677503269346](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1677503269346.png)

| def \__init__([group[,target[,name[,args[,kwargs[,daemon]]]]]]) |
| ------------------------------------------------------------ |
| 创建一个执行进程，参数作用如下：                             |
| group：分组定义                                              |
| target：进程处理对象（代替run（）函数）                      |
| name：进程名称，若不设置，则自动分配一个名称                 |
| args：进程处理对象所需要的执行参数                           |
| kwargs：调用对象字典                                         |
| daemon：是否设置为后台进程                                   |



```python
import multiprocessing, time
def worker(deply,count):
    for num in range(count):
        print("【%s】进程id：%s  进程名称：%s" %(num,multiprocessing.current_process().pid,multiprocessing.current_process().name))
        time.sleep(deply)

def main():
    for item in range(3):
        process = multiprocessing.Process(target = worker,args = (1,10),name = "R进程-%s"%item)
        process.start()

if __name__ == "__main__":
    main()
```



​	**当将属性daemon设置为True时，创建的进程将会在后台运行**

```python
'''守护进程'''
import multiprocessing, time
def status():
    item = 1
    while True:
        print("【守护进程id：%s、守护进程名：%s】item = %s"%(multiprocessing.current_process().pid,multiprocessing.current_process().name,item))
        item += 1
        time.sleep(1)

def worker():
    demon_process = multiprocessing.Process(target = status, name = "守护进程", daemon = True)  #为工作进程创建一个守护进程，并且将守护进程设置为后台运行
    demon_process.start()
    for i in range(10):
        print("【工作进程id：%s、工作进程名：%s】item = %s"%(multiprocessing.current_process().pid,multiprocessing.current_process().name,i))
        time.sleep(1)
def main():
    work_process = multiprocessing.Process(target = worker,name = "工作进程")
    work_process.start()

if __name__ == "__main__":
    main()
```



————————————————————————————————————



##### 进程池

进程池的主要设计思想是将系统可用的进程对象放到一个对象池中进行管理

这么做可以便于系统进程的管理，开发中可以利用进程池以提高进程对象的可复用性

| 方法                                       | 描述                                                 |
| ------------------------------------------ | ---------------------------------------------------- |
| apply(self.func,args=(),kwds={})           | 采用阻塞模式创建进程并接受返回对象                   |
| apply_async(func[,args[,kwds[,callback]]]) | 采用非阻塞模式创建进程，并且可以接受工作函数返回结果 |
| apply_async(self,func,args=(),kwds={})     | 采用非阻塞模式进行数据处理                           |
| map_async(self,func,iterable)              | 采用非阻塞模式进行数据处理                           |
| close(self)                                | 关闭进程池，不再接受新的进程                         |
| terminate(self)                            | 中断进程                                             |
| join(self)                                 | 进程强制执行                                         |



##### 进程通信

管道（pipe）是系统进程通信的一种技术手段，开发者可以利用管道创建两个通信连接对象，这两个连接对象可以实现单端通信，也可以实现双端通信

```python
'''Pipe进程通信管道'''
import multiprocessing, time
def send(conn,data):
    conn.send(["百度","下一度百",data])

def receive(conn):
    print("【数据接收】：%s"%conn.recv())

def main():
    conn_send,conn_recv, = multiprocessing.Pipe()   #创建两个进程通信管道，并设置好进程的处理函数与连接对象
    process_send = multiprocessing.Process(target = send, args = (conn_send,"R"))
    process_recv = multiprocessing.Process(target = receive, args = (conn_recv,))
    process_recv.start()
    process_send.start()
if __name__ == "__main__":
    main()
```

进程通信管道的实现可以通过multiprocessing.Pipe类完成，可以通过Pipe类提供的构造方法def Pipe(duplex)创建接收通道（conn_recv）与发送通道（conn_send）两个通信管道连接对象，构造方法中参数duplex有两种取值：

》duplex =True：默认设置，允许两个连接进行双向通信

》duplex = False：连接1（conn.recv）只允许接收数据，连接2（conn.send）只允许发送数据



——————————————————————————————————





##### 进程同步机制Semaphore

服务器能提供的资源量往往是有限的，所以当并发访问线程量较大时就需要针对所有的可用资源进行线程调度

这一点类似于银行办理业务

信号量可以通过multiprocessing模块中的Semaphore类实现，该类的操作方法与Lock类似。

**Semaphore类**本质上是一种**带有计数功能的进程同步机制**（acquire方法减少计数，replease方法增加计数，当可用进程的计数量为0时，则进程将会出现堵塞的情况）

```python
import multiprocessing,time
def worker(sem):
    if sem.acquire():
        print("【%s】进程开始执行。。。"%multiprocessing.current_process().name)
        time.sleep(1)
        sem.release()

def main():
    sem = multiprocessing.Semaphore(3)  #实例化Semaphore类，设置3个信息量，如果正在处理的进程数等于3个的时候，那么未获得操作资格的的其他进程则需要等待在线进程释放资源后再进行调度
    process = [multiprocessing.Process(target = worker, args = (sem,),name = "进程 - %s"%item)for item in range(10)]
    for process1 in process:
        process1.start()
        # time.sleep()
    for process1 in process:
        process1.join()

if __name__ == "__main__":
    main()
```

multiprocessing模块中又提供了一个**BoundedSemaphore类**，该类最大的特点是在使用release（）方法释放锁定资源时会查看计数是否超过上线，保证了正确的可用信息个数不超过限定范围



——————————————————————————————————————————————



##### Event

Event类提供了一个进程通信事件的管理操作，多个进程利用Event提供的阻塞标记实现等待与唤醒机制。









***



## 线程

### threading实现多线程

| 方法                                                         | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| def \__init__(self, group=None, target=None, name = None, args = (), kwargs=None,*,daemon=None) | 构造一个线程对象，参数作用如下。         》group：分组定义    》target：线程处理对象   》name：线程名称，如不设置，则自动分配一个名称   》args：线程处理对象所需要执行的参数   》kwargs：调用对象字典   》daemon：是否设置为后台线程 |
| def start(self)                                              | 线程启动                                                     |
| def run(self)                                                | 线程操作主体，若没设置target处理函数，则执行此方法           |
| def join(self , timeout=None)                                | 线程强制执行                                                 |
| def name(self)                                               | 获取线程名称                                                 |
| def ident（self）                                            | 获取线程标识                                                 |
| def is_alive(self)                                           | 判断线程存活状态                                             |







***



### Condition同步处理

在生产者与消费者模型中，为了实现两个操作线程的同步处理，则需要进行等待与唤醒的同步操作

（也就是说：当生产者未执行完毕，消费者应当等待生产者执行完毕后才可以消费数据，反之同理）

当各自的线程执行完毕后，则应当唤醒其他等待线程以继续执行后续操作



| 方法                                         | 描述                                |
| -------------------------------------------- | ----------------------------------- |
| def \__init__(self,lock = None)              | 设置锁类型，如不设置，则使用RLock锁 |
| def acquire(self,blocking =True,timeout =-1) | 获取同步锁                          |
| def wait(self, timeout = None)               | 线程等待                            |
| def notify(self, n =1 )                      | 唤醒一个等待进程对象                |
| def notify_all(self)                         | 唤醒所有进程                        |

**Condition通常与一个锁进行关联**，如果开发者在实例化Condition类对象时没有设置锁，则会默认使用RLock锁对象实现锁控制，所以在Condition类中会存在一个锁队列，同时还**会存在一个等待条件锁队列**，所有执行了**wait()操作的线程**在**等待条件锁队列中等待唤醒**（使用notify（）或者notigy_all()方法唤醒）

```

```







***





### ECHO程序模型

Echo是一个在客户端发送数据给服务端后，由服务端返回给客户端的数据，通常是由”【ECHO】+服务端接收的信息“组成



<u>此时的ECHO程序的客户端是基于单进程机制实现的网络通信，也就是说此时的服务器在同一时间内只允许一个客户端连接到服务器进行通信处理，并且当服务端退出之后服务器也将随之关闭，为了提高服务器端的性能，并且利用多进程de机制来处理多个客户端的通信需求</u>

```python
import multiprocessing, socket, re
SERVER_HOST = "localhost"
SEVER_PORT = 50000
def echo_handle(client_conn,address):
    #当连接上客户端后运行进程的处理函数，并且打开连接端口开始接收/处理信息
    print("客户端连接地址：%s 、 监听端口号：%s"%(SERVER_HOST,SEVER_PORT))
    with client_conn:
        while True:
            data = client_conn.recv(100).decode("UTF-8")
            print(data)
            match = re.match(r"\w*?\s*?BYEBYE",data.upper())
            if match:
                client_conn.send("exit".encode("UTF-8"))
                break
            else:
                client_conn.send(("【ECHO】%s"%data).encode("UTF-8"))

def main():
    with socket.socket() as server_socket:
        server_socket.bind((SERVER_HOST,SEVER_PORT))
        server_socket.listen()
        print(f"服务器启动完毕，在{SEVER_PORT}端口监听，等待客户端连接。。。")
        while True:
#等待客户端的连接，进入阻塞模式，并且在与客户端连接上时，创建一个新的端口进行接收/发送数据，并返回连接端口号
            client_conn, address = server_socket.accept()
			#连接到客户端后创建一个处理进程       
            multiprocess = multiprocessing.Process(target = echo_handle, args = (client_conn,address,), name = "服务器进程-%s"%address[1])
            multiprocess.start()
            print("服务端进程 - %s 开始运行"%(multiprocessing.current_process().pid,))

if __name__ == "__main__":
    main()
```





***



### UDP通信

UDP工作在传输层，采用数据报的形式进行数据交互，由于其采用的是无连接的处理协议，所以在传输的过程中可能会根据网络环境而出现数据丢失的情况

```python
'''
服务器端
'''
import socket
SERVER_HOST = "localhost"#通信地址
SERVER_POST = 50000		 #监听端口
def main():
    #通过socket.socket类创建了一个数据报“socket.SOCK_DGRAM”形式的服务器端口通信对象，并且将此服务器端的监听端口绑定在了主机50000端口
    with socket.socket(socket.AF_INET,socket.SOCK_DGRAM) as server_socket:
        server_socket.bind((SERVER_HOST,SERVER_POST))
        print("服务器启动完毕，在”%s“端口上监听，等待客户端连接...."%(SERVER_POST))
        while True:
            data, addr = server_socket.recvfrom(30)
            print(data.decode("UTF-8"))
            echo_data = ("【ECHO】%s"%data.decode("UTF-8")).encode("UTF-8")
            server_socket.sendto(echo_data,addr)

if __name__ == "__main__":
    main()
```

```python
'''
客户端
'''
import socket
SERVER_HOST = "localhost"
SERVER_POST = 50000
def main():
    with socket.socket(socket.AF_INET,socket.SOCK_DGRAM) as client_socket:
        while True:
            input_data = input("请输入你要发送的数据：")
            if input_data:
                client_socket.sendto(input_data.encode("UTF-8"),(SERVER_HOST,SERVER_POST))
                print("服务器端相应数据：%s"%client_socket.recv(30).decode("UTF-8"))
            else:
                break
if __name__ == "__main__":
    main()

```

本程序创建了一个UDP的通信对象，在进行网络通信时并不需要与服务器端进行连接，只需要 知道服务器端的地址即可实现数据通信下





***





### http服务器

```
参数一：地址簇

　　socket.AF_INET IPv4（默认）
　　socket.AF_INET6 IPv6

　　socket.AF_UNIX 只能够用于单一的Unix系统进程间通信

参数二：类型

　　socket.SOCK_STREAM　　流式socket , for TCP （默认）
　　socket.SOCK_DGRAM　　 数据报式socket , for UDP

　　socket.SOCK_RAW 原始套接字，普通的套接字无法处理ICMP、IGMP等网络报文，而SOCK_RAW可以；其次，SOCK_RAW也可以处理特殊的IPv4报文；此外，利用原始套接字，可以通过IP_HDRINCL套接字选项由用户构造IP头。
　　socket.SOCK_RDM 是一种可靠的UDP形式，即保证交付数据报但不保证顺序。SOCK_RAM用来提供对原始协议的低级访问，在需要执行某些特殊操作时使用，如发送ICMP报文。SOCK_RAM通常仅限于高级用户或管理员运行的程序使用。
　　socket.SOCK_SEQPACKET 可靠的连续数据包服务

参数三：协议

　　0　　（默认）与特定的地址家族相关的协议,如果是 0 ，则系统就会根据地址格式和套接类别,自动选择一个合适的协议
```







***





# OS模块

模块基本用法：

| 方法                                   | 描述                                                         |
| -------------------------------------- | ------------------------------------------------------------ |
| getcwd（）                             | 获取当前的工作目录                                           |
| chdir（path）                          | 修改工作目录                                                 |
| system（）                             | 执行操作系统命令                                             |
| popen（cmd, mode="r", buffering = -1） | 开启一个命令管道，方法中参数作用如下。    》cmd：要执行的命令    》mode：操作权限模式，可以是r或w    》buffering：设置缓冲大小，0表示不缓冲，1表示行缓冲，大于1表示全缓冲 |
| symlink（src， dst）                   | 创建软连接                                                   |
| link（src， dst）                      | 创建硬链接                                                   |





例：利用os模块在指定目录下创建目录

```python
import os
def main():
    os.chdir("d:/")
    os.system("md hello")
    print("在%s路径中创建hello子目录。 "%os.getcwd())

if __name__ == "__main__":
    main()
```



例：读取echo命令

功能说明：显示文字。

语 法：echo \[-ne][字符串]或 echo \[--help][--version]

```python
import os 
def main():
    #popen方法为调用本地命令，作用与system方法类似
    #echo为显示后面的文字，并且以可读的形式返回给fd，然后利用while循环将fd的信息按行打印出来
    fd = os.popen(cmd = "echo hello echo",mode = "r", buffering = 1)
    
    val = fd.readline()
    while val:
        print(val,end = "")
        val = fd.readline()
if __name__ == "__main__":
    main()
```



### OS.path子模块

| 方法                        | 描述                              |
| --------------------------- | --------------------------------- |
| abspath（path）             | 获取绝对路径                      |
| basename（path）            | 获取文件名称                      |
| dirname（path）             | 返回父路径                        |
| exists（path）              | 判断路径是否存在                  |
| expanduser（path）          | 将路径中的“~”替换为用户目录       |
| getatime（path）            | 返回最近访问时间                  |
| getmtime（path）            | 返回最近一次修改时间              |
| getctime（path）            | 返回创建时间                      |
| getsize（path）             | 返回文件大小                      |
| isabs（path）               | 判断给定路径是否为绝对路径        |
| isfile（path）              | 判断给定路径是否为文件            |
| isdir（path）               | 判断给定路径是否为目录            |
| islink（path）              | 判断给定路径是否为链接            |
| ismount（path）             | 判断给定路径是否为挂载点          |
| join（path[，path2[,...]]） | 路径合并                          |
| normcase（path）            | 规范化给定路径中的大小写和斜杠    |
| normpath（path）            | 规范化给定路径                    |
| realpath（path）            | 返回给定路径的真实路径            |
| samefile（path1，path2）    | 判断两个路径是否相同              |
| split（path）               | 将路径分隔为dirname和basename元组 |



os.path模块提供的路径变量

| 变量   | 描述                                                     |
| ------ | -------------------------------------------------------- |
| curdir | 表示当前文件夹“ . ”,一般可以省略                         |
| pardir | 上一层文件夹，例如：“ .. ”                               |
| sep    | 获取系统路径分隔符号，例如：windows为“ \ ”、Linux为“ / ” |
| extsep | 获取文件名称和后缀之间的间隔符号“ . ”                    |



例：使用os.path路径变量

```python
import os
PATH_A = "d:" + os.path.sep + '123' +os.path.extsep + "sh"
PATH_B = "d:" + os.path.sep + "123.sh"
def main():
    if os.path.samefile(PATH_A,PATH_B):
        print("这两个路径指向了同一个文件")
if __name__ == "__main__":
    main()
```





### twisted模块

由于并发编程以及单线程多线程的等待机制可能会出现的等待问题导致的硬件性能的利用并不是相当的好，所以出现了twisted模块



回调：

应用进程A让函数B做某件事情，并且继续执行别的事情，同时等待函数B的返回数据，好继续执行操作，而函数B要求应用进程A提供一个函数C作为参数传入函数B，让函数B能正常运行，函数B调用函数 C，然后继续执行自己的事，函数C执行完毕并返回数据，让函数B处理，然后函数B将所得到的数据处理后返回给应用进程A



异步调用：

应用进程的函数A通过建立新的线程来调用函数B，使得函数A无需等待函数B执行完毕过后才能继续执行。





***





## 函数式编程

概念：允许将一个函数作为参数传入另一个函数中，并且使其返回一个函数



————————

### map函数

格式：map(function,iterable)

function：为要对可迭代对象执行的一个操作

iterable：为将要执行操作的对象

例：

```python
def fun(x):
	return x*x
list = [1,2,3,4,5,6,7,8,9]
i = map(fun,list)
print(list(i))

```



———————

#### collections.nametuple()

collections.nametuple()是一个工厂函数，它用来创建一个自定义的tuple对象，也就是说他创建一个

自定义类，并且规定了tuple类的元素的个数，并且可以使用属性而不是索引来引用tuple中的元素

格式：collections.nametuple(类型，)





![1696742708587](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1696742708587.png)

当在定义包的时候，如果在包中定义了\_\_all__变量，那么在别的地方要使用这个包文件时只能使用\_\_all\_\_中定义好的



![1696744859883](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1696744859883.png)

`__main__` 是最高层级代码运行所在环境的名称。 “最高层级代码”即用户指定最先启动运行的 Python 模块。 它被称为“最高层级”是因为它将导入程序所需的所有其他模块。 有时“最高层级代码”也被称为应用的 *入口点*。





# python包

在物理上看，包就是一个文件夹，该文件夹下包含了一个\_\_init__.py文件，该文件夹可用于包含多个模块文件，从逻辑上看，包仍然是一个模块

**package包 = python模块文件  +  \_\_init__.py文件**

_\_init__.py文件其实是一个特殊的文件，只要这个文件存在于这个文件夹里面，那么它就是python包







# 串行和并行

从硬件设计上来讲，CPU 由专为顺序串行处理而优化的几个核心组成。另一方面，GPU 则由数以千计的更小、更高效的核心组成，这些核心专为同时处理多任务而设计。
![在这里插入图片描述](https://img-blog.csdnimg.cn/292cf2660f21465390760dfd7a32f030.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2hhcmxlcyBSZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)



