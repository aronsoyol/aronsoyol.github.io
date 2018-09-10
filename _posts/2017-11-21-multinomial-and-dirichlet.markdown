---
title: 多項分布とディリクレ分布
date: 2017-11-21
layout: post
tags : asd, adsf, asdf
---

例えば三色のボールが黒が１/5、白２/5個、青３/5の割合で袋に入っています。今６回ボールをとった結果は{黒,青,白,青,青,白}となりました。

するとこのボールの配列の生成確率は$$\frac{1}{5}\times\frac{3}{5}\times \frac{2}{5} \times\frac{3}{5}\times\frac{3}{5}\times \frac{2}{5}$$と計算されます。

もし、それぞれのボールの回数だけに興味ある場合、つまりp(\{黒× 1,青×3, 白×2\})はどうなるのでしょう？

黒,青,白,青,青,白  
黒,青,青,青,白,白  
黒,青,白,白,青,青  
...  
...  
...  
...  

以上のように、順番が違うけど｛黒× 1,青×3, 白×2｝の取り方はたくさんあります。具体的には


$$
C_6^3C_3^2C_1^1= \frac{6!}{3!3!}\frac{3!}{2!1!}{1!}=\frac{6!}{3!2!}=60
$$通りあります。こんな風に回数だけに興味があって、それの分布を一般化したのが多項分布です。

## 多項分布(Multinomial distribution)

- n回試行、毎回の結果として取りうる値$x_i\in\{1,2,...,K\}$
- $p(\{x_i=k\})=\pi_k$
- $\boldsymbol{\pi}=\lbrace \pi_1,\pi_2,...,\pi_K\rbrace, \sum\limits_{k=1}^K\pi_k=1$
- $p(x_1,x_2,...,x_n)=\prod\limits_{i=1}^{n}p(x_i)= \prod\limits_{i=1}^{K}\pi_i^{n_k}$
- 各試行の回数だけに興味ある場合

$$\begin{aligned}
\quad p(\{n_1,n_2,...,n_K\}|\boldsymbol{\pi},n)& =  Multi(\{n_1,n_2,...,n_K\}|\boldsymbol{\pi},n)\\
&=  C_n^{n_1}C_{n-n_1}^{n_2}...C_{n-\sum_{i=1}^{K-2}n_i}^{n_{k-1}}C_{n_k}^{n_k}\prod\limits_{i=1}^{K}\pi_i^{n_k}\\
&= \frac{n!}{\prod_{k=1}^Kn_k!}\prod\limits_{k=1}^K\pi_k^{n_k}\\
\end{aligned}$$

ここで

$$\begin{aligned}
& \quad C_n^{n_1}C_{n-n_1}^{n_2}...C_{n-\sum_{i=1}^{K-2}n_i}^{n_{k-1}}C_{n_k}^{n_k}\\
&= \frac{n!}{n_1!(n-n_1)!}\cdot \frac{(n-n_1)!}{n_2!(n-n_1-n_2)!}\cdot \frac{(n-n_1-n_2)!}{n_3!(n-n_1-n_2-n_3)!}\cdot...\cdot \frac{n_K!}{n_K!} \\
&= \frac{n!}{\prod_{k=1}^Kn_k!}\\
\end{aligned}$$

## ディリクレ分布(Dirichlet distribution)

- 多項分布の共役事前分布

$$
Dir(\boldsymbol{\pi}|\boldsymbol{\alpha})=\frac{\Gamma\left(\alpha_0\right)}{ \prod_{k=1}^{K}\Gamma\left(\alpha_k\right) }\prod_{k=1}^{K}\pi_k^{\alpha_k-1}$$ 

**Where:**
- $ \alpha_0=\sum_{k=1}^K\alpha_k$
- $ \Gamma(x)=(x-1)!$
- $\boldsymbol{\pi}$：確率変数
- $\boldsymbol{\alpha}$：ハイパーパラメータ


### 事後確率の計算

$$\begin{aligned}
p(\boldsymbol{\pi}|\boldsymbol{x},\boldsymbol{\alpha})\propto p(\boldsymbol{\pi}\vert\boldsymbol{\alpha})f(\boldsymbol{x}|\boldsymbol{\pi})\propto  \prod\limits_{k=1}^K{\pi}_k^{n_k} \cdot \prod_{k=1}^{K}{\pi}_k^{\alpha_k-1} = \prod_{k=1}^{K}{\pi}_k^{n_k+\alpha_k-1}
\end{aligned}$$

正規化すれば

$$\begin{aligned}
p(\boldsymbol{\pi}|\boldsymbol{x},\boldsymbol{\alpha})&= \frac{\prod_{k=1}^{K}{\pi}_k^{n_k+\alpha_k-1}}{\int_{\pi}{\prod_{k=1}^{K}{\pi}_k^{n_k+\alpha_k-1}d{\pi}}}\\
&=\frac{\Gamma\left( n+\alpha_0\right)}{\prod_{k=1}^K\Gamma\left(n_k+\alpha_k \right)}
\end{aligned}$$

但し、以下の証明は？

$$\int_{\pi}{\prod_{k=1}^{K}{\pi}_k^{n_k+\alpha_k-1}d{\pi}}=\frac{\prod_{k=1}^K\Gamma\left(n_k+\alpha_k \right)}{\Gamma\left(n + \alpha_0\right)}\prod_{k=1}^{K}{\pi}_k^{n_k+\alpha_k-1}$$


## 多項分布とディリクレ分布の比較

- 両分布は形式上非常に似ていますが微妙に**違う**。
- ディリクレ分布の正規化項は $\boldsymbol{\pi}$**に対する積分**。
- 多項分布の正規化項は $\boldsymbol{n}$**に対する積分**。


ディリクレ分布のガンマ関数を展開すれば




$$\frac{\left((\sum_{k=1}^K \alpha_k)-1\right)!}{ \prod_{k=1}^{K}(\alpha_k-1)! }\prod_{k=1}^{K}\pi_k^{\alpha_k-1}$$

ここで $\alpha_k-1=\beta_k$ とする

$$\begin{aligned}{}
\alpha_k-1&=\beta_k\\
\sum_{k=1}^K (\alpha_k-1)&=\sum_{k=1}^K\beta_k\\
\sum_{k=1}^K (\alpha_k)-K&=\sum_{k=1}^K\beta_k\\
\sum_{k=1}^K (\alpha_k)&=\sum_{k=1}^K\beta_k+K\end{aligned}$$


$$\therefore Dir(\boldsymbol{\pi}\vert\boldsymbol{\beta})=\frac{\left(\sum_{k=1}^K\beta_k+K-1\right)!}{ \prod_{k=1}^{K}(\beta_k)! }\prod_{k=1}^{K}\pi_k^{\beta_k}$$


|分布|変換した形|正規化項|積分項|
|:-- |:--|:--|---|
|多項分布|$$\frac{\left(\sum_{k=1}^{K}n_k\right)!}{\prod_{k=1}^K(n_k!)} \prod_{k=1}^K\pi_k^{n_k}$$| $$\int_{\boldsymbol{n}\in N}{\prod_{k=1}^K\pi_k^{n_k}d\boldsymbol{n}}$$| $\boldsymbol{n}$ に対する積分|
|ディリクレ分布|$$\frac{\left(\sum_{k=1}^K\beta_k+K-1\right)!}{ \prod_{k=1}^{K}(\beta_k)! }\prod_{k=1}^{K}\pi_k^{\beta_k}$$|$$\int_{\boldsymbol{\pi}\in{\Pi}}{\prod_{k=1}^K\pi_k^{n_k}d\boldsymbol{\pi}}$$| $\boldsymbol{\pi}$ に対する積分|





