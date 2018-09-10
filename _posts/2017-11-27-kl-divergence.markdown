---
title: KL情報量
layout: post
---

- divergence  
分歧; 差异

- **Kullback-Leibler divergence**

## KLダイバージェンス[^ref1]

二つの確率分布p(x)とq(x)のKLダイバージェンスは以下のように定義されます

$$\begin{equation}KL(p, q) =\sum_\limits{x}p(x)\log\frac{p(x)}{q(x)} \end{equation}$$

- KLダイバージェンスはゼロ以上

$$KL(q, p)\ge 0$$

- pとqが同じ分布である必要十分条件はKLダイバージェンスがゼロである

$$KL(p, q) = 0 \iff p =q$$


## KL情報量[^ref2]

- 公式

$$\begin{equation}KL[p^*(x)\Vert p(x|\phi)]=\int p^*(x)\log\frac{p^*(x)}{p(x|\phi)}dx.\end{equation}$$

- 性質

$$KL[p^*(x)\|p(x|\phi)] \geq 0$$

KL情報量が０の時は真の分布と近似の分布が一致する

$$KL[p^*(x)\Vert p(x|\phi)] = 0\iff p^*(x)=p(x|\phi)$$

- 以下によって$p(x\vert\phi)$を求める

$$\phi^*= \mathop{\rm argmin}\limits_{\phi}\left\{KL[p^*(x)\Vert p(x|\phi)]\right\}$$

## Jensen-Shannon ダイバージェン
KL不对称

$$KL(p, q) \neq KL(q,p)$$

所以引入JS

$$\begin{eqnarray}JS(P,Q)= \frac{1}{2}KL(P,M)+\frac{1}{2}KL(P,M)\\
ただし、M=\frac{P(X)+Q(X)}{2}\end{eqnarray}$$

$$JS(P,Q) = JS(Q,P)$$

## 参考文献

[^ref1]: 岩田具治, 「トピックモデル」,p6
[^ref2]: 奥村学,「トピックモデルによる統計的潜在意味解析」,p41
