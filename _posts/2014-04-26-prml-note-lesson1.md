---
layout: post
title: "PRML笔记--第一次课"
categories: 
- PRML笔记
tags: 
- Machine Learning
- PRML
- 


---
PRML讨论第一次课，讲的很好，把笔记记录下来。

## 本书的主要线索
>1. 模型是不是贝叶斯模型？
>1. 一个模型是有监督还是无监督？
>1. 一个模型是离散的还是连续的？
>1. 一个模型是参数模型还是非参模型？

## 参数方法与非参方法

### 区别

1. 参数方法：参数个数固定，以一种全局的方式去拟合一条曲线，注重整体性
1. 非参方法：参数不固定，随样本增加而增加(如KNN)；是以一种局部的方式去预测附近新
   数据点的位置

### 使用场景

1. 低维时，使用非参比较好。相信数据比较平滑，预测附近值
1. 高维时，使用参数方法，从整理拟合曲线。数据高维时，数据量比较少的时候，把空间
   想象成一个球体，那么在球体外壳质量占比更大，因而数据趋向于分布在壳上。数据高
  维时，如果要用非参方法，应该先做特征选择进行降维，相当于L0正则

## 机器学习的基础

概率论、信息论、线性代数

两种角度：离散数据时用概率分布；连续数据用概率密度

Bayes公式：
\begin{equation} p(x|y)=p(y|x)p(x)/p(y) \end{equation}
按Bayes理解，$p(x|y)是后验，$$p(y|x)$是似然，$p(x)$看成先验，$p(y)$看成是归一项或模型证据
即：$后验=似然×先验/归一项$

概率的两个性质：

1. 加法法则：$p(y)=\sum \_x p(x,y)$
1. 乘法法则：$p(x,y)=p(x\|y)p(y)$

## 频率学派与贝叶斯学派

频率学派：数据是变化的，参数是固定的
贝叶斯学派：数据是固定的，参数是随机变量；通过求概率来求解

极大似然估计(点估计)：\begin{equation} arg\_\theta p(D|\theta) \end{equation}
天然会产生过拟合，一般是加正则的方式，即加先验$p(\theta)$,
得到贝叶斯极大似然估计：\begin{equation}p(\theta|D) \propto arg\_\theta p(D|\theta)p(\theta) \end{equation}
贝叶斯估计：先求$p(\theta|D)$，再求解\begin{equation} p(t) = \int p(t|\theta)p(\theta|D)d\theta \end{equation}
相当于在数据D上求期望

## 机器学习的一般过程

数据集一般可分为训练集(train)、验证集(valid)和测试集(test)，如下图所示。机器学习的过程一般如下：

>1. 模型选择：选超参$\lambda$，确定模型的复杂度。用训练集进行训练，再用验证集验证结果来对模型进行选择
>1. 模型评估：将训练好的模型在测试集上进行最终的效果评估

![数据集](../../../images/dataset.jpeg)
当数据集较少时，为充分利用数据，一般会在模型通过评估后，会将确定好的模型在所有的数据集(train+valid+test)
进行训练，得到最终的参数(如逻辑回归中的权重参数)

**过拟合**：训练集上表现好，测试集上表现差
因而，希望模型尽量简单，函数变化缓慢，而不是剧烈变化

## 几种分布

1. 高斯分布
\begin{equation}N(x|\mu,{\delta}^2)=\frac{1}{Z}e^{-\frac{(x-\mu)^2}{2\delta^2}}\end{equation}
期望$\mu$：\begin{equation}\mu=\int xp(x)dx\end{equation}
方差${\delta}^2$：\begin{equation} {\delta}^2=\int (x-\mu)^2p(x)dx\end{equation}

1. T分布
\begin{equation}T(x)=\int_{0}^{\infty}t^{x-1}e^{-t}dt\end{equation}

1. 多维高斯
\begin{equation}N(x|\mu,\Sigma)=\frac{1}{Z}e^{-(x-\mu)^T\Sigma^{-1}(x-\mu)}\end{equation}

