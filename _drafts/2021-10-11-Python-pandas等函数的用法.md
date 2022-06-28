---
layout: post
title: "mysql练习"
subtitle: 'mysql'
author: "Kgod"
header-style: mysql
tags:
  - SQL
---

# mysql

## 176.第二高薪水
法一：先用子查询找到最高薪水，再去掉最高薪水，选择max(salary)
```sql
SELECT MAX(SALARY)
FROM EMPLOYEE E
WHERE SALARY !=
        (SELECT MAX(SALARY)
         FROM EMPLOYEE E2)
```


法二：
- 找出salary并降序(desc)排列，注意去除重复值
- 取第一个，因为limit是从0开始
- 当结果为null，返回 select(null)

```sql
SELECT IFNULL(
                  (SELECT DISTINCT SALARY
                   FROM EMPLOYEE_TEST ET
                   ORDER BY SALARY DESC LIMIT 1,1) -- 只选择一个
,NULL) AS SECONDSALARY 

-- OR

SELECT
    (SELECT DISTINCT SALARY
     FROM EMPLOYEE_TEST ET
     ORDER BY SALARY DESC LIMIT 1,
                                1 -- 只选择一个
) AS SECONDSALARY
```

## 177. 第N高的薪水

法一：单表查询

```sql


```




<!-- ## groupby
1.test
```python
# 按A列分组，获取其他列的均值
df.groupby('A').mean()
# 按多列分组
df.groupby(['A','B']).mean()
# dakdoks
# sds
# dsds
```
2 -->










