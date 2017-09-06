---
title: 潜在トピックモデル
layout: post
categories: 機械学習
date: 2017-08-08
tags: ["Topic_Model", LDA]
---

## Latent Dirichlet Allocation

- 言語モデル
    - 文の生成確率を計算
    - P(吃了吗)=？
- Bag of Words(順序無視、他1-gram)
- Bag of XXX
    - 購買履歴
    - 他画像処理、音声認識、情報検索など
- 教師なし学習
- 「白鵬が単独首位、琴欧州は敗れる。」トピック：相撲、？、？

## LDAの生成過程

- 文章は幾つかのトピックによって生成された（全K個のトピックと仮定）
単語の番号はそのトピックの番号

![adfadf]({{ site.baseurl }}/assets/lda1.jpg)

- トピックごとに単語の生成分布が違う。トピックにXXXのトピックと言うラベルが無い（教師なし学習）

![adfadf]({{ site.baseurl }}/assets/lda2.jpg)

## 多項分布(Multinomial distribution)

- n回試行,取りうる値={1,2,...,K}
- $x_i\in\{1,2,...,K\}$
- $p(x_i=k)=\pi$
- $\boldsymbol{\pi}=\{\pi_1,\pi_2,...,\pi_K\}, \sum\limits_{k=1}^K\pi_k=1$
- $p(x_1,x_2,...,x_n)=\prod\limits_{i=1}^{n}p(x_i)= \prod\limits_{i=1}^{K}\pi_i^{n_k}$
- 各試行の回数だけに興味ある場合

$$\begin{align*}
\quad p(\{n_1,n_2,...,n_K\}|\boldsymbol{\pi},n)& =  Multi(\{n_1,n_2,...,n_K\}|\boldsymbol{\pi},n)\\
&=  C_n^{n_1}C_{n-n_1}^{n_2}...C_{n-\sum_{i=1}^{K-2}n_i}^{n_{k-1}}C_{n_k}^{n_k}\prod\limits_{i=1}^{K}\pi_i^{n_k}\\
&= \frac{n!}{\prod_{k=1}^Kn_k!}\prod\limits_{k=1}^K\pi_k^{n_k}\\
\end{align*}$$

- トピックから単語を生成する分布
- 文章のトピックの分布

## ベイズ的統計(Bayesian statistics)

- ベイズの公式

$$P(B_i|A)= \frac{P(A|B_i)P(B_i)}{P(A)}=\frac{P(A|B_i)p(\theta)}{\sum_{i=1}^{N}P(A|B_i)P(B_i)}$$

- 事後分布

    $$p(\theta\vert\boldsymbol{x})=\frac{p(\theta)f(\boldsymbol{x}\vert\theta)}{\int_{\Theta}p(\theta)f(\boldsymbol{x}\vert\theta)d{\theta}}\propto p(\theta)\cdot f(\boldsymbol{x}\vert\theta)$$

    - $f(\boldsymbol{x}\vert\theta)=\prod_{i=i}^nf(x_i\vert\theta)$は尤度である、尤度は条件部$\theta$の関数で、$x$の分布ではない為、わざと$p$を使わない。
    - ベイズでは分布のパラメータ$\theta$が確率分布すると仮定する
    - $\propto$：比例する
    - 分母は変数$\theta$にとって定数である$\Rightarrow $ 事後分布は事前分布と尤度に比例する

- 尤度関数：$f({\boldsymbol{x}}\vert\theta)$

    - $\theta$が変数
    - $\boldsymbol{x}=\left\\{x_i,x_2,...mx_n\right\\}$が観測値なので定数
    - $\int_{\Theta} f({\boldsymbol{x}}\vert\theta)=1$が成立する保証がないので確率の要件を満たさない。その為わざと$p$と書かない。

- 共役事前分：$p(\theta\vert\eta)$

    - 事後分布と同じ分布族
    - $\eta$：ハイパーパラメータ

- 事後分布2

    $$p(\theta|\boldsymbol{x},\eta)\propto p(\theta\vert\eta)\cdot f(\boldsymbol{x}|\theta)$$


## ディリクレ分布(Dirichlet distribution)

$$\begin{array}{}\\
Dir(\boldsymbol{\pi}|\boldsymbol{\alpha})=\frac{\Gamma\left(\alpha_0\right)}{ \prod_{k=1}^{K}\Gamma\left(\alpha_k\right) }\prod_{k=1}^{K}\pi_k^{\alpha_k-1}\\
但し、 \left\{\begin{array}{ll}\alpha_0&=\sum_{k=1}^K\alpha_k\\
\Gamma(x)&=(x-1)!\end{array}\right.\end{array}$$ 

- 多項分布の共役事前分布
- $\boldsymbol{\pi}$：確率変数
- $\boldsymbol{\alpha}$：ハイパーパラメータ
- 事後確率の計算

    $$\begin{align*}
    p(\boldsymbol{\pi}|\boldsymbol{x},\boldsymbol{\alpha})\propto p(\boldsymbol{\pi}\vert\boldsymbol{\alpha})f(\boldsymbol{x}|\boldsymbol{\pi})\propto  \prod\limits_{k=1}^K{\pi}_k^{n_k} \cdot \prod_{k=1}^{K}{\pi}_k^{\alpha_k-1} = \prod_{k=1}^{K}{\pi}_k^{n_k+\alpha_k-1}
    \end{align*}$$

    正規化すれば

    $$\begin{align*}
    p(\boldsymbol{\pi}|\boldsymbol{x},\boldsymbol{\alpha})&= \frac{\prod_{k=1}^{K}{\pi}_k^{n_k+\alpha_k-1}}{\int_{\pi}{\prod_{k=1}^{K}{\pi}_k^{n_k+\alpha_k-1}d{\pi}}}\\
    &=\frac{\Gamma\left( n+\alpha_0\right)}{\prod_{k=1}^K\Gamma\left(n_k+\alpha_k \right)}
    \end{align*}$$

    但し、以下の証明は？

    $$\int_{\pi}{\prod_{k=1}^{K}{\pi}_k^{n_k+\alpha_k-1}d{\pi}}=\frac{\prod_{k=1}^K\Gamma\left(n_k+\alpha_k \right)}{\Gamma\left(n + \alpha_0\right)}\prod_{k=1}^{K}{\pi}_k^{n_k+\alpha_k-1}$$

## Bayes推定


### 観測値 $\boldsymbol{x}=\\{x_1,x_2,...,x_n\\}$に対して

- 真の分布： $p^*(x)$
    - 知ることが出来ない
    - 現実のデータは何らかの分布から生成されたとは限らない
    - 数学的仮定

- 統計的生成モデル：$p({x}\vert{\phi})$
    - $x_i \sim p(x_i\vert\phi)$
    - $p^*(x)$に出来るだけ近づける

- 問題：
    - $p^*(x)$と$p(x\vert\phi)$どれだけ近い？

### KL情報量

- 公式

$$KL[p^*(x)\|p(x|\phi)]=\int p^*(x)\log\frac{p^*(x)}{p(x|\phi)}dx.$$

- 性質

$$KL[p^*(x)\|p(x|\phi)] \geq 0$$

$$KL[p^*(x)\|p(x|\phi)] = 0\Leftrightarrow p^*(x)=p(x|\phi)$$

- 以下によって$p(x\vert\phi)$を求める

$$\phi^*= \mathop{\rm argmin}\limits_{\phi}\left\{KL[p^*(x)\|p(x|\phi)]\right\}$$

### 最尤推定, Maximum Likelihood Estimattion, (MLE)

$$KL[p^*(x)\|p(x|\phi)]=\int p^*(x)\log\frac{p^*(x)}{p(x|\phi)}dx.$$

- $p^*(x)$による期待値

$$\begin{align*}KL[p^*(x)\|p(x|\phi)]&=\int p^*(x)\log\frac{p^*(x)}{p(x|\phi)}dx.\\
&= \mathbb{E}_{p^*(x)}\left[\log\frac{p^*(x)}{p(x|\phi)}\right]\\
&= \mathbb{E}_{p^*(x)}\left[\log{p^*(x)}\right]-\mathbb{E}_{p^*(x)}\left[\log{p(x|\phi)}\right]
\end{align*}$$

$$\begin{align*}
\phi^*&=\mathop{\rm argmin}\limits_{\phi}\left\{KL[p^*(x)\|p(x|\phi)]\right\}\\
&=\mathop{\rm argmin}\limits_{\phi}\left\{\mathbb{E}_{p^*(x)}\left[\log{p^*(x)}\right]-\mathbb{E}_{p^*(x)}\left[\log{p(x|\phi)}\right]\right\}\\
&=\mathop{\rm argmin}\limits_{\phi}\left\{-\mathbb{E}_{p^*(x)}\left[\log{p(x|\phi)}\right]\right\}\\
&=\mathop{\rm argmax}\limits_{\phi}\left\{\mathbb{E}_{p^*(x)}\left[\log{p(x|\phi)}\right]\right\}\\
\end{align*}$$

- 真の分布
$p^*(x)$
が分からない

    $\mathbb{E}_{p^*(x)}\left[\log{p(x)|\phi)}\right]$
    を求めることが出来ない

- 観測データを真の分布からのサンプルとして期待値計算を近似する

$$\mathbb{E}_{p^*(x)}\left[\log{p(x|\phi)}\right]\approx\frac{1}{n}\sum\limits_{i=1}^n\log p(x_i|\phi)$$

$$\phi_{ML}^*=\mathop{\rm argmax}\limits_{\phi}\left\{\sum\limits_{i=1}^n\log p(x_i|\phi)\right\}$$

### 最大事後確率推定, Maximum a posterior, (MAP)

$$\phi_{MAP}^*=\mathop{\rm argmax}\limits_{\phi}\left\{\log p(\phi|\eta)+\sum\limits_{i=1}^n\log p(x_i|\phi)\right\}$$

- 過学習防止，汎化能力高い

### 期待事後推定, Expected a posterior, (EAP)

- 新たなデータ$x^*$
に対して、

$$p(x^*|\boldsymbol{x})=\int p(x^*|\phi)p(\phi|\boldsymbol{x})d\phi= \mathbb{E}_{p(\phi|\boldsymbol{x})}\left[p(x^*|\phi)\right].$$

- ベイズ推定の枠組み


