---
title: EM 算法
categories: [Statistics]
comments: true
---

## 介绍EM算法

EM算法是基于隐变量思想提出的一种算法。

+ 首先根据己经给出的观测数据，估计出模型参数的值；
+ 然后再依据上一步估计出的参数值估计缺失数据的值；
+ 再根据估计出的缺失数据加上之前己经观测到的数据重新再对参数值进行估计。
+ 然后反复迭代，直至最后收敛，迭代结束。


## 前置知识

+ 极大似然估计
+ Jensen不等式

$$f(E(x))\le E(f(x))$$

## 例子：男女生身高分布

我们目前有100个男生和100个女生的身高，但是我们不知道这200个数据中哪个是男生的身高，哪个是女生的身高，即抽取得到的每个样本都不知道是从哪个分布中抽取的。这个时候，对于每个样本，就有两个未知量需要估计：
+ （1）这个身高数据是来自于男生数据集合还是来自于女生？
+ （2）男生、女生身高数据集的正态分布的参数分别是多少？

### 问题条件

已知：
+ （1）分布模型
+ （2）随机抽取的样本

未知：
+ （1）每一个样本属于哪个分布
+ （2）分布的具体参数

### 算法流程

（1）初始化模型参数

（2）计算每一个样本来自男生分布或是女生分布

（3）通过（2）中属于男生分布的样本来重新估计男生分布的参数（极大似然估计），女生分布同理。

（4）重复（1）-（3）步骤，直到参数不发生变化，迭代终止。

## EM算法推导过程

+ （1）求样本的对数似然函数：

$$
l(\theta)=\log \prod_{i} p\left(x_{i} ; \theta\right)=\sum_{i} \log p\left(x_{i} ; \theta\right)
$$

+ (2)极大似然估计得到参数：

$$
\hat{\theta}=\operatorname{argmax} l(\theta)=\operatorname{argmax} \sum_{i} \log \sum_{z_{i}} p\left(x_{i}, z_{i} ; \theta\right)
$$

+ （3）由于$𝑝(𝑥_𝑖,𝑧_𝑖;\theta)$不能直接得到，故接下来利用Jensen不等式来找到它的逼近。

+ (4) 利用Jensen不等式缩放上式，其中$𝑄_𝑖 (𝑧_𝑖 )$为概率分布：

$$\sum_{i} \log \sum_{z_{i}} p\left(x_{i}, z_{i} ; \theta\right)= \sum_{i} \log \sum_{z_{i}} Q_{i}\left(z_{i}\right) \frac{p\left(x_{i}, z_{i} ; \theta\right)}{Q_{i}\left(z_{i}\right)}$$

$$\geq \sum_{i} \sum_{z_{i}} Q_{i}(z_{i}) \log \frac{p(x_{i}, z_{i} ; \theta)}{Q_{i}(z_{i})}$$

+ （5）由不等式成立的条件，$\sum_{i} \log \sum_{z_{i}} Q_{i}\left(z_{i}\right) \frac{p\left(x_{i}, z_{i} ; \theta\right)}{Q_{i}\left(z_{i}\right)}$为$l(\theta)$的下界，故改变$𝑄_𝑖 (𝑧_𝑖 )$的分布，可以使得$\sum_{i} \log \sum_{z_{i}} Q_{i}\left(z_{i}\right) \frac{p\left(x_{i}, z_{i} ; \theta\right)}{Q_{i}\left(z_{i}\right)}$的结果等于$l(\theta)$

+ (6)由于Jensen不等式要取等的条件是:

$$\frac{p\left(x_{i}, z_{i} ; \theta\right)}{Q_{i}\left(z_{i}\right)}=C$$

其中，c为常数
+ （7）又由于 $Q_{i}\left(z_{i}\right)$ 为概率分布，故满足： $\sum_{i} Q_{i}\left(z_{i}\right)=1$, 则 $\sum_{z} p\left(x_{i}, z_{i} ; \theta\right)=c$，故: 

$$Q_{i}\left(z_{i}\right)=\frac{p\left(x_{i}, z_{i} ; \theta\right)}{\sum_{z} p\left(x_{i}, z_{i} ; \theta\right)}=\frac{p\left(x_{i}, z_{i} ; \theta\right)}{p\left(x_{i} ; \theta\right)}=p\left(z_{i} \mid x_{i} ; \theta\right)$$

+ (8)综上所述: 

$$\hat{\theta}=argmax \sum_{i} \sum_{z_{i}} Q_{i}\left(z_{i}\right) \log \frac{p\left(x_{i}, z_{i} ;\theta\right)}{Q_{i}\left(z_{i}\right)}$$

其中: $\quad Q_{i}\left(z_{i}\right)=p\left(z_{i} \mid x_{i} ; \theta\right)$

## 算法流程


输入：
+ 数据$x=(x_1,x_2,…,x_n)$,
+ 联合分布$𝑝(x,z;\theta)$，
+ 条件分布$𝑝(z \mid x,\theta)$，
+ 最大迭代次数J。

初始化：
+ 随机初始化模型参数$\theta$为$\theta_0$
+ $j=1,2,\dots,J$开始迭代：
+ - E步：计算联合分布的条件概率期望

$$Q_{i}\left(z_{i}\right)=p\left(z_{i} \mid x_{i} ; \theta\right)$$

$$l\left(\theta, \theta_{j}\right)=\sum_{i} \sum_{z_{i}} Q_{i}\left(z_{i}\right) \log \frac{p\left(x_{i}, z_{i} ; \theta\right)}{Q_{i}\left(z_{i}\right)}$$

+ + M步：极大化 $l\left(\theta, \theta_{j}\right), \quad$ 得到 $\theta_{j+1}$

$$\theta_{j+1}=\operatorname{argmax} l\left(\theta, \theta_{j}\right)$$

输出：模型参数$\theta$
