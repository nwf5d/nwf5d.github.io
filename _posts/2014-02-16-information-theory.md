---
layout: post
title: "信息论"
categories:
- Machine Learning 
tags:
- 机器学习
- 信息
- 信息熵


---

信息论（Information Theory）是概率论与数理统计的一个分枝。用于信息处理、信息熵、通信系统、数据传输、率失真理论、密码学、信噪比、数据压缩和相关课题。

## 基本概念
先说明一点：在信息论里面对数log默认都是指以2为底数。

* 自信息量: 
\begin{equation} 
I(x_i) = -logp(x_i) 
\label{eq:self_infomation_content} 
\end{equation}

* 联合信息量: 
\begin{equation} 
I(x_i,y_i) = -logp(x_i,y_i) 
\label{eq:joint_infomation_content} 
\end{equation}

* 条件信息量: 
\begin{equation} 
I(x_i|y_i) = -logp(x_i|y_i) 
\label{eq:conditional_infomation_content} 
\end{equation}

* 信息熵: 
\begin{equation} 
H(X) = -\sum p(x_i)logp(x_i)
\label{eq:infomation_entropy} 
\end{equation}

* 条件熵: 
\begin{equation} 
H(X|Y) = -\sum_i\sum_j p(x_i,y_j)logp(x_i|y_j) = \sum_i \sum_j p(x_i,y_j)I(x_i|y_j)
\label{eq:conditional_entropy} 
\end{equation}

* 联合熵: 
\begin{equation} 
H(X,Y) = -\sum_i\sum_j p(x_i,y_j)logp(x_i,y_j) = \sum_i \sum_j p(x_i,y_j)I(x_i,y_j)
\label{eq:joint_entropy} 
\end{equation}

根据链式规则，有：
\begin{equation} 
H(X,Y) = H(X) + H(Y|X) = H(Y) + H(X|Y)
\label{eq:chained_rule1} 
\end{equation}
可以得出：
\begin{equation} 
H(X) - H(X|Y) = H(Y) - H(Y|X)
\label{eq:chained_rule2} 
\end{equation}

## 信息增益Information Gain
系统原先的熵是H(X)，在条件Y已知的情况下系统的熵（条件熵）为H(X|Y)，信息增益就是这两个熵的差值。
\begin{equation} 
IG = H(X) - H(X|Y) = H(Y) - H(Y|X)
\label{eq:information_gain} 
\end{equation}
熵表示系统的不确定度，所以信息增益越大表示条件Y对于确定系统的贡献越大。

### 信息增益在特征选择中的应用 
由（9）式可以直接推出词条w的信息增益，（9）式中的X代表类别的集合，Y代表w存在和不存在两种情况:

\begin{equation} 
IG(w) = H(C) - H(C|w) = -\sum_i p(c_i)logp(c_i) + \sum_ip(c_i,w)log(p(c_i|w)+ \sum_i p(c_i,\overline{w})log p(c_i|\overline{w}) = -\sum_ip(c_i)logp(c_i)+p(w)\sum_ip(c_i|w)logp(c_i|w)+p(\overline{w})\sum_ip(c_i|\overline{w})logp(c_i|\overline{w})
\label{eq:information_gain_fs} 
\end{equation}

$p(c_i)$ 是第i类文档出现的概率;
$p(w)$是在整个训练集中包含w的文档占全部文档的比例;
$p(c_i|w)$ 表示出现w的文档集合中属于类别i的文档所占的比例;
$p(c_i|\overline{w})$ 表示没有出现w的文档集合中属于类别i的文档所占的比例。

### 信息增益在决策树中的应用

| outlook | temperature | humidity | windy | play |
|----|:----|:----|:----|:----|
| sunny | hot | high | FALSE | no |
| sunny | hot | high | TRUE | no |
| overcast | hot | high | FALSE | yes |
| rainy | mild | high | FALSE | yes |
| rainy | cool | normal | FALSE | yes |
| rainy | cool | normal | TRUE | no |
| overcast | cool | normal | TRUE | yes |
| sunny | mild | high | FALSE | no |
| sunny | cool | normal | FALSE | yes |
| rainy | mild | normal | FALSE | yes |
| sunny | mild | normal | TRUE | yes |
| overcast | mild | high | TRUE | yes |
| overcast | hot | normal | FALSE | yes |
| rainy | mild | high | TRUE | no |

（7）式中的X表示打球和不打球两种情况。 

只看最后一列我们得到打球的概率是9/14，不打球的概率是5/14。因此在没有任何先验信息的情况下，系统的熵（不确定性）为
$H(X)=-\frac{9}{14}log\frac{9}{14}-\frac{5}{14}log\frac{5}{14}=0.94$

|outlook | temperature | humidity | windy | play |
|  | yes | no | | yes | no | | yes | no | | yes | no | yes | no |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| sunny | 2 | 3 | hot | 2 | 2 | high | 3 | 4 | FALSE | 6 | 2 | 9 | 5 |
| overcast | 4 | 0 | mild | 4 | 2 | normal | 6 | 1 | TRUR | 3 | 3 |  | |
| rainy | 3 | 2 | cool | 3 | 1 |  | | | | | | | |

如果选outlook作为决策树的根节点，（7）式中的Y为集合{sunny、overcast、rainy}，此时的条件熵为
$H(X|Y)=-\frac{5}{14}(\frac{2}{5}log\frac{2}{5}+\frac{3}{5}log\frac{3}{5})-\frac{4}{14}(\frac{4}{4}log\frac{4}{4}+0log0)-\frac{5}{14}(\frac{3}{5}log\frac{3}{5}+\frac{2}{5}log\frac{2}{5})=0.693$
$H(X|Y)=-\frac{5}{14}[\frac{5}{14}log\frac{9}{14}+\frac{9}{14}log\frac{9}{14}]$
即选择outlook作为决策树的根节点时，信息增益为0.94-0.693=0.247。

同样方法计算当选择temperature、humidity、windy作为根节点时系统的信息增益，选择IG值最大的作为最终的根节点。

## 互信息Mutual Information
$y_j$对$x_i$的互信息定义为后验概率与先验概率比值的对数。

\begin{equation} 
I(x_i;y_j) = log \frac{p(x_i|y_j)}{p(x_i}=I(x_i)-I(x_i|y_j)
\label{eq:mutual_information} 
\end{equation}
互信息越大，表明$y_j$对于确定$x_i$的取值的贡献度越大。
系统的平均互信息：
\begin{equation} 
I(X:Y) = \sum_i \sum_j p(x_i,y_j)I(x_i;y_j) = \sum_i \sum_jp(x_i,y_j)log \frac{p(x_i|y_j)}{p(x_i}
=H(X)-H(X|Y)=H(Y)-H(Y|X)
\label{eq:avg_mutual_information} 
\end{equation}

*可见平均互信息就是信息增益！*

### 互信息在特征选择中的应用
词条w与类别$c_i$的互信息为
\begin{equation} 
MI(w,c_i) = log \frac{p(w|c_i)}{p(w}
\label{eq:mutual_information_app} 
\end{equation}

$p(w)$表示出现$w$的文档点总文档数目的比例,
$p(w|c_i)$表示在类别
$c_i$中出现$w$的文档点总文档数目的比例。

对整个系统来说，词条$w$的互信息为
\begin{equation} 
MI_{avg}(w,c_i) = \sum_ip(c_i)log \frac{p(w|c_i)}{p(w}
\label{eq:avg_mutual_information_app} 
\end{equation}
最后选互信息最大的前K个词条作为特征项。

## 交叉熵Cross Entropy
  交叉熵是一种万能的Monte-Carlo技术，常用于稀有事件的仿真建模、多峰函数的最优化问题。交叉熵技术已用于解决经典的旅行商问题、背包问题、最短路问题、最大割问题等。这里给一个文章链接：[A Tutorial on the Cross-Entropy Method](http://eprints.eemcs.utwente.nl/7716/01/fulltext.pdf)

  交叉熵算法的推导过程中又牵扯出来一个问题：如何求一个数学期望？常用的方法有这么几种：

  *  概率方法，比如Crude Monte-Carlo
  *  测度变换法change of measure
  *  偏微分方程的变量代换法
  *  Green函数法
  *  Fourier变换法

  在实际中变量X服从的概率分布h往往是不知道的，我们会用g来近似地代替h----这本质上是一种函数估计。有一种度量g和h相近程度的方法叫Kullback-Leibler距离，又叫交叉熵：

\begin{equation} 
D(g,h) = E_g log \frac{g(X)}{h(X)} = \frac{1}{N}\sum_{i=1}g(x_i)log\frac{g(x_i)}{h(x_i)}
\label{eq:kullback-leibler} 
\end{equation}

通常选取g和h具有相同的概率分布类型（比如已知h是指数分布，那么就选g也是指数分布）----参数估计，只是pdf参数不一样（实际上h中的参数根本就是未知的）。

### 基于期望交叉熵的特征项选择

\begin{equation} 
CE(w) = \sum_ip(c_i|w)log\frac{p(c_i|w)}{p(c_i)}
\label{eq:kullback-leibler_app} 
\end{equation}

$p(c_i|w)$表示在出现词条
$w$时文档属于
类别$c_i$的概率。

交叉熵反应了文本类别的概率分布与在出现了某个词条的情况下文本类别的概率分布之间的距离。词条的交叉熵越大，对文本类别分布影响也就越大。所以选CE最大的K个词条作为最终的特征项。

(全文完)

原文来自:[博客园（华夏35度）](http://www.cnblogs.com/zhangchaoyang/articles/2655785.html)
