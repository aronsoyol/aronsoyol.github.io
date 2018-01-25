---
title: ベータ関数とガンマ関数の関係
layout: post
---


## ベータ関数

$$\begin{eqnarray}
B(x,y)&=& \int_0^1{t^{x-1}(1-t)^{y-1}dt}\\
&=& \int_0^1{\frac{1}{x}(1-t)^{y-1}dt^x}\\
&=& \left[\frac{1}{x}(1-t)^{y-1}t^x\right]_0^1-\frac{1}{x}\int_0^1{t^x d(1-t)^{y-1}}\\
&=&-\frac{1}{x}\int_0^1{(y-1){(1-t)^{y-2}}t^x d(-t)}\\
&=&\frac{y-1}{x}\int_0^1{t^x (1-t)^{y-2} dt}\\
&=&\frac{y-1}{x}B(x+1,y-1)\\
&=&\frac{y-1}{x}\frac{y-2}{x+1}B(x+2,y-2)\\
&=&\frac{y-1}{x}\frac{y-2}{x+1}...\frac{1}{x+y-2}B(x+y-1,1)\label{eq:beta_last}\\
&=&\frac{(y-1)!(x-1)!}{(x+y-1)!}
\end{eqnarray}$$

ここで式$\ref{eq:beta_last}$のベータ関数は

$$\begin{eqnarray}
B(x+y-1,1)&=&\int_0^1{t^{x+y-2} dt}=\frac{1}{x+y-1}\\
\end{eqnarray}$$

## ガンマ関数

$$\begin{eqnarray}
\Gamma(x)&=(x-1)\Gamma(x-1)&\\
\end{eqnarray}$$

ガンマ関数は階乗の一般化なので、ベータ関数の階乗をガンマ関数に書き換えると

$$\begin{eqnarray}
B(x,y)&=&\frac{\Gamma(x)\Gamma(y)}{\Gamma(x+y)}\\
\end{eqnarray}$$