---
layout: post
author: Aron
title: "复杂度"
date: "2018-06-14 10:31:01 +0900"
permalink: perplexity
---

## 字面意思
- perplexity
n. 困惑；混乱





## 信息量：
假设事件A的发生概率是：$P_A$，
事件A的信息量是：
$$I_A=\log_2{\frac{1}{P_A}} = -\log_2{P_A} $$


## 熵(平均信息量):
- 表示系统的不确定性
-
假设随机变量$X$的取值范围是
$\left\{x_1,x_2,...,x_n \right\}$

$$\begin{array}\
H(X) &= \sum_i P(x_i){I_i} \\ &= -\sum_i P(x_i){\log_2{P(x_i)}}
\end{array}$$

- 取值范围：
$$0 \leq H(X) \leq log(n)$$


- $X$服从均匀分布时，取最大值

## 复杂度(Perplexity):
- 复杂度越低，系统的预测能力越高
$$PP = 2^H$$
- 取值范围
$$1 \leq PP \leq n $$
- 表示语言模型的分歧数，候选数。

## 举例

#### 数据集

- 学习数据集1 ： `A` `B`
- 学习数据集2 ： `A`  `B`  `B`  `B`
- 测试数据  ： `A` `B`

#### 使用数据集1建立模型

- 模型参数
$$P_A=0.5 \\ P_B=0.5$$

- 信息量
$$\begin{array}\
I_A&=\log_2{\frac{1}{P_A}} = -\log_2{P_A} = 1\\
I_B&=\log_2{\frac{1}{P_B}} = -\log_2{P_B} = 1
\end{array}$$

- 熵的计算：
$$H=\frac{{I_A} + {I_B}}{2} = 1$$

- 复杂度是：
$$\begin{array}\
PP_1 = 2^H = 2
\end{array}$$



所以复杂度是**2**。

#### 使用数据集2建立模型

- 模型参数
$$P_A=\frac{1}{4} \\ P_B=\frac{3}{4}$$




- 信息量
$$\begin{array}\
I_A&=\log_2{\frac{1}{P_A}} = -\log_2{P_A} = 2.0\\
I_B&=\log_2{\frac{1}{P_B}} = -\log_2{P_B} = 0.4150374992788438
\end{array}$$

- 熵的计算：
$$H=\frac{{I_A} + {I_B}}{2} = 1.207518749639422$$

- 复杂度是：
$$\begin{array}\
PP_2 = 2^H = 2.3
\end{array}$$

#### 结论
因为$PP_1 < PP_2$，所以 使用数据集1建立的模型,对于测试数据集的预测性能更好。

## LDA 的 Perplexity

$$\exp\left\{ - \frac{\sum_{d=1}^{D^{test}}\log p(\boldsymbol{w}_d^{test}|\mathcal{M})}{\sum_{d=1}^{D^{test}}N_d^{test}}\right\}$$

- $\sum_{d=1}^{D^{test}}N_d^{test}$ 表示所有测试文档中单词数的总和。
    - $N_d$是文档d的单词总数。
    - D是文档的总数。
- $p(\boldsymbol{w}_d^{test}|\mathcal{M})$ 文档d中单词的似然。

$$\begin{array} \
&\quad p(\boldsymbol{w}_d^{test}|\mathcal{M})
&= \prod_{n=1}^{N_d} p(\mathrm{w_{dn}}|\mathcal{M})
\end{array}$$

其中$\boldsymbol{w}_d=\{\mathrm{w_{d1}},\mathrm{w_{d2}},...,\mathrm{w_{dN_d}} \}$，


任意一个单词的分布$$p(\mathrm{w_{dn}}|\mathcal{M}) = \sum_{k=1}^{K}\theta_{dk}\phi_{kw_{dn}}$$


其中

- $\theta_{dk}$ Topic k 出现的概率
- $\phi_{kw_{dn}}$ Topic k 里单词$w_{dn}$出现的概率
