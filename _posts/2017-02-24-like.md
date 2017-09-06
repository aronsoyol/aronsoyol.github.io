---
layout: post
author: aron
title: 最尤推定 VS 全確率定理
categories: 数学
data: 2017-02-24
tag: [最尤推定, 全確率定理, 音声認識]
---


*『音声認識システム』p26,28

## 事像$X_i$の確率  $p_i^{ML}$と$p_i^{TP}$


### キーワード

 - 最尤推定 Maximum Likelihood Estimation(ML)
 - 全確率定理 Total Probability Theorem(TP)

複数系列O<sub>k</sub>(1<=k<=K)が確率的に与えられており、その観測確率がp(O<sub>k</sub>)で与えられている場合、事像X<sub>i</sub>の生起回数n<sub>i</sub>で、その期待値は:

$$E(n_i)=\sum\limits_{k=1}^Kp(O_k)\cdot n_i^{(k)\tag{1}}$$

但し，$n_i^{(k)}$は事像k番目の系列において、事像X<sub>i</sub>の生起回数である。この時、最尤パラメータは

$$\tag{2}p_i^{ML}=\frac{\sum\limits_{k=1}^Kp(O_k)\cdot n_i^{(k)}}{\sum\limits_{i=1}^M\sum\limits_{k=1}^Kp(O_k)\cdot n_i^{(k)}}=\frac{E(n_i)}{\sum\limits_{i=1}^ME(n_i)} $$

により求めることができる。しかしp(O<sub>k</sub>)が既知で、且つ全事像のn<sub>i</sub>が全ての系列に於いて数えられる場合、全確率の定理によって

$$p_i^{TP}=\sum\limits_{k=1}^Kp(O_k)\cdot p(i|O_k)$$

$p_i$が簡単に求まるのでは？ここで$p_i^{ML}$と$p_i^{TP}$はどんな関連があるのだろう？？？

***
<div style="text-align: center;font-size:3em">
$p_i^{ML}\quad vs \quad p_i^{TP}$</div>
***

## 例

A,B,C三種類の系列がある。 
 - **A** 長さ:300, 個数3
<div style="width: 300px;padding: 5px 0px 0px 0px;margin:0px 0px 30px 0px !important;">
	<table style="width: 100%; display: table;;margin: 0px">
		<tr>
			<td style="width: 50%; background-color: green;border: 0px;margin: 0px;padding: 0px;text-align: center">150</td>
			<td style="width: 20%; background-color: yellow;border: 0px;margin: 0px;padding: 0px;text-align: center">60</td>
			<td style="width: 30%; background-color: red;border: 0px;margin: 0px;padding: 0px;text-align: center">90</td>
		</tr><tr>
			<td style="width: 50%; background-color: green;border: 0px;margin: 0px;padding: 0px;text-align: center">150</td>
			<td style="width: 20%; background-color: yellow;border: 0px;margin: 0px;padding: 0px;text-align: center">60</td>
			<td style="width: 30%; background-color: red;border: 0px;margin: 0px;padding: 0px;text-align: center">90</td>
		</tr><tr>
			<td style="width: 50%; background-color: green;border: 0px;margin: 0px;padding: 0px;text-align: center">150</td>
			<td style="width: 20%; background-color: yellow;border: 0px;margin: 0px;padding: 0px;text-align: center">60</td>
			<td style="width: 30%; background-color: red;border: 0px;margin: 0px;padding: 0px;text-align: center">90</td>
		</tr>
	</table></div>

 - <strong>B</strong> 長さ:600,個数9
<div style="width: 600px;padding: 5px 0px 0px 0px;margin:0px 0px 30px 0px !important;">

	<table style="width: 100%; display: table;margin: 0px">
		<tr>
			<td style="width: 50%; background-color: green;border: 0px;margin: 0px;padding: 0px;text-align: center">300</td>
			<td style="width: 40%; background-color: yellow;border: 0px;margin: 0px;padding: 0px;text-align: center">240</td>
			<td style="width: 10%; background-color: red;border: 0px;margin: 0px;padding: 0px;text-align: center">60</td>
		</tr><tr>
			<td style="width: 50%; background-color: green;border: 0px;margin: 0px;padding: 0px;text-align: center">300</td>
			<td style="width: 40%; background-color: yellow;border: 0px;margin: 0px;padding: 0px;text-align: center">240</td>
			<td style="width: 10%; background-color: red;border: 0px;margin: 0px;padding: 0px;text-align: center">60</td>
		</tr><tr>
			<td style="width: 50%; background-color: green;border: 0px;margin: 0px;padding: 0px;text-align: center">300</td>
			<td style="width: 40%; background-color: yellow;border: 0px;margin: 0px;padding: 0px;text-align: center">240</td>
			<td style="width: 10%; background-color: red;border: 0px;margin: 0px;padding: 0px;text-align: center">60</td>
		</tr><tr>
			<td style="width: 50%; background-color: green;border: 0px;margin: 0px;padding: 0px;text-align: center">300</td>
			<td style="width: 40%; background-color: yellow;border: 0px;margin: 0px;padding: 0px;text-align: center">240</td>
			<td style="width: 10%; background-color: red;border: 0px;margin: 0px;padding: 0px;text-align: center">60</td>
		</tr><tr>
			<td style="width: 50%; background-color: green;border: 0px;margin: 0px;padding: 0px;text-align: center">300</td>
			<td style="width: 40%; background-color: yellow;border: 0px;margin: 0px;padding: 0px;text-align: center">240</td>
			<td style="width: 10%; background-color: red;border: 0px;margin: 0px;padding: 0px;text-align: center">60</td>
		</tr><tr>
			<td style="width: 50%; background-color: green;border: 0px;margin: 0px;padding: 0px;text-align: center">300</td>
			<td style="width: 40%; background-color: yellow;border: 0px;margin: 0px;padding: 0px;text-align: center">240</td>
			<td style="width: 10%; background-color: red;border: 0px;margin: 0px;padding: 0px;text-align: center">60</td>
		</tr><tr>
			<td style="width: 50%; background-color: green;border: 0px;margin: 0px;padding: 0px;text-align: center">300</td>
			<td style="width: 40%; background-color: yellow;border: 0px;margin: 0px;padding: 0px;text-align: center">240</td>
			<td style="width: 10%; background-color: red;border: 0px;margin: 0px;padding: 0px;text-align: center">60</td>
		</tr><tr>
			<td style="width: 50%; background-color: green;border: 0px;margin: 0px;padding: 0px;text-align: center">300</td>
			<td style="width: 40%; background-color: yellow;border: 0px;margin: 0px;padding: 0px;text-align: center">240</td>
			<td style="width: 10%; background-color: red;border: 0px;margin: 0px;padding: 0px;text-align: center">60</td>
		</tr><tr>
			<td style="width: 50%; background-color: green;border: 0px;margin: 0px;padding: 0px;text-align: center">300</td>
			<td style="width: 40%; background-color: yellow;border: 0px;margin: 0px;padding: 0px;text-align: center">240</td>
			<td style="width: 10%; background-color: red;border: 0px;margin: 0px;padding: 0px;text-align: center">60</td>
		</tr>
	</table></div>

 - <strong>C</strong> 長さ500, 個数:4

<div style="width: 500px;padding: 5px 0px 0px 0px;margin:0px 0px 30px 0px !important;">

	<table style="width: 100%; display: table;">
	<tr>
		<td style="width: 50%; background-color: green;border: 0px;margin: 0px;padding: 0px;text-align: center">250</td>
		<td style="width: 20%; background-color: yellow;border: 0px;margin: 0px;padding: 0px;text-align: center">100</td>
		<td style="width: 30%; background-color: red;border: 0px;margin: 0px;padding: 0px;text-align: center">150</td>
	</tr><tr>
		<td style="width: 50%; background-color: green;border: 0px;margin: 0px;padding: 0px;text-align: center">250</td>
		<td style="width: 20%; background-color: yellow;border: 0px;margin: 0px;padding: 0px;text-align: center">100</td>
		<td style="width: 30%; background-color: red;border: 0px;margin: 0px;padding: 0px;text-align: center">150</td>
	</tr><tr>
		<td style="width: 50%; background-color: green;border: 0px;margin: 0px;padding: 0px;text-align: center">250</td>
		<td style="width: 20%; background-color: yellow;border: 0px;margin: 0px;padding: 0px;text-align: center">100</td>
		<td style="width: 30%; background-color: red;border: 0px;margin: 0px;padding: 0px;text-align: center">150</td>
	</tr><tr>
		<td style="width: 50%; background-color: green;border: 0px;margin: 0px;padding: 0px;text-align: center">250</td>
		<td style="width: 20%; background-color: yellow;border: 0px;margin: 0px;padding: 0px;text-align: center">100</td>
		<td style="width: 30%; background-color: red;border: 0px;margin: 0px;padding: 0px;text-align: center">150</td>
	</tr>
</table></div>

### 最尤パラメータ推定

$$\begin{align*}
\\E(G) &= \frac{3}{16} × 150 &+& \frac{9}{16} × 300 &+& \frac{4}{16} × 250 = 259.375  
\\E(Y) &= \frac{3}{16} ×  60 &+& \frac{9}{16} × 240 &+& \frac{4}{16} × 100 = 171.25 
\\E(R) &= \frac{3}{16} ×  90 &+& \frac{9}{16} ×  60 &+& \frac{4}{16} × 150 = 88.125 
\end{align*}$$

 - <strong>平均系列</strong> 長さ＝ 259.375 + 171.25 + 88.125 = <strong>518.7</strong>

<table style="display: table !important;">
	<tr style="border: 0px;margin: 0px;padding: 0px;text-align: center">
		<td style="width: 259.375px; background-color: green;border: 0px;margin: 0px;padding: 0px;">259.375</td>
		<td style="width: 171.25px; background-color: yellow;border: 0px;margin: 0px;padding: 0px;">171.25</td>
		<td style="width: 88.125px; background-color: red;border: 0px;margin: 0px;padding: 0px;">88.125</td>
	</tr>
</table>
$$\begin{align*}
\\p^{ML}(G)&=\frac{E(G)}{E(G) + E(Y) + E(R)}=\frac{259.375}{518.7} = 0.50
\\p^{ML}(Y)&=\frac{E(Y)}{E(G) + E(Y) + E(R)}=\frac{171.2  }{518.7} = 0.33
\\p^{ML}(R)&=\frac{E(R)}{E(G) + E(Y) + E(R)}=\frac{ 88.125}{518.7} = 0.17
\end{align*}$$

### 全確率の定理

|  |G |Y |R |
|:-|:-|:-|:-|
| p(A) = 3/16 | p(G\|A) = 150/300 | p(Y\|A) =  60/300 | p(R\|A) =  90/300 |
| p(B) = 9/16 | p(G\|B) = 300/600 | p(Y\|B) = 240/600 | p(R\|B) =  60/600 |
| p(C) = 4/16 | p(G\|C) = 250/500 | p(Y\|C) = 100/500 | p(R\|C) = 150/500 |

$p(G)$  
$= p(A) × p(G|A) + p(B) × p(G|B) + p(C) × p(G|C)$    
$= 3/16 × 150/300 + 9/16 × 300/600 + 4/16 × 250/500$   
$= 0.5$ 

$p(Y)$  
$= p(A) × p(Y|A) + p(B) × p(Y|B) + p(C) × p(Y|C)$  
$= 3/16 × 60/300 + 9/16 × 240/600 + 4/16 × 100/500$   
$= 0.3125$  

$p(R)$  
$= p(A) × p(R|A) + p(B) × p(R|B) + p(C) × p(R|C)$  
$= 3/16 × 90/300 + 9/16 × 60/600 + 4/16 × 150/500$   
$= 0.1875$  
 
## 比較

~~全確率の公式で求まるのに、なぜ最尤パラメータ推定なんかをする必要が生じるのだろう？<strong>全確率公式が適用せず、最尤パラメータ推定をしなければならない場合は今一思いつかない。</strong>~~

最尤推定は、その名の通り尤度を最大にする事が目的である。しかし、本当に尤度が最大になったのか？
尤度を比べてみる：   
$$\begin{align*}\\
L^{ML}&=p^{ML}(G)×p^{ML}(Y)×p^{ML}(R)&=&0.5×0.33×0.17&=&0.02805\\
L^{TP}&=p(G)×p(Y)×p(R)&=&0.5×0.3125×0.1875&=&0.029296\\
\end{align*}$$

$L_{最尤推定}< L_{完全確率}$
結果として最尤推定が負けた。
<div style="text-align: center;font-size:5em">
どうして？？</div>
