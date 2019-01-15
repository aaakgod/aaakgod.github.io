---
layout: post
title: "贷款预测数据"
subtitle: 'Using Python For Data Prediction '
author: "Kgod"
header-style: text
tags:
  - python 
---

# 一.提出问题111111122222333
## 1.1 问题背景
在所有行业中，保险领域是分析和数据科学方法使用最广的行业之一。这个数据集为你提供了保险公司的数据工作体验——那里面临什么挑战，使用什么策略，哪些变量影响结果等。这是一个分类问题。数据有615行13列。

任务：预测贷款是否会得到批准。

数据：https://datahack.analyticsvidhya.com/contest/practice-problem-loan-prediction-iii/

教程：https://www.analyticsvidhya.com/blog/2016/01/complete-tutorial-learn-data-science-python-scratch-2/

## 1.2 问题陈述


### 关于公司

Dream Housing Finance公司处理所有房屋贷款。他们遍布所有城市，半城市和农村地区。在该公司验证客户是否有资格获得贷款后，客户首先申请住房贷款。

### 问题

公司希望根据填写在线申请表时提供的客户详细信息自动化贷款资格流程（实时）。这些详细信息包括性别，婚姻状况，教育，家属人数，收入，贷款金额，信用记录等。为了使这一过程自动化，他们在识别客户细分方面遇到了问题，这些细分符合贷款金额，因此他们可以专门针对这些客户。他们在这里提供了部分数据集。



## 1.3 数据
### 变量

### 描述

Loan_ID

独特的贷款ID

性别

男/女

已婚

申请人结婚（是/否）

家属

家属人数

教育

申请人教育（研究生/本科生）

自雇人士

自雇（Y / N）

ApplicantIncome

申请人收入

CoapplicantIncome

共同收入

贷款额度

贷款金额为数千

Loan_Amount_Term

几个月的贷款期限

Credit_History

信用记录符合指南
信用记录符合指南

Property_Area

城市/半城市/乡村

Loan_Status

贷款批准（是/否）

## 注意： 

### 评估指标是准确性，即您正确预测的贷款审批百分比。
您需要以“sample_submission.csv”格式上传解决方案
# 二. 解决问题
## 2.1 导入库和数据集:numpy  matplotlib pandas 

## 2.2 快速数据探索:



1.LoanAmount 有 614-592 个缺失值

2. Loan_Amount_Term 有614-600 个缺失值

3. Credit_History 有614-564 个缺失值

4. 大约84.21%的申请人拥有Credit_History (有信用记录为1，反之0)

5. 

1.LoanAmount 有 614-592 个缺失值

2. Loan_Amount_Term 有614-600 个缺失值

3. Credit_History 有614-564 个缺失值

4. 大约84.21%的申请人拥有Credit_History (有信用记录为1，反之0)

5. 


