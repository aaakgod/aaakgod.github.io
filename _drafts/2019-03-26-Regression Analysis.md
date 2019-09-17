``
layout: post
post title: "regression analysis" 
subtitle: 'regression analysis' 
author: "Kgod" 
header-style: text 
tags: 
  - regression analysis 
---
目录
<!-- levels="2,3" autolink="true" style="orderd -->
<!-- MarkdownTOC "-->

- 第二章 随机向量
  - 2.1 均值向量与协方差阵
  - 2.2 随机向量的二次型
  - 2.3 正态随机变量的性质
- 第三章 回归参数的最小二乘估计
  - 3.1 预备知识
  - 3.2 最小二乘估计
  - 3.3 线性模型的中心化和标准化
  - 3.4 最下二乘估计的性质
    - 3.4.1 一般线性回归模型

<!-- /MarkdownTOC -->

# 第二章 随机向量
### 2.1 均值向量与协方差阵
**性质:**
1. $E(AX+b)=AE(X)+E(b)$.
2. $E(AXB)=AE(X)B$.
3. $trCov(X)=\sum_{i=1}^{n}Var(X_i)$.
4. $R.V$向量$X$的协差阵是半正定的对称的.
5. 定理2.1.3 设$A$为$m \times n$阵,$X$为$n \times 1$随机向量,$Y=AX$,则$Cov(Y)=ACov(X)A'$.
6. 设$X,Y$分别是$n \times 1$和$m \times 1$阶$R.V$向量,$A$和$B$分别为$p \times n$和$q \times m$非随机阵.则$Cov(AX,BY)=ACov(X,Y)B'$.
7. $Cov(X,Y)=[Cov(Y,X)]'$.

### 2.2 随机向量的二次型
1. 分块矩阵的对角化
2. 分块矩阵求逆
3. 分块矩阵的行列式
4. 迹的可交换性:$$trAB=trBA$$
5. 二次型的期望:  
定理2.2.1: $E(X)=\mu,Cov(X)=\Sigma \implies E(X'AX)=\mu' A \mu +tr(A \Sigma)$.

### 2.3 正态随机变量的性质
1. $X\sim N(\mu,\Sigma) \implies EX=\mu,Cov(X)=\Sigma$
2. 变换性质: 
    * 定理2.3.2  前提:$A$是非随机矩阵且可逆,$b$是向量,$X\sim N(\mu,\Sigma) \implies Y=AX+b \sim N(A \mu +b,A\Sigma A')$
    * 定理2.3.4  前提:$A$是$m \times n$非随机阵,秩$(A)=m < n$,$X\sim N_n(\mu,\Sigma) \implies Y=AX \sim N_m(A \mu,A\Sigma A')$
3. 再生性:
    * 定理2.3.1:  
    $$(a)X=\begin{pmatrix} X_1 \\ X_2\end{pmatrix} \sim N_n \left(\begin{pmatrix} \mu_1 \\ \mu_2\end{pmatrix},\begin{pmatrix} \Sigma_{11}&0 \\0&\Sigma_{22} \end{pmatrix}\right) \implies X_i \sim N(\mu, \Sigma_{ii}),i=1,2$$.且$X_1$与$X_2$相互独立.
4. 其他性质:
    - 分量相关,方差不等的多元正态向量,**存在线性变换**$\implies$多元标准正态向量
    - 分量独立,等方差的正太向量,**正交变换**$\implies$分量独立,等方差正态向量
    - 正态向量$X_1$与$X_2$独立$\iff X_1$与$X_2$不相关
    - $X正态 \implies 各分量正态;反之不成立$.
    



# 第三章 回归参数的最小二乘估计
### 3.1 预备知识
1. 定义: 
    * 设$\xi$是关于$X=(x_1,\cdots,x_n)'$的函数,定义$\dfrac{\partial\xi}{\partial X}=\left(\dfrac{\partial\xi}{\partial x_1},\cdots,\dfrac{\partial\xi}{\partial x_n}\right)'$
    * 设$X=(x_1,\cdots,x_n)'$个分量是关于$\xi$的函数,定义$\dfrac{\partial X}{\partial\xi}=\left(\dfrac{\partial x_1}{\partial\xi},\cdots,\dfrac{\partial x_n}{\partial\xi}\right)'$ 
    * 设$\xi$是一函数,$X=(x_ij)$是一矩阵,定义$\dfrac{\partial\xi}{\partial X}=\left(\dfrac{\partial\xi}{\partial x_ij}\right)$.
2. 性质:
    * 设$X$是$n \times 1$维向量,$a$是$n \times 1$常向量,则$\dfrac{\partial (a'X)}{\partial X}=\dfrac{\partial (X'a)}{\partial X}=a$
    * 设$X$是$n \times 1$维向量,$A$是$n \times n$常数矩阵(不要求$A$对称),则$\dfrac{\partial(X'AX)}{\partial X}=(A+A')X$
    * 特别地,当$A$对称时,$$\dfrac{\partial(X'AX)}{\partial X}=2AX$$.

### 3.2 最小二乘估计
**多元线性回归模型:**$Y=X\beta+e$,假设$E(e)=0,Cov(e)=\sigma^2 I_n$.  
**结论:**$\hat{\beta}=(X'X)^{-1}X'Y$.  
**经验回归方程:**$\hat{y}= \hat{\beta_0}+\hat{\beta_1} x_1+\cdots+\hat{\beta_{p-1}} x_{p-1}$.  
**推导:**$||Y-X \beta||^2=(Y-X\beta)'(Y-X\beta)=Y'Y-2Y'X\beta+\beta'X'X\beta$,对$\beta$求偏导,令为0.  

### 3.3 线性模型的中心化和标准化
**矩阵形式:**$Y=\alpha 1_n + X_c \beta +e=(1_n:X_c)$
$$\begin{pmatrix}
  \alpha \\ 
  \beta 
  \end{pmatrix}$$ +$e$  
  其最小二乘估计是 $$\left\{\begin{matrix}
\hat{\alpha} = y & \\ 
\hat{\beta} = (X_{c}^{'}X_c)^{-1} X_{c}^{'} Y & 
\end{matrix}\right.$$

### 3.4 最下二乘估计的性质
#### 3.4.1 一般线性回归模型
**Th3.2.1** 最小二乘估计$\hat{\beta} = (X'X)^{-1}X'Y$的性质:  
1. $E(\hat{\beta}) = \beta$  
2. $Cov(\hat{\beta}) = \sigma^2 (X'X)^{-1}$  
分析:$Y=X\beta+e$中 $Y$ 与 $e$ 是随机的,$X\beta$是非随机的,所以  
$E(Y)=X\beta,CovY=Cov(e)=\sigma^2 I$  

**定义:** 称$C'\hat{\beta}$为$C'\beta$的最小二乘估计,$C'\hat{\beta} = C'(X'X)^{-1}X'Y$  

**推论3.2.1**  
1. $E(C'\hat{\beta})=C'\beta$
2. $Cov(C'\hat{\beta}) = \sigma^2C'(X'X)^{-1}C = Var(C'\hat{\beta})$  
proof 2:$Cov(C'\hat{\beta}) = C'Cov(\hat{\beta})C = C'\sigma^2(X'X)^{-1}C$

























