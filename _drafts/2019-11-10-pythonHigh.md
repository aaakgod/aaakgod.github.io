---
layout: post
title: "Python-HighLever"
subtitle: 'python高级编程'
author: "Kgod"
header-style: text
tags:
  - python
---
<!-- MarkdownTOC -->

- 1.深拷贝、浅拷贝
    - A. 浅拷⻉
    - B. 深拷⻉
    - C.拷贝的其他方式
- 2.私有化
- 3.属性property
    - 1. 私有属性添加getter和setter⽅法
    - 2. 使⽤property升级getter和setter⽅法
    - 3. 使⽤property取代getter和setter⽅法
- 4.生成器
    - 1. 什么是⽣成器
    - 2. 创建⽣成器⽅法1
    - 3.创建⽣成器⽅法2 **yield**
    - 4.send
    - 5.多任务\(看上去同时执行\)
- 5.迭代器
    - A. 可迭代对象
    - B. 判断是否可以迭代
    - C.迭代器
    - D.iter\(\)函数
    - 总结
- 6.闭包
    - A. 函数引⽤
    - B.什么是闭包
    - C.闭包例子
- 7.装饰器
    - A.明白：
    - B.需求来了
    - C.多个装饰器
    - D.装饰器什么时候进行装饰
    - E.使用装饰器对无参数的函数进行装饰
    - F.使用装饰器对有参数的函数进行装饰
    - G.使用装饰器对有不定长参数的函数进行装饰
    - H.使用装饰器对有返回值的函数进行装饰
    - I.使用通用的装饰器完成对函数进行装饰
    - J.有参数的装饰器

<!-- /MarkdownTOC -->

# 1.深拷贝、浅拷贝

### A. 浅拷⻉
浅拷⻉是对于⼀个对象的顶层拷⻉  
通俗的理解是：拷⻉了引⽤，并没有拷⻉内容
<img src="/picturesWork/pythonHigh/001.png">

### B. 深拷⻉
深拷⻉是对于⼀个对象所有层次的拷⻉(递归)
<img src="/picturesWork/pythonHigh/002.png">
<img src="/picturesWork/pythonHigh/003.png">
<img src="/picturesWork/pythonHigh/006.png">

### C.拷贝的其他方式
浅拷⻉对不可变类型和可变类型的copy不同
<img src="/picturesWork/pythonHigh/004.png">
<img src="/picturesWork/pythonHigh/005.png">

# 2.私有化

- xx: 公有变量
- _x: 单前置下划线,私有化属性或⽅法，from somemodule import *禁⽌导⼊,类对象和⼦类可以访问
- __xx：双前置下划线,避免与⼦类中的属性命名冲突，⽆法在外部直接访问(名字重整所以访问不到)
- __xx__:双前后下划线,⽤户名字空间的魔法对象或属性。例如: __init__ , __ 不要⾃⼰发明这样的名字
- xx_:单后置下划线,⽤于避免与Python关键词的冲突  

通过name mangling（名字重整(⽬的就是以防⼦类意外重写基类的⽅法或者属性)如：_Class__object）机制就可以访问private了：

```python
class Test(object):
    def __init__(self):
       self.__num = 100

    def setNum(self, newNum):
        self.__num = newNum

    def getNum(self):
        return self.__num


t = Test()
#print(t.__num)
#t.__num = 200

print(t.getNum())
t.setNum(50)
print(t.getNum())
```


# 3.属性property
### 1. 私有属性添加getter和setter⽅法
```python
class Money(object):
    def __init__(self):
        self.__money = 0
    def getMoney(self):
        return self.__money
    def setMoney(self, value):
        if isinstance(value, int):
            self.__money = value
        else:
            print("error:不是整型数字")
```
### 2. 使⽤property升级getter和setter⽅法
```python
class Money(object):
    def __init__(self):
        self.__money = 0
    def getMoney(self):
        return self.__money
    def setMoney(self, value):
        if isinstance(value, int):
            self.__money = value
        else:
            print("error:不是整型数字")
    money = property(getMoney, setMoney)
```
<img src="/picturesWork/pythonHigh/007.png">

### 3. 使⽤property取代getter和setter⽅法
@property 成为属性函数，可以对属性赋值时做必要的检查，并保证代码的清晰短⼩，主要有2个作⽤:
- 将⽅法转换为只读
- 重新实现⼀个属性的设置和读取⽅法,可做边界判定

```python
class Money(object):
    def __init__(self):
        self.__money = 0
    @property
    def money(self):
        return self.__money
    @money.setter
    def money(self, value):
        if isinstance(value, int):
            self.__money = value
        else:
            print("error:不是整型数字")
```
<img src="/picturesWork/pythonHigh/008.png">

```python
class Test(object):
    def __init__(self):
       self.__num = 100

    def setNum(self, newNum):
        print("----setter----")
        self.__num = newNum

    def getNum(self):
        print("----getter----")
        return self.__num

    num = property(getNum, setNum)


t = Test()
#print(t.__num)
#t.__num = 200

#print(t.getNum())
#t.setNum(50)
#print(t.getNum())

print("-"*50)

t.num = 200 #相当于调用了 t.setNum(200)

print(t.num) #相当于调用了 t.getNum()

#注意点:
#t.num 到底是调用getNum()还是setNum(),要根据实际的场景来判断,
#1. 如果是给t.num赋值 那么一定调用setNum()
#2. 如果是获取t.num的值,那么就一定调用getNum()
#
#property的作用:相当于把方法进行了封装, 开发者在对属性设置数据的时候更方便
```

```python
class Test(object):
    def __init__(self):
       self.__num = 100

    @property
    def num(self):
        print("----getter----")
        return self.__num

    @num.setter
    def num(self, newNum):
        print("----setter----")
        self.__num = newNum

t = Test()

t.num = 200 #相当于调用了 t.setNum(200)

print(t.num) #相当于调用了 t.getNum()
```

# 4.生成器
### 1. 什么是⽣成器
通过列表⽣成式，我们可以直接创建⼀个列表。但是，受到内存限制，列表容量肯定是有限的。⽽且，创建⼀个包含100万个元素的列表，不仅占⽤很⼤的存储空间，如果我们仅仅需要访问前⾯⼏个元素，那后⾯绝⼤多数元素占⽤的空间都⽩⽩浪费了。所以，如果列表元素可以按照某种算法推算出来，那我们是否可以在循环的过程中不断推算出后续的元素呢？这样就不必创建完整的list，从⽽节省⼤量的空间。在Python中，这种⼀边循环⼀边计算的机制，称为⽣成器：generator。

### 2. 创建⽣成器⽅法1
要创建⼀个⽣成器，有很多种⽅法。第⼀种⽅法很简单，只要把⼀个列表⽣成式的 [ ] 改成 ( )

### 3.创建⽣成器⽅法2 **yield**
```python
def Fib():
    print("------start----")
    a,b = 0,1
    for i in range(5):
        yield b
        a,b = b,a+b
    print("------stop----")
```
**yield 作用是把一个函数变成一个 generator，带有 yield 的函数不再是一个普通函数，Python 解释器会将其视为一个 generator，调用 fab(5) 不会执行 fab 函数，而是返回一个 iterable 对象！
在 for 循环执行时，每次循环都会执行 fab 函数内部的代码，执行到 yield b 时，fab 函数就返回一个迭代值，下次迭代时，代码从 yield b 的下一条语句继续执行，而函数的本地变量看起来和上次中断执行前是完全一样的，于是函数继续执行，直到再次遇到 yield。**

```python
def Fib():
    print("------start----")
    a,b = 0,1
    for i in range(5):
        print("----1---")
        yield b
        print("----2---")
        a,b = b,a+b
        print("----3---")
    print("------stop----")

#创建了一个生成器对象
a = Fib()

for num in a:
    print(num)
```
<img src="/picturesWork/pythonHigh/009.png">


```python
def Fib():
    print("------start----")
    a,b = 0,1
    for i in range(5):
        print("----1---")
        yield b
        print("----2---")
        a,b = b,a+b
        print("----3---")
    print("------stop----")

#创建了一个生成器对象
a = Fib()

#for num in a:
#    print(num)

ret = next(a)    #让a这个生成器对象开始执行,如果是第一次执行,那么就从creatNum的开始部分执行
                 #如果是之前已经执行过了,那么就从上一次停止的位置开始执行

ret = next(a)
ret = next(a)
ret = next(a)
ret = next(a)
ret = next(a)  #报错 越界
ret = next(a)
ret = next(a)
```
<img src="/picturesWork/pythonHigh/011.png">


```python
def Fib():
    print("------start----")
    a,b = 0,1
    for i in range(5):
        print("----1---")
        yield b
        print("----2---")
        a,b = b,a+b
        print("----3---")
    print("------stop----")

#创建了一个生成器对象
a = Fib()

ret = a.__next__()
print(ret)

#for num in a:
#    print(num)
#注意:
#next(a)
#a.__next__()
#以上两种方式是一样的
# for 循环不会报错
```

### 4.send
执⾏到yield时，gen函数作⽤暂时保存，返回i的值;temp接收下次 c.send("python")，send发送过来的值，c.next()等价c.send(None)
```python
def gen():
    i = 0
    while i<5:
        temp = yield i  #在下一次传一个值给temp ，第一次没传值 (yield i) 为None, 第二次传send('haha')，temp = 'haha'
        print(temp)     
        i+=1
```
<img src="/picturesWork/pythonHigh/010.png">




### 5.多任务(看上去同时执行)
```python
def test1():
    while True:
        print("--1--")
        yield None

def test2():
    while True:
        print("--2--")
        yield None


t1 = test1()
t2 = test2()
while True:
    t1.__next__()
    t2.__next__()
```



# 5.迭代器
### A. 可迭代对象
以直接作⽤于 for 循环的数据类型有以下⼏种：
- ⼀类是集合数据类型，如 list 、 tuple 、 dict 、 set 、 str 等；
- ⼀类是 generator ，包括⽣成器和带 yield 的generator function。这些可以直接作⽤于 for 循环的对象统称为可迭代对象： Iterable 。

### B. 判断是否可以迭代
可以使⽤ isinstance() 判断⼀个对象是否是 Iterable 对象:
```python
from collections import Iterable
isinstance([], Iterable)
#True
isinstance({}, Iterable)
#True
isinstance('abc', Iterable)
#True
isinstance((x for x in range(10)), Iterable)
#True
isinstance(100, Iterable)
#False
```
*⽣成器不但可以作⽤于 for 循环，还可以被 next() 函数不断调⽤并返回下⼀个值，直到最后抛出 StopIteration 错误表示⽆法继续返回下⼀个值了*

### C.迭代器
可以被next()函数调⽤并不断返回下⼀个值的对象称为迭代器：Iterator。  
可以使⽤ isinstance() 判断⼀个对象是否是 Iterator 对象：
```python
from collections import Iterator
isinstance((x for x in range(10)), Iterator)
#True
isinstance([], Iterator)
#False
isinstance({}, Iterator)
#False
isinstance('abc', Iterator)
#False
isinstance(100, Iterator)
#False
```
**生成器一定是迭代器，迭代器不一定是生成器**

### D.iter()函数
⽣成器都是 Iterator 对象，但 list 、 dict 、 str 虽然是 Iterable ，却不是Iterator 。  
把 list 、 dict 、 str 等 Iterable 变成 Iterator 可以使⽤ iter() 函数:
```python
from collections import Iterator
isinstance(iter([]), Iterator)
isinstance(iter('abc'), Iterator)
```

### 总结
- 凡是可作⽤于 for 循环的对象都是 Iterable 类型；
- 凡是可作⽤于 next() 函数的对象都是 Iterator 类型；
- 集合数据类型如 list 、 dict 、 str 等是 Iterable 但不是 Iterator ，不过可以通过 iter() 函数获得⼀个 Iterator 对象。

# 6.闭包
### A. 函数引⽤
```python
def test1():
    print("--- in test1 func----")
#调⽤函数
test1()
#引⽤函数
ret = test1
print(id(ret))
print(id(test1))
#通过引⽤调⽤函数
ret()
###############运行结果
#--- in test1 func----
#140212571149040
#140212571149040
#--- in test1 func----
```
<img src="/picturesWork/pythonHigh/01.png">

### B.什么是闭包
```python
def test(number):
    print("--1--")
    #在函数内部再定义⼀个函数，并且这个函数⽤到了外边函数的变量，那么将这个函数以及⽤到的⼀些变量称之为闭包
    def test_in(number2):
        print("--2--")
        print(number+number2)
    print("--3--")
    return test_in #返回函数的引用 而不是调用函数
ret = test(100)
print("-"*30)
ret(1)
ret(100)
ret(200)
```
<img src="/picturesWork/pythonHigh/02.png">

### C.闭包例子
```python
def test(a,b):
    def test_in(x):
        print(a*x+b)

    return test_in

line1 = test(1,1)
line1(0)
line2 = test(10,4)
line2(0)
line1(0)
#
#def createNum(a,b,x):
#    print(a*x+b)
#
#a=1
#b=1
#x=0
#createNum(a,b,x)
#createNum(a,b,x)

#1.闭包似优化了变量，原来需要类对象完成的⼯作，闭包也可以完成
#2.由于闭包引⽤了外部函数的局部变量，则外部函数的局部变量没有及时释放，消耗内存
```
<img src="/picturesWork/pythonHigh/03.png">

# 7.装饰器
*装饰器是程序开发中经常会⽤到的⼀个功能，⽤好了装饰器，开发效率如⻁添翼，所以这也是Python⾯试中必问的问题，但对于好多初次接触这个知识
的⼈来讲，这个功能有点绕，⾃学时直接绕过去了，然后⾯试问到了就挂了，因为装饰器是程序开发的基础知识，这个都不会，别跟⼈家说你会Python, 看了下⾯的⽂章，保证你学会装饰器。*

### A.明白：
```python
#### 第⼀波 ####
def foo():
    print("---foo---")
foo  #表示是函数
foo() #表示调用执行foo函数 

#### 第⼆波 ####
def foo():
    print('foo')
foo = lambda x: x + 1

foo() # 执⾏下⾯的lambda表达式，⽽不再是原来的foo函数，因为foo这个名字被重新指向
```
<img src="/picturesWork/pythonHigh/04.png">

### B.需求来了
```python
def w1(func):
    def inner():
        print("---正在验证权限----")
        func()
    return inner

def f1():
    print("---f1---")

def f2():
    print("---f2---")

#innerFunc = w1(f1)
#innerFunc()

f1 = w1(f1)
f1()
```
<img src="/picturesWork/pythonHigh/05.png">
<img src="/picturesWork/pythonHigh/06.png">

```python
def w1(func):
    def inner():
        print("---正在验证权限----")
        if False:
            func()
        else:
            print("没有权限")
    return inner

#f1 = w1(f1)
@w1
def f1():
    print("---f1---")

@w1
def f2():
    print("---f2---")

f1()
f2()
```

### C.多个装饰器
```python
#定义函数：完成包裹数据
def makeBold(fn):
    def wrapped():
        print("----1---")
        return "<b>" + fn() + "</b>"
    return wrapped

#定义函数：完成包裹数据
def makeItalic(fn):
    def wrapped():
        print("----2---")
        return "<i>" + fn() + "</i>"
    return wrapped

@makeBold
@makeItalic
def test3():
    print("----3---")
    return "hello world-3"

ret = test3()
print(ret)
```
<img src="/picturesWork/pythonHigh/07.png">
<img src="/picturesWork/pythonHigh/08.png">

### D.装饰器什么时候进行装饰
```python
def w1(func):
    print("---正在装饰1----")
    def inner():
        print("---正在验证权限1----")
        func()
    return inner

def w2(func):
    print("---正在装饰2----")
    def inner():
        print("---正在验证权限2----")
        func()
    return inner

#只要python解释器执行到了这个代码,那么就会自动的进行装饰,而不是等到调用的时候才装饰的
@w1
@w2
def f1():
    print("---f1---")

#在调用f1之前,已经进行装饰了
f1()
```
<img src="/picturesWork/pythonHigh/09.png">


### E.使用装饰器对无参数的函数进行装饰
```python
def func(functionName):
    print("---func---1---")
    def func_in():
        print("---func_in---1---")
        functionName()
        print("---func_in---2---")

    print("---func---2---")
    return func_in

@func
def test():
    print("----test----")


#test = func(test)

test()

```

### F.使用装饰器对有参数的函数进行装饰
```python
def func(functionName):
    print("---func---1---")
    def func_in(a, b):#如果a,b 没有定义,那么会导致16行的调用失败
        print("---func_in---1---")
        functionName(a, b)#如果没有把a,b当做实参进行传递,那么会导致调用12行的函数失败
        print("---func_in---2---")

    print("---func---2---")
    return func_in

@func
def test(a, b):
    print("----test-a=%d,b=%d---"%(a,b))


test(11,22)

```

### G.使用装饰器对有不定长参数的函数进行装饰
```python
def func(functionName):
    print("---func---1---")
    def func_in(*args, **kwargs):#采用不定长参数的方式满足所有函数需要参数以及不需要参数的情况
        print("---func_in---1---")
        functionName(*args, **kwargs)#这个地方,需要写*以及**,如果不写的话,那么args是元祖,而kwargs是字典
        print("---func_in---2---")

    print("---func---2---")
    return func_in

@func
def test(a, b, c):
    print("----test-a=%d,b=%d,c=%d---"%(a,b,c))

@func
def test2(a, b, c, d):
    print("----test-a=%d,b=%d,c=%d,d=%d---"%(a,b,c,d))

test(11,22,33)

test2(44,55,66,77)

```


### H.使用装饰器对有返回值的函数进行装饰
```python
def func(functionName):
    print("---func---1---")
    def func_in():
        print("---func_in---1---")
        ret = functionName() #保存 返回来的haha
        print("---func_in---2---")
        return ret #把haha返回岛17行处的调用

    print("---func---2---")
    return func_in

@func
def test():
    print("----test----")
    return "haha"

ret = test()
print("test return value is %s"%ret)

```

### I.使用通用的装饰器完成对函数进行装饰
```python
def func(functionName):
    def func_in(*args, **kwargs):
        print("-----记录日志-----")
        ret = functionName(*args, **kwargs)
        return ret

    return func_in

@func
def test():
    print("----test----")
    return "haha"

@func
def test2():
    print("----test2---")

@func
def test3(a):
    print("-----test3--a=%d--"%a)

ret = test()
print("test return value is %s"%ret)

a = test2()
print("test2 return value is %s"%a)


test3(11)

```

### J.有参数的装饰器
```python
def func_arg(arg):
    def func(functionName):
        def func_in():
            print("---记录日志-arg=%s--"%arg)
            if arg=="heihei":
                functionName()
                functionName()
            else:
                functionName()
        return func_in
    return func

#1. 先执行func_arg("heihei")函数,这个函数return 的结果是func这个函数的引用
#2. @func
#3. 使用@func对test进行装饰
@func_arg("heihei")
def test():
    print("--test--")

#带有参数的装饰器,能够起到在运行时,有不同的功能
@func_arg("haha")
def test2():
    print("--test2--")

test()
test2()

```





