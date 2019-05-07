---
layout: post
title: "The art of war-python-II"
subtitle: 'The art of war-python-II'
author: "Kgod"
header-style: text
tags:
  - Python
--- 

<!-- MarkdownTOC -->

- 五、排序与搜索
    - 5-01 排序算法的稳定性
    - 5-02 冒泡排序及实现
    - 5-03 选择排序算法及实现
    - 5-04 插入排序
    - 5-05 希尔排序
    - 5-06 快速排序
    - 5-07 归并排序
    - 5-08 二分查找
- 六、树和树的算法
    - 6-01 树的概念
    - 6-02 二叉树的概念
    - 6-03 二叉树的广度优先遍历
    - 6-04 二叉树的实现
    - 6-05 二叉树的先序、中序、后序遍历
    - 6-06 二叉树由遍历确定一棵树

<!-- /MarkdownTOC -->


## 五、排序与搜索
排序算法（Sorting algorithm）是一种能将一串数据依照特定顺序进行排列的一种算法。

### 5-01 排序算法的稳定性
**稳定性**：稳定排序算法会让原本有相等键值的纪录维持相对次序。也就是如果一个排序算法是稳定的，当有两个相等键值的纪录R和S，且在原本的列表中R出现在S之前，在排序过的列表中R也将会是在S之前。简单来说,如下:
<br>(4, 1)  (3, 1)  (3, 7)（5, 6）
<br>排序后:
<br>(3, 1)  (3, 7)  (4, 1)  (5, 6)  （维持次序）
<br>(3, 7)  (3, 1)  (4, 1)  (5, 6)  （次序被改变）

### 5-02 冒泡排序及实现
- **冒泡排序（Bubble Sort）**是一种简单的排序算法。它重复地遍历要排序的数列，一次比较两个元素，如果他们的顺序错误就把他们交换过来。遍历数列的工作是重复地进行直到没有再需要交换，也就是说该数列已经排序完成。这个算法的名字由来是因为越小的元素会经由交换慢慢“浮”到数列的顶端。
- 冒泡排序算法的运作如下：
    - 比较相邻的元素。如果第一个比第二个大（升序），就交换他们两个。
    - 对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对。这步做完后，最后的元素会是最大的数。
    - 针对所有的元素重复以上的步骤，除了最后一个。
    - 持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较。
- 冒泡排序的分析
<br>交换过程图示(第一次)：
<img src="/picturesWork/the_art_of_war_python/19.png">
<br>那么我们需要进行n-1次冒泡过程，每次对应的比较次数如下图所示：
<img src="/picturesWork/the_art_of_war_python/20.png">

- 实现:

```python
def bubble_sort(alist):
    """冒泡排序"""
    n = len(alist)
    for j in range(n-1):
        #控制循环次数
        
        count = 0 #优化

        for i in range(0,n-1-j):
            #班长从头走到尾
            if alist[i] > alist[i+1]:
                alist[i],alist[i+1] = alist[i+1],alist[i]
                count += 1
        if count == 0:
            #为0说明顺序对的,直接退出
            return

# i 0 ~ n-2   range(0, n-1) j=0
# i 0 ~ n-3   range(0, n-1-1) j=1
# i 0 ~ n-4   range(0, n-1-2) j=2
# j=n   i   range(0,n-1-j)
if __name__ == "__main__":
    li = [54, 26, 93, 17, 77, 31, 44, 55, 20]
    print(li)
    bubble_sort(li)
    print(li)
```

- 时间复杂度:
    - 最优时间复杂度：O(n) （表示遍历一次发现没有任何可以交换的元素，排序结束。）
    - 最坏时间复杂度：O($n^2$)
    - 稳定性：稳定
- 演示:
<img src="/picturesWork/the_art_of_war_python/01.gif">

### 5-03 选择排序算法及实现
- **选择排序（Selection sort）**是一种简单直观的排序算法。它的工作原理如下:**首先在未排序序列中找到最小（大）元素，存放到排序序列的起始位置，然后，再从剩余未排序元素中继续寻找最小（大）元素，然后放到已排序序列的末尾。**以此类推，直到所有元素均排序完毕。

- 选择排序的主要优点与数据移动有关。如果某个元素位于正确的最终位置上，则它不会被移动。选择排序每次交换一对元素，它们当中至少有一个将被移到其最终位置上，因此对n个元素的表进行排序总共进行至多n-1次交换。在所有的完全依靠交换去移动元素的排序方法中，选择排序属于非常好的一种。

-选择排序分析
<img src="/picturesWork/the_art_of_war_python/21.png">
<img src="/picturesWork/the_art_of_war_python/02.gif">
红色表示当前最小值，黄色表示已排序序列，蓝色表示当前位置。

- 实现:

```python
def select_sort(alist):
    """选择排序"""
    n = len(alist)
    for j in range(0,n-1):
        #记录最小值的索引
        min_index = j
        for i in range(j+1,n):
            #i 比min_index还小
            if alist[i] < alist[min_index]:
                #记录最小位置
                min_index = i
        #交换
        alist[j],alist[min_index] = alist[min_index],alist[j]


if __name__ == "__main__":
    li = [9 , 16, 17, 15, 11, 26 ]

    print(li)
    select_sort(li)
    print(li)
```

- 时间复杂度:
    - 最优时间复杂度：O($n^2$)
    - 最坏时间复杂度：O($n^2$)
    - 稳定性：不稳定（考虑升序每次选择最大的情况）
- 演示:
<img src="/picturesWork/the_art_of_war_python/03.gif">

### 5-04 插入排序
- **插入排序（Insertion Sort）**是一种简单直观的排序算法。它的工作原理是通过构建有序序列，对于未排序数据，在已排序序列中从后向前扫描，找到相应位置并插入。插入排序在实现上，在从后向前扫描过程中，需要反复把已排序元素逐步向后挪位，为最新元素提供插入空间。
- 插入排序分析
<img src="/picturesWork/the_art_of_war_python/22.png">
<img src="/picturesWork/the_art_of_war_python/04.gif">
- 实现:

```python
def insert_sort(alist):
    """插入排序"""
    # 从右边的无序序列中取出多少个元素执行这样的过程
    n = len(alist)
    for j in range(1,n):
        # j = [1,2,3,...,n-1]
        # i = [1,2,3,...,n-1] 代表内层循环起始值
        i = j
        # 执行从右边的无序序列中取出第一个元素i 然后插入到正确位置中
        while i > 0:
            if alist[i] < alist[i-1]:
                alist[i],alist[i-1] = alist[i-1],alist[i]
                i -= 1
            # 优化
            else:
                break
        # i=j j-1 j-2 ... 1   range(j,0,-1)

if __name__ == "__main__":
    li = [9 , 16, 17, 15, 11,     26    ]

    print(li)
    insert_sort(li)
    print(li)
```

- 时间复杂度:
    - 最优时间复杂度：O($n$)
    - 最坏时间复杂度：O($n^2$)
    - 稳定性：不稳定（考虑升序每次选择最大的情况）
- 演示:
<img src="/picturesWork/the_art_of_war_python/05.gif">

### 5-05 希尔排序


### 5-06 快速排序

### 5-07 归并排序

### 5-08 二分查找


## 六、树和树的算法
### 6-01 树的概念

### 6-02 二叉树的概念

### 6-03 二叉树的广度优先遍历

### 6-04 二叉树的实现

### 6-05 二叉树的先序、中序、后序遍历

### 6-06 二叉树由遍历确定一棵树
