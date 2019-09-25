---
layout: post
title: "Python List"
subtitle: 'list'
author: "Kgod"
header-style: text
tags:
  - python
---
## Python基础
[Python官网](https://www.python.org)  
[廖雪峰](https://www.liaoxuefeng.com/wiki/1016959663602400)    
[Python 详细视频](https://pan.baidu.com/s/1hOcl3GT3Ko4EttcPI95QLg)  提取码: 2esp  
[PanDownload](http://pandownload.com/)

[python1](http://c.biancheng.net/view/4427.html)
[python2](https://blog.csdn.net/github_38614120/article/details/79163534)

## if else
```python
gender = input("请输入你的性别：") #获取性别
#判断性别
if gender=="男": #input输入的全是str
    print("高富帅")
elif gender=="女":
    print("白富美")
else:
    print("你很666")
#==================================================================================================================
score_s = input("请输入你的成绩")
score =int(score_s)
if score>=90 and score<=100:
    print("本次考试等级为A")
elif score>=80 and score<90:
    print("本次考试等级为B")
elif score>=70 and score<80:
    print("本次考试等级为C")
elif score>=60 and score<70:
    print("本次考试等级为D")
elif score>=0 and score<60:
    print("本次考试等级为E")
#==================================================================================================================
import random
player = input("请输入：剪刀（0） 石头（1） 布（2）：")
player = int(player)
computer = random.randint(0,2)
if((player == 0) and (computer == 2)) or ((player == 1) and (computer == 0)) or ((player ==2) and (computer == 1)):
    print("获胜，哈哈，你太厉害了！")
elif player == computer:
    print("平局，要不要再来一局")
else:
    print("输了，不要走，洗洗手在接着来，决战到天明")
```

## while
```python
i = 0
while i<5:
    print("当前是第%d次循环"%(i+1))
    print("i=%d"%i)
    i+=1
#================================================================
i =0
sum = 0
while i<=100:
    sum = sum + i 
    i +=1
print("1到100的和是：%d"%sum) 
#================================================================
i = 0
sum = 0
while i<= 100:
    if i%2 == 0: #判断是否是偶数
        sum = sum +i
    i+=1
print("1到100的偶数和是%d"%sum) 
#================================================================
i = 1
while i<=5:
    j = 1
    while j<=i:
        print("* ",end='')
        j+=1

    print("\n")
    i+=1
#================================================================
i = 1
while i<=9:
    j=1
    while j<=i:
        print("%d*%d=%d "%(j,i,i*j),end='')
        j+=1
    print("\n")
    i+=1    
```

## for 
```python
name = 'dongGe'
for x in name:
    print(x)
else:
    print("没有数据")
#================================================================
for x in name:
    print("-----")
    if x == 'g':
        break
    print(x)
#================================================================
for x in name:
    print("-----")
    if x == 'g':
        continue
    print(x)
#================================================================
i = 0
while i<10:
    i+=1
    print("-----")
    if i == 5:
        break #break的作用 ： 用来结束整个循环 
    print(i)
#================================================================
i = 0 
while i<10:
    i+=1
    print("-----")
    if i==5:
        continue #continue的作用  用来结束本次循环，紧接着执行下一次的循环
    print(i)
```

## List
**列表是包含若干元素的有序连续内存空间**  
Python常用的序列结构：列表、元组、字典、字符串、集合等  

Python内置对象：

 对象类型  |   类型名称   | 示例
-----   |  ---- | ------
  数字   |  int /float /complex | 1234/3.14/1.3e5/3+4j
  字符串 |  str | 'hello'
  字节串 | bytes |  b'hello world'
  列表 |  list | [1,2,3]
  字典 | dict | {1:'food',2:'taste'}
  元组 | tuple | (2,-5,6) 
  集合 | set/frozenset  | {'a','b','c'}
  布尔型 |  bool | True /False
  空类型 | NoneType | None
  异常 | Exception | 
  文件 |      | 
  其他迭代对象 |   |
  编程单元 |   |

1 创建一个列表 

```python
nameList = [] #创建空列表

nameList = ['xiaoWang','xiaoZhang','xiaoHu']

testList = [1,'a'] #比c语言强大
```

2 列表元素访问  
使用整数作为下标来访问其中的元素，**下标为0的元素表示第1个元素，下标为-1的元素表示最后一个元素，以此类推**

```python
nameList = ['xiaoWang','xiaoZhang','xiaoHu']

#第一种遍历：
for name in nameList: #for循环遍历列表
    print(name)

#第二种遍历：
length = len(nameList) #列表长度
i = 0 #Python中第一个字符是从0开始
while i<length:
    print(nameList[i])
    i+=1

#访问某个元素
print(nameList[0])
print(nameList[-1])
```

3 列表常用方法

```python
A = ['xiaoWang','xiaoZhang','xiaoHua']
print('===操作之前，列表A的数据===')
for tempName in A:
    print(tempName)
```
```python
#1.添加元素 ：三种，都属于原地操作，不影响列表对象在内存中的起始地址

#list.append() 在末尾添加
temp = input('请输入要添加的姓名：')
A.append(temp)
print('===操作之后，列表A的数据===')
for tempName in A:
    print(tempName)

#extend 可以将另一个集合中的元素逐一添加到列表中
a = [1,2]
b = [3,4]
a.extend(b) #a=[1,2,3,4]

#insert(index,object) 在指定位置index前插入元素object
a = [0,1,2]
a.insert(1,3)#在下标为1的位置前插入元素 3
print(a)
```
```python
#2.删除元素  也是原地操作

#del 根据下标进行删除
del moveName[2] # 删除下标为2 的元素的值

#pop() 删除最后一个元素
moveName.pop # 删除末尾

#remove() 根据元素的值进行删除
moveName.remove('指环王') # 删除 指环王

#clear()
x = [1,2,3]
x.clear() # 清空列表所有元素
```
```python
#3.修改元素 原地操作

A = ['1','g','f','9']
A[1] = 'hahaha'
print(A)
```
```python
#4.查找元素

#in 或者 not in
if findName in namelist:  
    print("找到啦哈哈哈")
else:
    print("没找到呜呜呜")
```
```python
#5.其他常见列表操作函数：

#index()
m.index(A) #输出元素A在列表m里面的索引位置号
m.index(A,a,b) #对于列表m里面包含多个元素A时，输出在列表m索引号a-b之间的特定索引号 
a = ['f','a','b','c','a','b']
a.index('a',2,5) #左闭右开 在第2到4个位置找到a 发现在第4个位置 返回4
#----------------------------------------------------------------------------------------------------------------------
#count() 返回列表中指定元素出现次数
a.count('a') 

#len()  返回列表长度
len(a)

#sort() reverse()
a = [1,4,2,3]
a.reverse() #将list逆置
print(a)
a.sort() #将list按特定顺序默认为从小到大， 参数reverse=Ture 可改为倒序 即由大到小 a.sort(reverse=True)
print(a)
```
```python
#6. copy() 浅复制
#深复制与浅复制
#浅复制是指生成一个新的列表，并且把源列表中所有元素的引用都复制到新列表中，当原列表只包含 整数、实数、复数、元组、字符串这样的不可变类型的数据，没问题。但是如果是包含列表之类的可变数据类型，浅复制只是把列表的引用复制到新列表中，修改任何一个都会影响另一个。
x = [1,2[3,4]]
y = x.copy()
print(y) #[1,2,[3,4]]
y[2].append(5)  #y=[1, 2, [3, 4, 5]] 
x[0] = 6 #x=[6,2,[3,4,5]]
y.append(6) #y=[1, 2, [3, 4, 5],6]

#deepcopy() 深复制：指对原列表中的元素进行递归，把所有的值都复制到新列表中，对嵌套的子列表不再是复制引用，这样两个列表相互独立，修改任何一个都互不影响。
import copy
x = [1,2,[3,4]]
y = copy.deepcopy(x)
x[2].append(5)
y.append(6) #y=[1,2,[3,4],6] x=[1,2,[3,4,5]]

#还有一种情况 对x做任何修改y都会受到影响
x = [1,2,[3,4]]
y = x
x[2].append(5)
x.append(6)
x[0] = 7 #x=[7,2,[3,4,5],6] y=[7,2,[3,4,5],6]



```

4  列表对象支持的运算符
加法运算符’+‘也可以实现列表增加元素的目的，但是这个运算符不属于原地操作，而是返回新列表，并且涉及大量元素的复制，效率低，使用’+=‘属于原地操作，与append()方法一样高效。
```python
x = [1,2,3]
print(id(x)) #原始id

x = x + [4] #连接两个列表 
print(x)
print(id(x)) #内存地址发生变化

x += [5] #为列表追加元素
print(x)
print(id(x)) #与之前的原始id一样
#--------------------------------------------------------------------------------------------
x = [1,2,3,4]
x = x*2 #元素重复，返回新列表 x=[1,2,3,4,1,2,3,4]
x *= 2
#--------------------------------------------------------------------------------------------
#比较 >,< 主要进行数据型列表的元素比较
#and 逻辑运算符，可以进行列表之间的逻辑判断

```

5  内置函数对列表的操作

函数 |  
--- | ---  
max() |
min() |
sum() |
len() |
zip() | 多个列表中元素重新组合为元组并返回包含这些元组的zip对象
map() | 把函数映射到列表上的每个元素

6  列表模拟向量运算
```python
x = [1,2,3] + [4,5,6]
print(x) # x=[1,2,3,4,5,6]
```

7  列表推导式
```python
aList = [x*x for x in range(10)]
print(aList) # [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

vec = [[1,2,3],[4,5,6],[7,8,9]]
[num for elem in vec for num in elem] #[1, 2, 3, 4, 5, 6, 7, 8, 9]

matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
[[row[i] for row in matrix] for i in range(4)] #[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
```

8  切片的强大功能 [start:end:step]
```python
#1. 使用切片获取列表部分元素
aList = [3,4,5,6,7,9,11,13,15,17]
aList[::] #start默认为0 step默认为1 可以不写
aList[::-1] #反向切片 [17, 15, 13, 11, 9, 7, 6, 5, 4, 3]
aList[::2] #[3,5,7,11,15]
aList[1::2] #[4,6,9,13,17]
aList[3:6] #[6,7,9]
aList[3:-10:-1] # 位置3在位置-10的右侧 -1表示反向切片 [6,5,4]
aList[3:-5] #位置3在位置-5的左侧，正向切片 [6,7]

#2. 使用切片为列表增加元素
aList = [3,5,7]
aList[len(aList):] = [9] #尾部增加元素9
aList[:0] = [1,2] #头部插入多个元素
aList[3:3] = [4] #中间插入元素

#3. 使用切片替换和修改列表中的元素
aList = [3,5,7,9]
aList[:3] = [1,2,3] #替换列表元素，等号两边的列表长度相等 [1,2,3,9]
aList[3:] = [4,5,6] #切片连续，等号两边的列表长度可以不相等 [1,2,3,4,5,6]
aList[::2] = [0] * 3 #各一个修改一个 [0,2,0,4,0,6]

#4. 使用切片删除列表中的元素
aList = [3,5,7,9]
aList[:3] = [] #删除列表中前3个元素 [9]

aList = [3,5,7,9,11]
del aList[:3] #[9,11]

aList = [3,5,7,9,11]
del aList[::2] #[5,9]

#5. 切片得到的是浅复制
aList = [3,5,7]
bList = aList[::]
aList == bList #True 两列表值相等 
aList is bList #False 浅复制 不是同一个对象
id(aList) == id(bList) #False 两个列表对象的地址不相等

bList[1] = 8
print(bList) #[3,8,7]
print(aList) #[3,5,7] 修改bList 不影响aList
```

9  列表嵌套
list元素也可以是另一个list，比如：
```python
s = ['python', 'java', ['asp', 'php'], 'scheme']
len(s)
#还可以是元组，字典等
```

10 [Python编程核心知识体系](https://woaielf.github.io/2017/06/13/python3-all/)  
<img src="/picturesWork/python-list/01.png">

