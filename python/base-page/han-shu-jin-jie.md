# 函数进阶

## 1 函数参数和返回值的作用

1. 如果函数 **内部处理的数据不确定**，就可以将外界的数据以参数传递到函数内部
2. 如果希望一个函数 **执行完成后，向外界汇报执行结果**，就可以增加函数的返回值

### 1.1 无参数，无返回值

此类函数，不接收参数，也没有返回值，应用场景如下：

1. **只是单纯地做一件事情**，例如 **显示菜单**
2. 在函数内部 **针对全局变量进行操作**，例如：**新建名片**，最终结果 **记录在全局变量** 中

* 如果全局变量的数据类型是一个 **可变类型**，在函数内部可以使用 **方法** 修改全局变量的内容 —— **变量的引用不会改变**
* 在函数内部，**使用赋值语句** 才会 **修改变量的引用**

### 1.2 无参数，有返回值

此类函数，不接收参数，但是有返回值，应用场景如下：

* 采集数据，例如 **温度计**，返回结果就是当前的温度，而不需要传递任何的参数

### 1.3 有参数，无返回值

此类函数，接收参数，没有返回值，应用场景如下：

* 函数内部的代码保持不变，针对 **不同的参数 处理 不同的数据**
* 例如 **名片管理系统** 针对 **找到的名片** 做 **修改**、**删除** 操作

### 1.4 有参数，有返回值

此类函数，接收参数，同时有返回值，应用场景如下：

* 函数内部的代码保持不变，针对 **不同的参数 处理 不同的数据**，并且 **返回期望的处理结果**
* 例如 **名片管理系统** 使用 **字典默认值** 和 **提示信息** 提示用户输入内容
  * 如果输入，返回输入内容
  * 如果没有输入，返回字典默认值

## 2 函数的返回值 -- 进阶

* 在程序开发中，有时候，会希望 **一个函数执行结束后，告诉调用者一个结果**，以便调用者针对具体的结果做后续的处理
* **返回值** 是函数 **完成工作**后，**最后** 给调用者的 **一个结果**
* 在函数中使用 `return` 关键字可以返回结果
* 调用函数一方，可以 **使用变量** 来 **接收** 函数的返回结果

```python
def measure():
    """返回当前的温度"""
    
    print("开始测量")
    temp = 39
    print("测量结束...")
    
    return temp
result = measure()
print(result)

#-----------------------------

# 再利用元组在返回温度的同时，返回湿度
# 改造如下：
def measure():
    """返回当前的温度"""

    print("开始测量...")
    temp = 39
    wetness = 10
    print("测量结束...")

    # 小括号可以省略 return (temp, wetness)
    return temp, wetness # 没有小括号是返回了元组

# result 是元组
result = measure() 
print(result)

# 需要单独的处理温度或者湿度  --- 不方便
print(result[0])
print(result[1])

# 如果函数返回的类型是元组，同时希望单独的处理元组中的元素
# 可以使用多个变量，一次接受函数的返回结果
gl_temp,gle_wetness = measure()
print(gl_temp)
print(gle_wetness)
```

使用 `return` 时，元组可以不用小括号

技巧：将一个元组 使用 赋值语句 同时赋值给多个变量

#### 【面试题】交换两个数字

题目要求：

有两个整数变量 `a = 6`, `b = 100`不使用其他变量，**交换两个变量的值**

```python
# 第一种方法
a = a + b
b = a - b
a = a - b

# 第二种方法
# python专属，利用元组

a,b =(b,a)

```

## 3 函数的参数--进阶

### 3.1 不可变和可变的参数

在函数内部，针对参数使用 **赋值语句**，不会影响调用函数时传递的 **实参变量**

**只要针对参数使用赋值语句，会在函数内部修改局部变量的引用，不会影响到外部变量的引用**

如果传递的参数是可变类型，在函数内部，使用方法修改了数据的内容，同样会影响到外部的数据

#### 3.1.1 面试题  关于+=操作

在python中，<mark style="color:blue;">**列表变量**</mark>调用 += 本质上是在执行列表变量的extend方法，不会修改变量的引用

```python
def demo(num,num_list):
    print("函数开始")
    
    num += num
    # 列表变量使用 + 不会做相加再赋值的操作
    # num_list = num_list + numlist
    # 本质上是在调用列表的extend方法
    # num_list += num_list
    num_list.extend(num_list)
    
    print(num)
    print(num_list)
    
    print("函数完成")
    
gl_num = 9
gl_list = [1,2,3]
demo(gl_num,gl_list)
print(gl_num)
print(gl_list)
```

### 3.2 缺省参数

定义函数时，可以给 **某个参数** 指定一个**默认值**，具有默认值的参数就叫做 **缺省参数**

```python
gl_list = [6,3,9]

# 默认升序
gl_list.sort()

# 降序
gl_list.sort(reverse=True) # reverse就是缺省函数，默认false

print(gl_list)

```

#### 3.2.1 指定函数的缺省参数

在参数后使用赋值语句，可以指定参数的缺省值

```python
def print_info(name, gender=True):

    gender_text = "男生"
    if not gender:
        gender_text = "女生"

    print("%s 是 %s" % (name, gender_text))
 # 在指定缺省函数的默认值时，应该使用最常见的值作为默认值   
print_info("小明")
print_info("小妹",False)
```

#### 3.2.2 缺省参数注意事项

1. 缺省参数的定义位置\
   必须保证 带有默认值的缺省参数 在参数列表末尾
2. 调用带有多个缺省参数的函数\
   在调用函数时，如果有多个缺省参数，需要制定参数名。

### 3.3 多值参数

#### 3.3.1 定义支持多值参数的函数

* `python` 中有 **两种** 多值参数：
  * 参数名前增加 **一个** `*` 可以接收 **元组**
  * 参数名前增加 **两个** `*` 可以接收 **字典**
* 一般在给多值参数命名时，**习惯**使用以下两个名字
  * `*args` —— 存放 **元组** 参数，前面有一个 `*`
  * `**kwargs` —— 存放 **字典** 参数，前面有两个 `*`
* `args` 是 `arguments` 的缩写，有变量的含义
* `kw` 是 `keyword` 的缩写，`kwargs` 可以记忆 **键值对参数**

```python
def demo(num, *args, **kwargs):

    print(num)
    print(args)
    print(kwargs)


demo(1, 2, 3, 4, 5, name="小明", age=18, gender=True)
```

#### 3.3.2 多值参数案例 —— 计算任意多个数字的和

需求：1. 定义一个函数，可以接受 任意多个整数；

### 3.4  元组和字典的拆包

* 在调用带有多值参数的函数时，如果希望：
  * 将一个 **元组变量**，直接传递给 `args`
  * 将一个 **字典变量**，直接传递给 `kwargs`
* 就可以使用 **拆包**，简化参数的传递，**拆包** 的方式是：
  * 在 **元组变量前**，增加 **一个** `*`
  * 在 **字典变量前**，增加 **两个** `*`

```python
def demo(*args, **kwargs):

    print(args)
    print(kwargs)


# 需要将一个元组变量/字典变量传递给函数对应的参数
gl_nums = (1, 2, 3)
gl_xiaoming = {"name": "小明", "age": 18}

# 会把 num_tuple 和 xiaoming 作为元组传递个 args
# demo(gl_nums, gl_xiaoming)
demo(*gl_nums, **gl_xiaoming)

```

## 4 函数递归

### 4.1 递归函数的特点

一个函数 内部 调用自己

1. 函数内部的 **代码** 是相同的，只是针对 **参数** 不同，**处理的结果不同**
2. 当 **参数满足一个条件** 时，函数不再执行
   * **这个非常重要**，通常被称为递归的出口，否则 **会出现死循环**！

```python
def sum_numbers(num):

    print(num)
    
    # 递归的出口很重要，否则会出现死循环
    if num == 1:
        return

    sum_numbers(num - 1)
    
sum_numbers(3)
```

### 4.2 递归案例 —— 计算数字累加

计算1+2...+num的结果

```python
def sum_number(num):
    if num ==1:
        return 1
    
    # 假设 sum_number 能够完成 num -1 的累加
    temp = sum_number(num - 1)
    
    # 函数内部的核心算法就是 两个数字的相加
    
    return num + temp

print(sum_number(5))
```

在处理 **不确定的循环条件时**，格外的有用
