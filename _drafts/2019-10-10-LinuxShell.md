---
layout: post
title: "Linux Shell"
subtitle: 'linux'
author: "Kgod"
header-style: text
tags:
  - linux
---
# 第1章
## 1.1 终端打印
echo  
printf

## 1.2 玩转变量和环境变量
### 1.2.1 做好准备
查看运行环境变量：
```
cat /proc/$PID/environ
PID获取： pgrep gedit
cat /proc/12501/environ  | tr '\0' '\n'
```
### 1.2.2 怎么做
```
var=value  
var 是变量的名称，value是要分配的值。如果value不包含任何空格字符（如空格），则不必将其括在引号中，
否则必须将其括在单引号或双引号中。请注意，var = value和var=value 是不同的。
后者是赋值运算，而前者是相等运算。
```

通过使用 <label style="color:red">$</label> + 变量名称的前缀来打印变量的内容
```
var='value'
echo $var
OR echo ${var} 
```

```
#!/bin/bash
fruit=apple
count=5
echo "We have $count  ${fruit}(s)"
```

### 1.2.3 补充内容
1. 获取字符串长度：`length=${#var}` ,`echo ${#var}`
2. 识别当前shell版本：`echo $0 / echo $SHELL`
3. 检查是否为超级用户：root用户的UID是0
4. 修改BAsh提示字符串

## 1.3 通过shell进行数学运算
```
#!/bin/bash
no1=4;
no2=5;
let result=no1+no2
echo $result
```
































