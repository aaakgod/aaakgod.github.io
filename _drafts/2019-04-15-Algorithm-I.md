---
layout: post
title: "The art of war-python-I"
subtitle: 'The art of war-python-I'
author: "Kgod"
header-style: text
tags:
  - Python
--- 

# 数据结构与算法（Python）
*课程参见:<a href="https://www.bilibili.com/video/av21540971/?p=2"> Python 兵法  </a>*

<!-- MarkdownTOC -->

- 一、引入概念
    - 1-01算法引入
    - 1-02 时间复杂度与大O表示法
    - 1-03-最坏时间复杂度与计算规则
    - 1-04-常见时间复杂度与大小关系
    - 1-05-代码执行时间测量模块
    - 1-07-Python列表与字典操作的时间复杂度
    - 1-08-数据结构引入
- 二、顺序表
    - 2-01 内存、类型本质、连续存储
    - 2-02 基本顺序表与元素外围顺序表
    - 2-03 顺序表的一体式结构与分离式结构
    - 2-04 顺序表数据区替换与扩充
    - 2-05 顺序表的操作
    - 2-06 Python中的顺序表
- 三、链表
    - 3-01 链表的提出
    - 3-02 单链表的ADT模型
    - 3-03 Python中变量标识的本质
    - 3-04 单链表及结点的定义代码
    - 3-05 单链表的操作与实现
    - 3-06 单链表与顺序表的对比
    - 3-07 双向链表
    - 3-08 双向链表操作与实现
    - 3-09 单向循环链表
    - 3-10 链表扩展
- 四、栈
    - 4-01 栈与队列的概念
    - 4-02 栈的实现
    - 4-03 队列与双端队列的实现

<!-- /MarkdownTOC -->

## 一、引入概念
**Python兵法**  
看题:  
如果 a+b+c=1000，且 a^2+b^2=c^2（a,b,c 为自然数），如何求出所有a、b、c可能的组合?

### 1-01算法引入
- 解法1:枚举法  

```python
import time

start_time = time.time()
for a in range(0,1001):
    for b in range(0,1001):
        for c in range(0,1001):
            if a+b+c == 1000 and a**2 + b**2 == c**2:
                print("a,b,c:%d,%d,%d"%(a,b,c))

end_time = time.time()
print("time:%d"%(end_time-start_time))
print("pao wan la...")
```
<img src="/picturesWork/the_art_of_war_python/01.png">

运行时间为80多秒,这跟计算机CPU等配置有关.  

- 算法提出:  
    - 算法是计算机处理信息的本质，因为计算机程序本质上是一个算法来告诉计算机确切的步骤来执行一个指定的任务。一般地，当算法在处理信息时，会从输入设备或数据的存储地址读取数据，把结果写入输出设备或某个存储地址供以后再调用。
    **算法是独立存在的一种解决问题的方法和思想。对于算法而言，实现的语言并不重要，重要的是思想。**

    - 算法的五大特性
        1. 输入: 算法具有0个或多个输入.
        2. 输出: 算法至少有1个或多个输出.
        3. 有穷性:算法在有限的步骤之后会自动结束而不会无限循环，并且每一个步骤可以在可接受的时间内完成.
        4. 确定性：算法中的每一步都有确定的含义，不会出现二义性.
        5. 可行性：算法的每一步都是可行的，也就是说每一步都能够执行有限的次数完成.

<!-- <table><tr><td bgcolor="#D1EEEE"><font  size="4" color="#dd00dd">一万年太久,只争朝夕</font></td></tr></table> -->
<font  size="4" color="#dd00dd" face="楷体">一万年太久,只争朝夕</font>

```python
import time

start_time = time.time()

for a in range(0,1001):
    for b in range(0,1001):
        c = 1000 - a - b
        if a**2 + b**2 == c**2:
            print("a,b,c:%d,%d,%d"%(a,b,c))

end_time = time.time()
print("time:%d"%(end_time-start_time))
print("pao wan la...")

```
<img src="/picturesWork/the_art_of_war_python/02.png">

### 1-02 时间复杂度与大O表示法
- 我们假定计算机执行算法每一个基本操作的时间是固定的一个时间单位，那么有多少个基本操作就代表会花费多少时间单位。算然对于不同的机器环境而言，确切的单位时间是不同的，但是对于算法进行多少个基本操作（即花费多少时间单位）在规模数量级上却是相同的，由此可以忽略机器环境的影响而客观的反应算法的时间效率。

- 对于算法的时间效率，我们可以用“大O记法”来表示。

### 1-03-最坏时间复杂度与计算规则
- 最坏时间复杂度:分析算法时，存在几种可能的考虑：  
    算法完成工作最少需要多少基本操作，即最优时间复杂度  
    算法完成工作最多需要多少基本操作，即最坏时间复杂度  
    算法完成工作平均需要多少基本操作，即平均时间复杂度  

- 时间复杂度的几条基本计算规则:
    - 基本操作，即只有常数项，认为其时间复杂度为$O(1)$.
    - 顺序结构，时间复杂度按加法进行计算.
    - 循环结构，时间复杂度按乘法进行计算.
    - 分支结构，时间复杂度取最大值.
    - 判断一个算法的效率时，往往只需要关注操作数量的最高次项，其它次要项和常数项可以忽略.
    - 在没有特殊说明时，我们所分析的算法的时间复杂度都是指最坏时间复杂度.

- 分析上述两种解法的时间复杂度:  
$$T_1(n) = O(n ^3)$$  
$$T_2(n) = O(n ^2)$$

### 1-04-常见时间复杂度与大小关系

执行次数函数举例   |   阶  
-----   |  ----
    $12$ |  $O(1)$
    $2n+3$ |  $O(n)$
    $3n^2+2n+1$ |  $O(n^2)$
    $5log_2 n +20$ |  $O(logn)$
    $2n+3nlog_2 n +19$ |  $O(nlogn)$
    $6n^3+2n^2+3n+2$ |  $O(n^3)$
    $2^n$ |  $O(2^n)$

<br>注意:经常将$log_2 n $ 写成$logn $.
<!-- <font  size="4" color="#dd0000">$O(1)<O(logn)<O(n)<O(nlogn)<O(n^2)<O(n^3)<O(2^n)<O(n!)<O(n^n)$</font> -->
<br>常见复杂度之间关系:
<table><tr><td bgcolor="#D1EEEE"><font  size="4" color="#dd0000">$O(1)<O(logn)<O(n)<O(nlogn)<O(n^2)<O(n^3)<O(2^n)<O(n!)<O(n^n)$</font> </td></tr></table>

### 1-05-代码执行时间测量模块
- 利用 **timeit** 模块  
    ```python
        class timeit.Timer(stmt='pass', setup='pass', timer=<timer function>)
    ```
    <br>Timer是测量小段代码执行速度的类。
    <br>stmt参数是要测试的代码语句（statment）；
    <br>setup参数是运行代码时需要的设置；
    <br>timer参数是一个定时器函数，与平台有关。  
 
    ```python
    timeit.Timer.timeit(number=1000000)
    ```
    Timer类中测试语句执行速度的对象方法。number参数是测试代码时的测试次数，默认为1000000次.

- list操作测试

    ```python
    def test1():
       l = []
       for i in range(1000):
          l = l + [i]

    def test2():
       l = []
       for i in range(1000):
          l.append(i)

    def test3():
       l = [i for i in range(1000)]

    def test4():
       l = list(range(1000))

    from timeit import Timer

    t1 = Timer("test1()", "from __main__ import test1")
    print("concat ",t1.timeit(number=1000), "seconds")

    t2 = Timer("test2()", "from __main__ import test2")
    print("append ",t2.timeit(number=1000), "seconds")

    t3 = Timer("test3()", "from __main__ import test3")
    print("comprehension ",t3.timeit(number=1000), "seconds")

    t4 = Timer("test4()", "from __main__ import test4")
    print("list range ",t4.timeit(number=1000), "seconds")

    ```
    <img src="/picturesWork/the_art_of_war_python/03.png">

- pop操作测试

    ```python
    from timeit import Timer
    x = list(range(2000000)) #注意此处range 返回的是对象 ,要转变为lsit
    pop_zero = Timer("x.pop(0)","from __main__ import x")
    print("pop_zero ",pop_zero.timeit(number=1000), "seconds")
    x = list(range(2000000))
    pop_end = Timer("x.pop()","from __main__ import x")
    print("pop_end ",pop_end.timeit(number=1000), "seconds")

    ```
    <img src="/picturesWork/the_art_of_war_python/04.png">

    从结果可以看出，pop最后一个元素的效率远远高于pop第一个元素.

<!-- 
<pre name="code" class="c++" face="Consolas"> 
　#include &lt;stdio.h> 
　#include &lt;cstring> 
　#include &lt;cstdio&gt; 
　 int main(int argc, char const *argv[])　 
　 { 
　　 int a = 1; 
　　 String str = "abc"; 
　 　scanf("%d", &a); 
　 cout &lt;&lt;"str:"&lt;&lt; str &lt;&lt; endl; 
　　　return 0; 
　　} 
</pre> -->

<!-- ### 1-06-Python列表类型不同操作的时间效率 -->

### 1-07-Python列表与字典操作的时间复杂度
- list 内置操作时间复杂度

    Operation   |   Big-O Efficiency  
    -----   |  ----
    index x[] |  $O(1)$
    index assignment |  $O(1)$
    append |  $O(1)$
    pop()  |  $O(1)$
    pop(i) |  $O(n)$
    insert(i,item) |  $O(n)$
    del operator |  $O(n)$
    iteration(迭代) |  $O(n)$
    contains(in) |  $O(n)$
    get slice[x:y] |  $O(k),k=y-x$
    del slice   |  $O(n)$
    set slice |  $O(n+k)$
    reverse |  $O(n)$
    concatenate |  $O(k)$
    sort |  $O(nlogn)$
    multiply |  $O(nk)$

- dict 内置操作时间复杂度

    Operation  |  Big-O Efficiency
    -------    |  -----
    copy       |    $O(n)$
    get item       |    $O(1)$
    set item       |    $O(1)$
    delete item    |    $O(1)$
    contains(in)   |    $O(1)$
    iteration      |    $O(n)$



### 1-08-数据结构引入
- 数据结构
    我们如何用Python中的类型来保存一个班的学生信息？ 如果想要快速的通过学生姓名获取其信息呢？

    实际上当我们在思考这个问题的时候，我们已经用到了数据结构。列表和字典都可以存储一个班的学生信息，但是想要在列表中获取一名同学的信息时，就要遍历这个列表，其时间复杂度为O(n)，而使用字典存储时，可将学生姓名作为字典的键，学生信息作为值，进而查询时不需要遍历便可快速获取到学生信息，其时间复杂度为O(1)。

    我们为了解决问题，需要将数据保存下来，然后根据数据的存储方式来设计算法实现进行处理，那么数据的存储方式不同就会导致需要不同的算法进行处理。我们希望算法解决问题的效率越快越好，于是我们就需要考虑数据究竟如何保存的问题，这就是数据结构。

    在上面的问题中我们可以选择Python中的列表或字典来存储学生信息。列表和字典就是Python内建帮我们封装好的两种数据结构。

- 概念
    数据是一个抽象的概念，将其进行分类后得到程序设计语言中的基本类型。如：int，float，char等。数据元素之间不是独立的，存在特定的关系，这些关系便是结构。数据结构指数据对象中数据元素之间的关系。

    Python给我们提供了很多现成的数据结构类型，这些系统自己定义好的，不需要我们自己去定义的数据结构叫做Python的内置数据结构，比如列表、元组、字典。而有些数据组织方式，Python系统里面没有直接定义，需要我们自己去定义实现这些数据的组织方式，这些数据组织方式称之为Python的扩展数据结构，比如栈，队列等。

- 算法与数据结构的区别
    - 数据结构只是静态的描述了数据元素之间的关系。
    - 高效的程序需要在数据结构的基础上设计和选择算法。
    - 程序 = 数据结构 + 算法

    **总结：算法是为了解决实际问题而设计的，数据结构是算法需要处理的问题载体**

- 抽象数据类型(Abstract Data Type)
    抽象数据类型(ADT)的含义是指一个数学模型以及定义在此数学模型上的一组操作。即把数据类型和数据类型上的运算捆在一起，进行封装。引入抽象数据类型的目的是把数据类型的表示和数据类型上运算的实现与这些数据类型和运算在程序中的引用隔开，使它们相互独立。

- 最常用的数据运算有五种：
    - 插入
    - 删除
    - 修改
    - 查找
    - 排序


## 二、顺序表
在程序中，经常需要将一组（通常是**同为某个类型的**）数据元素作为整体管理和使用，需要创建这种元素组，用变量记录它们，传进传出函数等。一组数据中包含的元素个数可能发生变化（可以增加或删除元素）。

对于这种需求，最简单的解决方案便是将这样一组元素看成一个序列，用元素在序列里的位置和顺序，表示实际应用中的某种有意义的信息，或者表示数据之间的某种关系。

这样的一组序列元素的组织形式，我们可以将其抽象为**线性表**。一个线性表是某类元素的一个集合，还记录着元素之间的一种顺序关系。线性表是最基本的数据结构之一，在实际程序中应用非常广泛，它还经常被用作更复杂的数据结构的实现基础。

根据线性表的实际存储方式，分为两种实现模型：
- **顺序表**,将元素顺序地存放在一块连续的存储区里，元素间的顺序关系由它们的存储顺序自然表示。
- **链表**，将元素存放在通过链接构造起来的一系列存储块中。

### 2-01 内存、类型本质、连续存储 
<img src="/picturesWork/the_art_of_war_python/05.jpeg">

### 2-02 基本顺序表与元素外围顺序表 
<img src="/picturesWork/the_art_of_war_python/06.jpeg">

### 2-03 顺序表的一体式结构与分离式结构 
<img src="/picturesWork/the_art_of_war_python/07.jpeg">

### 2-04 顺序表数据区替换与扩充 
- 一体式结构由于顺序表信息区与数据区连续存储在一起，所以若想更换数据区，则只能整体搬迁，即整个顺序表对象（指存储顺序表的结构信息的区域）改变了。

- 分离式结构若想更换数据区，只需将表信息区中的数据区链接地址更新即可，而该顺序表对象不变。

- 元素存储区扩充
    采用分离式结构的顺序表，若将数据区更换为存储空间更大的区域，则可以在不改变表对象的前提下对其数据存储区进行了扩充，所有使用这个表的地方都不必修改。只要程序的运行环境（计算机系统）还有空闲存储，这种表结构就不会因为满了而导致操作无法进行。人们把采用这种技术实现的顺序表称为动态顺序表，因为其容量可以在使用中动态变化。

- 扩充的两种策略

    - 每次扩充增加固定数目的存储位置，如每次扩充增加10个元素位置，这种策略可称为线性增长。
      特点：节省空间，但是扩充操作频繁，操作次数多。

    + 每次扩充容量加倍，如每次扩充增加一倍存储空间。
      特点：减少了扩充操作的执行次数，但可能会浪费空间资源。以空间换时间，推荐的方式。

### 2-05 顺序表的操作
- 增加元素
<img src="/picturesWork/the_art_of_war_python/08.png">
<br>a. 尾端加入元素，时间复杂度为$O(1)$
<br>b. 非保序的加入元素（不常见），时间复杂度为$O(1)$
<br>c. 保序的元素加入，时间复杂度为$O(n)$

- 删除元素
<img src="/picturesWork/the_art_of_war_python/09.png">
<br>a. 删除表尾元素，时间复杂度为$O(1)$
<br>b. 非保序的删除元素（不常见），时间复杂度为$O(1)$
<br>c. 保序的元素删除，时间复杂度为$O(n)$

### 2-06 Python中的顺序表
- Python中的list和tuple两种类型采用了顺序表的实现技术，具有前面讨论的顺序表的所有性质。
- tuple是不可变类型，即不变的顺序表，因此不支持改变其内部状态的任何操作，而其他方面，则与list的性质类似。
- list的基本实现技术
<br>Python标准类型list就是一种元素个数可变的线性表，可以加入和删除元素，并在各种操作中维持已有元素的顺序（即保序），而且还具有以下行为特征：
    - 基于下标（位置）的高效元素访问和更新，时间复杂度应该是O(1)；
    - 为满足该特征，应该采用顺序表技术，表中元素保存在一块连续的存储区中。
    - 允许任意加入元素，而且在不断加入元素的过程中，表对象的标识（函数id得到的值）不变。
    - 为满足该特征，就必须能更换元素存储区，并且为保证更换存储区时list对象的标识id不变，只能采用分离式实现技术。

    *在Python的官方实现中，**list就是一种采用分离式技术实现的动态顺序表**。这就是为什么用list.append(x) （或 list.insert(len(list), x)，即尾部插入）比在指定位置插入元素效率高的原因。*  

    *在Python的官方实现中，list实现采用了如下的策略：在建立空表（或者很小的表）时，系统分配一块能容纳8个元素的存储区；在执行插入操作（insert或append）时，如果元素存储区满就换一块4倍大的存储区。但如果此时的表已经很大（目前的阀值为50000），则改变策略，采用加一倍的方法。引入这种改变策略的方式，是为了避免出现过多空闲的存储位置。*

## 三、链表
### 3-01 链表的提出
- 为什么需要链表  
    1.顺序表的构建需要预先知道数据大小来申请连续的存储空间，而在进行扩充时又需要进行数据的搬迁，所以使用起来并不是很灵活。  
    2.链表结构可以充分利用计算机内存空间，实现灵活的内存动态管理。

- 链表的定义  
    链表（Linked list）是一种常见的基础数据结构，是一种线性表，但是不像顺序表一样连续存储数据，而是在每一个节点（数据存储单元）里存放下一个节点的位置信息（即地址）。
    <img src="/picturesWork/the_art_of_war_python/10.png">

### 3-02 单链表的ADT模型
- 抽象数据类型(**Abstract Data Type 简称ADT**)是指一个数学模型以及定义在此数学模型上的一组操作。抽象数据类型需要通过固有数据类型（高级编程语言中已实现的数据类型）来实现。抽象数据类型是与表示无关的数据类型，是一个数据模型及定义在该模型上的一组运算。

### 3-03 Python中变量标识的本质
<img src="/picturesWork/the_art_of_war_python/11.jpeg">
**python中的赋值操作改变的并不是内存中变量的值, 而是变量名指向的变量.**  
Python的变量本质是指针可以把Python的变量想象成便利贴，数据就存储在那里，发生赋值语句，就是把便利贴往数据存储地方贴例如 b = [3,4,5]：计算机为[3,4,5]这个数据开辟存储地址，然后赋值给变量b，就是把b这张便利贴往存储地址贴,a=b就是把a这张便利贴往b所在的地方贴，所以a和b贴的都是同一个地方，即：a和b指向同一个内存地址(同一个数据).

### 3-04 单链表及结点的定义代码
**单向链表也叫单链表，是链表中最简单的一种形式，它的每个节点包含两个域，一个信息域（元素域）和一个链接域。这个链接指向链表中的下一个节点，而最后一个节点的链接域则指向一个空值。**  
<img src="/picturesWork/the_art_of_war_python/12.png">  
    - 表元素域elem用来存放具体的数据。
    - 链接域next用来存放下一个节点的位置（python中的标识）
    - 变量p指向链表的头节点（首节点）的位置，从p出发能找到表中的任意节点。

**节点实现**

```python
class SingleNode(object):
    """单链表的节点"""
    def __init__(self,item):
        #item 存放数据元素
        self.item = item

        #next 是下一个节点的标识
        self.next = None
```

### 3-05 单链表的操作与实现
- is_empty() 链表是否为空
- length() 链表长度
- travel() 遍历整个链表
- add(item) 链表头部添加元素
- append(item) 链表尾部添加元素
- insert(pos, item) 指定位置添加元素
- remove(item) 删除节点
- search(item) 查找节点是否存在

实现:
<img src="/picturesWork/the_art_of_war_python/12_2.jpeg">
```python
class SingleNode(object):
    """单链表的节点"""
    def __init__(self,item):
        #item 存放数据元素
        self.item = item

        #next 是下一个节点的标识
        self.next = None

class SingleLinkList(object):
    """单链表"""
    def __init__(self):
        self.__head = None

    def is_empty(self):
        """判断列表是否为空"""
        return self.__head == None

    def length(self):
        """链表长度"""

        #cur 初始头节点
        cur = self.__head
        count = 0

        #尾节点指向None,此处循环跳出条件由count=0/1不同而定
        #完成一次遍历
        while cur != None:
            count += 1
            #cur节点往后移动
            cur = cur.next
        return count

    def travel(self):
        """遍历列表"""
        cur = self.__head
        #完成一次遍历
        while cur != None:
            print(cur.item,end = " ")
            cur = cur.next
        print(" ")

    def add(self,item):
        """链表头部添加元素"""
        #创造新添加的节点
        node = SingleNode(item)
        #将新节点指向头节点
        node.next = self.__head
        #将头__head指向新节点
        self.__head = node

    def append(self,item):
        """尾部添加"""
        node = SingleNode(item)
        #特殊情况 判断列表是否为空,空链表直接将__head指向新节点
        if self.is_empty():
            self.__head = node
        #若不是空,找到尾部,在将尾节点的next指向node
        else:
            #找尾部,完成一次遍历
            cur = self.__head
            while cur.next != None:
                cur = cur.next
            #指向None的最后一个节点改变指向到新添加的节点
            cur.next = node

    def insert(self,pos,item):#pos用来传插入位置
        """指定位置添加元素"""
        #判断 是否是头插法
        if pos <= 0:
            self.add(item)
        #判断 是否是尾插法
        elif pos > (self.length()-1):
            self.append(item)
        else:
            node = SingleNode(item)
            #找插入位置
            count = 0
            #pre 用来指向指定位置pos前一个位置pos-1,初始从头节点开始移动到指定位置
            pre = self.__head
            #找pos位置
            while count < (pos-1):
                count += 1
                pre = pre.next
            # 找到,现将Node的next指向插入位置的节点
            node.next = pre.next
            #在将插入位置的前一个节点的next指向新节点
            pre.next = node

    def remove(self,item):
        """删除节点"""
        cur = self.__head
        pre = None
        #找删除的节点
        while cur != None:
            #找到删除的元素
            if cur.item == item:
                #判断是否删除的是第一个节点
                if not pre:
                    #将头指针指向下一个节点
                    self.__head = cur.next
                else:
                    #将删除位置的前一个节点的next指向下一个pre
                    pre.next = cur.next
                #删除后要终止
                break
            else:
                #没找到往后移
                pre = cur
                cur = cur.next

    def search(self,item):
        """查找节点是否存在"""
        cur = self.__head
        #查找也要经过一次遍历
        while cur != None:
            if cur.item == item:
                return True
            #移动指针
            cur = cur.next
        return False



if __name__ == '__main__':
    """test"""
    ll = SingleLinkList()
    # print(ll.is_empty())
    # print(ll.length())

    # ll.append(1)
    # print(ll.is_empty())
    # print(ll.length())

    # ll.add(1)
    # ll.add(2)
    # ll.append(3)
    # ll.insert(2,4)#看参数传递,此处是在第2个位置插入元素4
    # print("ll'length :%d"%ll.length())
    # ll.travel()
    ll.append(2)
    ll.add(8)
    ll.append(3)
    ll.append(4)
    ll.append(5)
    ll.append(6)
    ll.insert(-1, 9)
    ll.insert(3,100)
    ll.insert(10,100)
    ll.remove(100)
    ll.travel()
    print(ll.search(100))
```

### 3-06 单链表与顺序表的对比
链表失去了顺序表随机读取的优点，同时链表由于增加了结点的指针域，空间开销比较大，但对存储空间的使用要相对灵活。链表与顺序表的各种操作复杂度如下所示:

操作  |  链表  |  顺序表
---- |  ----  |  ----
访问元素 | $O(n)$ | $O(1)$
头部插入/删除  | $O(1)$ | $O(n)$
尾部插入/删除  | $O(n)$ | $O(1)$
中间插入/删除  | $O(n)$ | $O(n)$

*注意虽然表面看起来复杂度都是 O(n)，但是链表和顺序表在插入和删除时进行的是完全不同的操作。链表的主要耗时操作是遍历查找，删除和插入操作本身的复杂度是O(1)。顺序表查找很快，主要耗时的操作是拷贝覆盖。因为除了目标元素在尾部的特殊情况，顺序表进行插入和删除时需要对操作点之后的所有元素进行前后移位操作，只能通过拷贝和覆盖的方法进行。*

### 3-07 双向链表
- 一种更复杂的链表是“双向链表”或“双面链表”。每个节点有两个链接：一个指向前一个节点，当此节点为第一个节点时，指向空值；而另一个指向下一个节点，当此节点为最后一个节点时，指向空值。  
<img src="/picturesWork/the_art_of_war_python/14.png">

### 3-08 双向链表操作与实现
- 操作与单向链表一样
- 实现:
<img src="/picturesWork/the_art_of_war_python/14_2.jpeg">

```python
#
#File Name:04-DlintList.py
#Author:Kgod
#Email:17621512033@163.com
#Create Date:2019-04-18 17:04:45
#Last Modified:2019年04月28日 星期日 21时35分34秒
#Description:
#/
class DoubleNode(object):
    """双链表的节点"""
    def __init__(self,item):
        #item 存放数据元素
        self.item = item

        #next 是下一个节点的标识
        self.next = None
        self.prev = None

class DlinkList(object):
    """双链表"""
    def __init__(self):
        self.__head = None

    def is_empty(self):
        """判断列表是否为空"""
        return self.__head is None

    def length(self):
        """链表长度"""

        #cur 初始头节点
        cur = self.__head
        count = 0

        #尾节点指向None,此处循环跳出条件由count=0/1不同而定
        #完成一次遍历
        while cur != None:
            count += 1
            #cur节点往后移动
            cur = cur.next
        return count

    def travel(self):
        """遍历列表"""
        cur = self.__head
        #完成一次遍历
        while cur != None:
            print(cur.item,end = " ")
            cur = cur.next
        print(" ")

    def add(self,item):
        """链表头部添加元素"""
        #创造新添加的节点
        node = DoubleNode(item)

        #如果是空链表,将__head指向node
        if self.is_empty():
            self.__head = node
        else:
            #将node的next指向__head的头节点
            node.next = self.__head
            #将__head的头节点的prev指向node
            self.__head.prev = node
            #将__head指向node
            self.__head = node

            """或者这样:
            #将node的next指向__head的头节点
            node.next = self.__head
            #将__head指向node
            self.__head = node
            #将node的next的prev指向node
            node.next.prev = node
            """
    def append(self,item):
        """尾部添加"""
        node = DoubleNode(item)
        #特殊情况 判断列表是否为空,空链表直接将__head指向新节点
        if self.is_empty():
            self.__head = node
        else:
            #若不是空,移到链表尾部
            cur = self.__head
            while cur.next != None:
                cur = cur.next
            #指向None的最后一个节点改变指向到新添加的节点
            cur.next = node
            #将node的prev指向cur
            node.prev = cur

    def insert(self,pos,item):#pos用来传插入位置
        """指定位置添加元素"""
        #判断 是否是头插法
        if pos <= 0:
            self.add(item)
        #判断 是否是尾插法
        elif pos > (self.length()-1):
            self.append(item)
        else:
            node = DoubleNode(item)
            #找插入位置
            count = 0
            cur = self.__head
            while count < pos:
                count += 1
                cur = cur.next
            #当循环退出,cur指向指定位置pos

            #node的next指向cur
            node.next = cur
            #node的prev指向cur的prev
            node.prev = cur.prev
            #cur的prev的next指向node
            cur.prev.next = node
            #cur的prev指向node
            cur.prev = node

            '''或者:
            #node的next指向cur
            node.next = cur
            #node的prev指向cur的prev
            node.prev = cur.prev
            #cur的prev指向node
            cur.prev = node
            #node的prev的next指向node
            node.prev.next = node
            '''


    def remove(self,item):
        """删除节点"""
        cur = self.__head
        pre = None
        #找删除的节点
        while cur != None:
            #找到删除的元素
            if cur.item == item:
                #判断是否删除的是第一个节点
                if not pre:
                    #将头指针指向下一个节点
                    self.__head = cur.next
                else:
                    #将删除位置的前一个节点的next指向下一个pre
                    pre.next = cur.next
                #删除后要终止
                break
            else:
                #没找到往后移
                pre = cur
                cur = cur.next

    def search(self,item):
        """查找节点是否存在"""
        cur = self.__head
        #查找也要经过一次遍历
        while cur != None:
            if cur.item == item:
                return True
            #移动指针
            cur = cur.next
        return False

if __name__ == '__main__':

    ll = DlinkList()
    print(ll.is_empty())
    print(ll.length())

    ll.append(1)
    print(ll.is_empty())
    # print(ll.length())

    # ll.add(1)
    # ll.add(2)
    # ll.append(3)
    # ll.insert(2,4)#看参数传递,此处是在第2个位置插入元素4
    # print("ll'length :%d"%ll.length())
    # ll.travel()
    ll.append(2)
    ll.add(8)
    ll.append(3)
    ll.append(4)
    ll.append(5)
    ll.append(6)
    ll.insert(-1, 9)
    ll.insert(3,100)
    ll.insert(10,100)
    ll.remove(100)
    ll.travel()
    print(ll.search(100))
```

### 3-09 单向循环链表
- 单链表的一个变形是单向循环链表，链表中最后一个节点的next域不再为None，而是指向链表的头节点。
<img src="/picturesWork/the_art_of_war_python/15.png">

- 操作与单向链表一样
- 实现:
<img src="/picturesWork/the_art_of_war_python/15_2.jpeg">

```python
#
#File Name:05-Single-cycle-link-list.py
#Author:Kgod
#Email:17621512033@163.com
#Create Date:2019-04-18 17:04:45
#Last Modified:2019年05月02日 星期四 13时11分15秒
#Description:
#/
class Node(object):
    """单链表的节点"""
    def __init__(self,item):
        #item 存放数据元素
        self.item = item
        #next 是下一个节点的标识
        self.next = None

class SinCycleLinkList(object):
    """单链表"""
    def __init__(self):
        self.__head = None

    def is_empty(self):
        """判断列表是否为空"""
        return self.__head is None

    def length(self):
        """返回链表长度"""
        if self.is_empty():
            return 0

        #cur 初始头节点
        cur = self.__head
        count = 1#此处从1开始
        #尾节点指向None,此处循环跳出条件由count=0/1不同而定
        #完成一次遍历
        while cur.next is not self.__head:
            count += 1
            #cur节点往后移动
            cur = cur.next
        return count

    def travel(self):
        """遍历列表"""
        if self.is_empty():
            return

        cur = self.__head
        while cur.next is not self.__head:
            print(cur.item,end = " ")
            cur = cur.next
        #退出循环,cur指向尾结点,但是尾结点未打印
        print(cur.item)

    def add(self,item):
        """链表头部添加元素 头插法"""
        node = Node(item)
        if self.is_empty():
            #头结点指向node
            self.__head = node
            #node.next指向自身
            node.next = node

        else:
            # #将新节点指向头节点
            # node.next = self.__head
            # #将头__head指向新节点
            # self.__head = node
            # #寻找原始尾结点
            # while cur.next is not node.next:
                # cur = cur.next
            # #原始尾结点指向node
            # cur.next = node

            #先找尾结点
            cur = self.__head
            while cur.next is not self.__head:
                cur = cur.next
            node.next = self.__head
            self.__head = node
            cur.next = node #or cur.next = self.__head

    def append(self,item):
        """尾部添加 尾插法"""
        node = Node(item)
        #特殊情况 判断列表是否为空,空链表直接将__head指向新节点,自身指向自身
        if self.is_empty():
            self.__head = node
            node.next = node
        #若不是空,找到尾部,在将尾节点的next指向node,node指向self.__head
        else:
            #找尾部,完成一次遍历
            cur = self.__head
            while cur.next is not self.__head:
                cur = cur.next
            cur.next = node
            node.next = self.__head

    def insert(self,pos,item):#pos用来传插入位置
        """指定位置添加元素 与单链表一模一样"""
        #判断 是否是头插法
        if pos <= 0:
            self.add(item)
        #判断 是否是尾插法
        elif pos > (self.length()-1):
            self.append(item)
        else:
            node = Node(item)
            #找插入位置
            count = 0
            #pre 用来指向指定位置pos前一个位置pos-1,初始从头节点开始移动到指定位置
            pre = self.__head
            #找pos位置
            while count < (pos-1):
                count += 1
                pre = pre.next
            # 找到,现将Node的next指向插入位置的节点
            node.next = pre.next
            #在将插入位置的前一个节点的next指向新节点
            pre.next = node

    def remove(self,item):
        """删除节点"""
        if self.is_empty():
            return 

        cur = self.__head
        pre = None
        #找删除的节点
        while cur.next is not self.__head:
            if cur.item == item:
                # 判断是否删除的是第一个节点
                if cur == self.__head:
                    #头结点情况
                    #先找尾结点
                    rear = self.__head
                    while   rear.next is not self.__head:
                        rear = rear.next
                    #将头指针指向cur.next
                    self.__head = cur.next
                    rear.next = self.__head
                else:
                    #中间结点
                    #将删除位置的前一个节点的next指向下一个pre
                    pre.next = cur.next
                #删除后要终止
                return
            else:
                #没找到往后移
                pre = cur
                cur = cur.next
        #退出循环,cur指向尾结点
        if cur.item == item:
            if cur == self.__head:
            #只有一个结点
                self.__head = None
            else:
                #pre.next = cur.next or
                pre.next = self.__head

    def search(self,item):
        """查找结点是否存在"""
        if self.is_empty():
            return False

        cur = self.__head
        #查找也要经过一次遍历
        while cur.next is not self.__head:
            if cur.item == item:
                return True
            #移动指针
            else:
                cur = cur.next
        #退出循环,尾结点没有判断
        if cur.item == item:
            return True
        return False

if __name__ == '__main__':

    ll = SinCycleLinkList()
    print(ll.is_empty())
    print(ll.length())
    ll.append(1)
    print(ll.is_empty())
    print(ll.length())
    ll.append(2)
    ll.add(8)
    ll.append(3)
    ll.append(4)
    ll.append(5)
    ll.append(6)# 8 1 2 3 4 5 6
    ll.insert(-1, 9) # 9 8 1 23456
    ll.travel()
    ll.insert(3, 100) # 9 8 1 100 2 3456
    ll.travel()
    ll.insert(10, 200) # 9 8 1 100 23456 200
    ll.travel()
    ll.remove(100)
    ll.travel()
    ll.remove(9)
    ll.travel()
    ll.remove(200)
    ll.travel()
```

### 3-10 链表扩展


## 四、栈

### 4-01 栈与队列的概念
- 栈（stack），有些地方称为堆栈，是一种容器，可存入数据元素、访问元素、删除元素，它的特点在于**只能允许在容器的一端（称为栈顶端指标，英语：top）进行加入数据（英语：push）和输出数据（英语：pop）的运算**。没有了位置概念，保证任何时候可以访问、删除的元素都是此前最后存入的那个元素，确定了一种默认的访问顺序。
- **由于栈数据结构只允许在一端进行操作，因而按照后进先出（LIFO, Last In First Out）的原理运作**。
<img src="/picturesWork/the_art_of_war_python/16.png">

- 队列（queue）是只允许在一端进行插入操作，而在另一端进行删除操作的线性表。
- **队列是一种先进先出的（First In First Out）的线性表，简称FIFO**。允许插入的一端为队尾，允许删除的一端为队头。队列不允许在中间部位进行操作！假设队列是q=（a1，a2，……，an），那么a1就是队头元素，而an是队尾元素。这样我们就可以删除时，总是从a1开始，而插入时，总是在队列最后。这也比较符合我们通常生活中的习惯，排在第一个的优先出列，最后来的当然排在队伍最后。
<img src="/picturesWork/the_art_of_war_python/17.png">

- 双端队列（deque，全名double-ended queue），是一种具有队列和栈的性质的数据结构。**双端队列中的元素可以从两端弹出，其限定插入和删除操作在表的两端进行。双端队列可以在队列任意一端入队和出队。**
<img src="/picturesWork/the_art_of_war_python/18.png">


### 4-02 栈的实现
- 栈可以用顺序表实现，也可以用链表实现。
- 栈的操作
    - Stack() 创建一个新的空栈
    - push(item) 添加一个新的元素item到栈顶
    - pop() 弹出栈顶元素
    - peek() 返回栈顶元素
    - is_empty() 判断栈是否为空
    - size() 返回栈的元素个数
- 实现:

```python

class Stack(object):
    """栈"""
    def __init__(self):
        self.items = []

    def is_empty(self): 
        """判断栈是否为空"""
        return self.items == []

    def push(self,item): 
        """添加一个新的元素item到栈顶"""
        self.items.append(item)
    
    def pop(self): 
        """弹出栈顶元素"""
        return self.items.pop() #pop默认最后一个元素

    def peek(self): 
        """返回栈顶元素"""
        # return self.items[len(self.items-1)]
        if self.items:
            return self.items[-1]
        else:
            return None
    
    def size(self): 
        """返回栈的元素个数"""
        return len(self.items)

if __name__ == "__main__":
    stack = Stack()
    stack.push("hello")
    stack.push("world")
    stack.push("itcast")
    print (stack.size())
    print (stack.peek())
    print (stack.pop())
    print (stack.pop())
    print (stack.pop())

```

### 4-03 队列与双端队列的实现
- 同栈一样，队列也可以用顺序表或者链表实现。
- 操作
    - Queue() 创建一个空的队列
    - enqueue(item) 往队列中添加一个item元素
    - dequeue() 从队列头部删除一个元素
    - is_empty() 判断一个队列是否为空
    - size() 返回队列的大小
- 实现:

```python

class queue(object):
    """队列"""
    def __init__(self):
        self.__list = []

    def enqueue(self,item):
        """往队列中添加一个item元素"""
        self.__list.append(item) #从尾部添加,与pop(0)搭配
        # self.__list.insert(0,item) #从第0个位置插入,与pop()搭配

    def dequeue(self): 
        """从队列头部删除一个元素"""
        return self.__list.pop(0) #默认从末尾删除,需加参数
        # return self.__list.pop() #默认从末尾删除,需加参数

    def is_empty(self):
        """判断一个队列是否为空"""
        return self.__list == []

    def size(self):
        """返回队列的大小"""
        return len(self.__list)


if __name__ == "__main__":
    s = queue()
    s.enqueue(1)
    s.enqueue(2)
    s.enqueue(3)
    s.enqueue(4)
    print(s.dequeue())
    print(s.dequeue())
    print(s.dequeue())
    print(s.dequeue())
```

- 双端队列实现:
- 操作
    - Deque() 创建一个空的双端队列
    - add_front(item) 从队头加入一个item元素
    - add_rear(item) 从队尾加入一个item元素
    - remove_front() 从队头删除一个item元素
    - remove_rear() 从队尾删除一个item元素
    - is_empty() 判断双端队列是否为空
    - size() 返回队列的大小
    
```python

class Dqueue(object):
    def __init__(self):
        self.__list = []

    def add_front(self,item):
        """从队头加入一个item元素"""        
        return self.__list.insert(0,item)

    def add_rear(self,item):
        """从队尾加入一个item元素"""
        return self.__list.insert(-1,item)
        # return self.__list.append(item)

    def remove_front(self):
        """从队头删除一个item元素"""
        return self.__list.pop(0)

    def remove_rear(self):
        """从队尾删除一个item元素"""
        return self.__list.pop()
     
    def is_empty(self):
        """判断双端队列是否为空"""
        return self.__list == []

    def size(self):
        """返回队列的大小"""
        return len(self.__list)


if __name__ == "__main__":
    deque = Dqueue()
    deque.add_front(1)
    deque.add_front(2)
    deque.add_rear(3)
    deque.add_rear(4)
    print(deque.size())
    print(deque.remove_front())
    print(deque.remove_front())
    print(deque.remove_rear())
    print(deque.remove_rear())
```

