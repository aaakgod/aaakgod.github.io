--- 
layout: post
title: "Time Series " 
subtitle: ' Time Series ' 
author: "Kgod" 
header-style: text 
tags: 
  - Time Series 
---
# 第1章 时间序列的预处理
### 1.1 平稳时间序列的定义
1. **严平稳(strictly stationary):** 只有当序列所有的统计性质都不会随着时间的推移而发生变化,  
**定义1.1** 设${X_t}$为一时间序列,对任意正整数$m$,任取$t_1,t_2,\cdots,t_m \in T,$对任意整数$\tau$,有
$$F_{t_1,t_2,\cdots,t_m}(x_1,x_2,\cdots,x_m)=F_{t_{1+\tau},t_{2+\tau},\cdots,t_{m+\tau}}(x_1,x_2,\cdots,x_m)$$  
则称时间序列${X_t}$为严平稳时间序列.

2. **宽平稳(weak stationary):**  
**定义1.2** 如果${X_t}$满足如下三个条件:  
- 任取$t \in T$,有$EX_{t}^{2} < \infty$;
- 任取$t \in T$,有$EX_t=\mu,\mu$为常数;
- 任取$t,s,k \in T$,且$k+s-t \in T$,有$\gamma(t,s)=\gamma(k,k+s-t)$  
则称${X_t}$为宽平稳时间序列,宽平稳也称为弱平稳或二阶平稳.  
*特例:不能互推 柯西分布 它不存在均值和方差*

3. 平稳时间序列的统计性质
    - 常数均值:$EX_t=\mu,\forall t\in T$
    - 自协方差函数和自相关系数只依赖于时间的平移长度而与时间的起止点无关
$$\gamma(t,s)=\gamma(k,k+s-t),\forall t,s,k \in T$$

### 1.2 纯随机序列检验
1. **定义2.5** 如果时间序列${X_t}$满足如下性质:
    - 任取$t\in T$,有$EX_t=\mu$;
    - 任取$t,s\in T$,有$$\gamma(t,s)= \begin{cases} \sigma^2, & \text {t=s} \\ 0, & \text{$t\neq s$} \end{cases}$$  
称序列${X_t}$为纯随机序列,也称为白噪声(white noise)序列,简记为$X_t \sim WN(\mu,\sigma^2)$.

2. **白噪声序列的性质** 
    - 纯随机性  
    $$\gamma(k)=0,\forall k \neq 0$$
    - 方差齐性    
    $$DX_t=\gamma(0)=\sigma^2$$.

# 第2章 平稳时间序列模型及其性质
## 2.1 差分方程和滞后算子
### 2.1.1 差分运算与滞后算子
**1. p阶差分运算:** 对于一个观察值序列{$x_t$}来讲,相邻两时刻序列值之差为**1阶差分(first-order difference)**,**下面引入1阶向后差分**,记为$\nabla x_t$,即
$$\nabla x_t = x_t-x_{t-1}$$.
<br/>**2阶向后差分:**,记为$$\nabla ^2x_t = \nabla x_t-\nabla x_{t-1}$$.
<br/>**p阶向后差分:**,记为$$\nabla ^p x_t = \nabla ^{p-1} x_t - \nabla ^{p-1}x_{t-1}$$.

**2. m步差分运算:**一般地,称观察值序列${x_t}$相距$m$个时刻的值之差为**$m$步差分**,记作:$\nabla_m x_t$,即<center>$\nabla_m x_t=x_t-x_{t-m}$</center> 

**3. 滞后算子:**为了简化后面平滑模型的表达式并便于求解,我们引入滞后算子的概念,如果算子$B$满足<center>$Bx_t = x_{t-1}$</center>
那么称$B$为关于时间$t$的1步**滞后算子(lag operator)**,滞后算子有如下性质:  
1. $B^0 x_t = x^t$
2. $B^k x_t = x_{t-k},k=1,2,\cdots$
3. 若${x_t}$和${y_t}$为任意两个序列,且$c_1$和$c_2$为任意常数,则有<center>$B(c_1 x_t \pm c_2 y_t) = c_1 x_{t-1} \pm c_2 y_{t-1} = c_1 B x_t \pm c_2 B y_t$</center>
4. $(1-B)^n x_t = \sum_{i=0}^n (-1)^i \tbinom{n}{i} B^i x_t,$其中$\tbinom{n}{i}=\dfrac{n!}{i!(n-i)!}$.  

**4. 滞后算子与差分运算的关系:**  
(1). $\nabla^n x_t=(1-B)^n x_t=\sum\limits_{i=0}^{n}(-1)^i \tbinom{n}{i} B^i x_t=\sum\limits_{i=0}^{n}(-1)^i \tbinom{n}{i} x_{t-i}$;  
(2). $\nabla_n x_t=(1-B^n)x_t$.

### 2.1.2 线性差分方程
**1. 线性差分方程的概念:** 称$x_t+a_1 x_{t-1}+a_2 x_{t-2}+\cdots a_n x_{t-n}=f(t)$为序列${x_t,t=0,\pm1,\pm2,\cdots}$的**n阶线性差分方程(nth-order linear difference equation)**,其中$n \geq 1;a_1,a_2,\cdots,a_n$为实数,且$a_n \not= 0$;$f(t)$为$t$的已知函数.式中$c_1,c_2,\cdots,c_n$为任意$n$个实常数.

**2. 齐次线性差分方程解的结构:** 齐次线性差分方程解的结构依赖于它的特征方程和特征根的取值情况.n阶齐次线性差分方程的特征方程为
<p>$$\lambda^n+a_1\lambda^{n-1}+a_2\lambda^{n-2}+\cdots a_n=0$$</p>
由于$a_n\not=0$,所以上述方程最多有$n$个非零根,不妨记作
$$\lambda_1,\lambda_2,\cdots,\lambda_n$$.根据特征根情况不同,其解的结构如下:
1. 当$\lambda_1,\lambda_2,\cdots,\lambda_n$为特征方程的互不相等的$n$个实根时,齐次线性差分方程的通解为$x_t=c_1 \lambda_{1}^{t}+c_2 \lambda_{2}^{t}+\cdots+c_n \lambda_{n}^{t}$,式中$c_1,c_2,\cdots,c_n$为任意$n$个实常数.

2. 当$\lambda_1,\lambda_2,\cdots,\lambda_n$中有相同实根时,不妨假设$\lambda_1=\lambda_2=\cdots=\lambda_m$为$m$个相等实根,而$\lambda_{m+1},\lambda_{m+2},\cdots,\lambda_{n}$为互不相等的实根,则齐次线性差分方程的通解为$x_t=(c_1+c_2t+\cdots+c_mt^{m-1})\lambda_{1}^{t}+c_{m+1}\lambda_{m+1}^{t}+\cdots+c_n\lambda_{n}^{t}$,式中$c_1,c_2,\cdots,c_n$为任意$n$个实常数.

3. 当$\lambda_1,\lambda_2,\cdots,\lambda_n$中有复根时,复根必然成对共轭出现,不妨假设$\lambda_1=a+ib=\gamma e^{i\omega},\lambda_2=a-ib=\gamma e^{-i\omega}$为一对共轭复根,其中$\gamma=\sqrt{a^2+b^2},\omega=arccos\dfrac{a}{\gamma}$,而$\lambda_3,\lambda_4,\cdots,\lambda_n$为互不相同的实根,这时齐次线性差分方程的通解为$$x_t=\gamma^t (c_1 e^{it\omega}+c_2 e^{-it\omega})+c_3 \lambda_{3}^{t}+\cdots+c_n \lambda_{n}^{t}$$,式中$c_1,c_2,\cdots,c_n$为任意$n$个实常数.

**3. 非齐次线性差分方程的解:** $$x_t=x_t^{'}+x_{t}^{''}$$. 

# 2.2 自回归模型($AR(p)$)的概念和性质
### 2.2.1 自回归模型的定义
1. $p$阶自回归模型(lag-p autoregressive mdoel)  
设$\{x_t,t \in T\}$为一个序列,满足如下结构:  
$$x_t=\phi_0+\phi_1 x_{t-1}+\phi_2 x_{t-2}+\cdots+\phi_p x_{t-p}+\varepsilon_t,\phi_0,\phi_1,\cdots,\phi_p为p+1个固定常数$$  
则称之为**$p$阶自回归模型(lag-p autoregressive mdoel)**,简记为$AR(p)$.  
*注意: 随机干扰项$\varepsilon_t$满足$E\varepsilon_t=0,Var(\varepsilon_t)=\sigma^2,E(\varepsilon_t \varepsilon_s)=0,s\neq t$.*  

2. 中心化模型  
当$\phi_0 = 0$,为**中心化AR(p)模型:**  
当$\phi_0 \neq 0$,令$\mu= \dfrac{\phi_0}{1-\phi_1-\cdots-\phi_p},y_t=x_t-\mu$,则${y_t}$为中心化序列.  
中心化$AR(p)$模型可表示为
$$\Phi(B)x_t=\varepsilon_t,\Phi(B)=1-\phi_1B-\phi_2B^2-\cdots-\phi_p B^p$$

3. 解释$\phi_1$影响  
针对中心化$AR(1)$模型$y_t=\phi_1 y_{t-1}+\varepsilon_t$.反复迭代:  
$\begin{align} 
y_t =\phi_1 y_{t-1}+\varepsilon_t=\phi_1(\phi_1 y_{t-2}+\varepsilon_{t-1})+\varepsilon_t=\phi_1^2 y_{t-2}+\phi_1 \varepsilon_{t-1}+\varepsilon_t=\cdots \\ 
    &=\sum_{k=0}^{\infty} \phi_1^k \varepsilon_{t-k} \tag{2.10}
\end{align}$  
服从$AR(1)$过程的时间序列经过多次迭代成为白噪声序列${\varepsilon_t}$的加权和,$\phi_1^k$描述了第$t-k$期噪声对$y_t$的影响,如果$|\phi_1|<1$,意味着随着k的增加,噪声对$y_t$的影响越来越弱,特别地,当$k \rightarrow \infty$,噪声对$y_t$影响趋于零.此时$y_t$是个平稳的时间序列.

### 2.2.2 稳定性与平稳性
1. Green函数: 设${x_t,t \in T}$是一个序列,如果$x_t$可表示为零均值白噪声序列$\varepsilon_t$的级数和,即  
$$x_t=G_0\varepsilon_t+G_1\varepsilon_{t-1}+G_2\varepsilon_{t-2}+\cdots$$  
那么系数函数$G_i(i=0,1,2,\cdots)$称为**Green函数.**  
根据$(2.10)$,$AR(1)$序列可以表示为$x_t=\sum\limits_{k=0}^{\infty}\phi_1^k \varepsilon_{t-k}$,所以$AR(1)$模型的Green函数是$G_k=\phi_1^k$.  
**Green函数的递推计算公式:**  
$$G_0=1, G_k=\sum\limits_{i=1}^{k}\phi_i^* G_{k-i},k=1,2,\cdots$$.  
其中,当$i\leq p$时,$\phi_i^* =\phi_i$;当$i>p$时,$\phi_i^* =0$.



2. AR模型平稳性的判定:  
**定理2.1** 设${x_t,t \in T}$是一个中心化$AR(p)$模型,  
$$\Phi(B) x_t=\varepsilon_t.$$  
其中$\Phi(B)=1-\phi_1 B-\phi_2 B^2-\cdots-\phi_p B^p$,则${x_t,t \in T}$平稳的充要条件是:  
$$\Phi(\mu)=1-\phi_1 \mu-\phi_2 \mu^2-\cdots-\phi_p \mu_p=0$$.  
的根在单位圆外.






























