---
title: 练习 2-2 解答
date: 2022-12-17 22:17:00
description: 标准记号与常用函数相关的习题解答
---

#### Problem 1 (教材习题 3.2-2)

证明：$a^{\log_b c} = c^{\log_b a}$ 。

##### Solution

证明：因为

$$
\begin{aligned}
\ln{a^{\log_b c}} & = \log_b c\ln a = \frac{\ln c}{\ln b} \ln a \\
& = \frac{\ln a}{\ln b} \ln c = \log_b a\ln c\\
& = \ln{c^{\log_b a}}
\end{aligned}
$$

所以 $a^{\log_b c} = c^{\log_b a}$ 。

#### Problem 2 (教材习题 3.2-3)

证明 $\log(n!) = \Theta(n\log n)$ ，并证明 $n! = \omega(2^n)$ 且 $n! = o(n^n)$ 。

##### Solution

证明：根据斯特林近似公式（见[第2讲PPT第10页](/slides/lec02-growth-of-functions.pdf#page=10)，教材3.2节），有：

$$
\begin{aligned}
\log(n!) &= \log(\sqrt{2\pi n}(\frac{n}{e})^n(1 + \Theta(\frac{1}{n})))\\
&= \frac12\log(2\pi n) + n\log n - n \log e + \log(1 + \Theta(\frac1n))
\end{aligned}
$$

其中最高阶项是 $n \log n$ ，所以 $\log(n!) = \Theta(n\log n)$ 。

$$
\begin{aligned}
\lim_{n \to \infty}\frac{2^n}{n!} &= \lim_{n \to \infty} \frac{1}{\sqrt{2\pi n}(1+\Theta(\frac1n))} (\frac{2e}{n})^n \le \lim_{n \to \infty} (\frac{2e}{n})^n\\
&\le \lim_{n \to \infty} (\frac12)^n ,n \ge 4e \\
&= 0
\end{aligned}
$$

于是 $\lim\limits_{n \to \infty}\frac{2^n}{n!} = 0$ ，则 $n! = \omega(2^n)$ 。

$$
\begin{aligned}
\lim_{n \to \infty}\frac{n^n}{n!} &= \lim_{n \to \infty} \frac{1}{\sqrt{2\pi n}(1+\Theta(\frac1n))} e^n \\
&\ge \lim_{n\to\infty} \frac{e^n}{c\cdot n}, c \text{ is a constant}\\
&= \infty
\end{aligned}
$$

于是 $\lim\limits_{n \to \infty}\frac{n^n}{n^!} = \infty$ ，则 $n! = o(n^n)$ 。

#### Problem 3 (教材习题 3.2-4)

函数 $\lceil\log n\rceil!$ 多项式有界吗？函数 $\lceil\log\log n\rceil!$ 多项式有界吗？

##### Solution

1. 函数 $\lceil\log n\rceil!$ 不是多项式有界的。

证明：反证法。假设 $\lceil\log n\rceil!$ 是多项式有界的，则存在常数 $c, a, n_0$ ，使得当 $n \ge n_0$ 时， $\lceil\log n\rceil! \le cn^a$ 恒成立。特别地，考虑 $n = 2^k, k\in\mathbb{N}$ 的情况，有  $\lceil k\rceil! \le c(2^a)^k$ ，这与阶乘并不是指数有界是矛盾的。

> 阶乘不是指数有界的这件事情可以通过问题2中类似的方式证明： $n! = \omega(a^n)$ 。

2. 函数 $\lceil\log\log n\rceil!$ 是多项式有界的。

证明：不是一般性，令 $n = 2^{2^k}$ ，则有

$$
\lceil\log\log n\rceil! = k! = \prod_{i = 1}^{k} i \le \prod_{i = 1}^{k} 2^{2^{i - 1}} = 2^{\sum\limits_{i = 1}^{k} 2^{i - 1}} = 2^{2^k - 1} \le 2^{2^k} = n
$$

于是， $\lceil\log\log n\rceil!$ 是多项式有界的。


#### Problem 4 (教材习题 3.2-5)

如下两个函数中，哪一个渐近更大些：$\log(\log^* n)$ 还是 $\log^*(\log n)$ ？

##### Solution

注意到 $\log^*(2^n) = 1 + \log^* n$ ，则：

$$
\begin{aligned}
\lim_{n\to\infty} \frac{\log(\log^* n)}{\log^*(\log n)} &= \lim_{n\to\infty} \frac{\log(\log^* (2^n))}{\log^*(\log (2^n))} (\text{换元：} n \to 2^n ) \\
&= \lim_{n\to\infty} \frac{\log(\log^*n + 1)}{\log^* n} \\
&= \lim_{n\to\infty} \frac{\log(n + 1)}{n} (\text{换元：} \log^* n \to n)
&= \lim_{n\to\infty} \frac{1}{n + 1} (\text{洛必达法则}) \\
&= 0
\end{aligned}
$$

从而 $\log(\log^* n) = o(\log^*(\log n))$ ， $\log^*(\log n)$ 渐近更大些。


#### Problem 5 (教材习题 3.2-8)

证明： $k\ln k = \Theta(n) \Rightarrow k = \Theta(n / \ln n)$ 。 

##### Solution

证明：下面的讨论都是在 $n$ 和 $k$ 充分大的情况下。

由 $k\ln k = \Theta(n)$ 有 $c_1 n \le k\ln k \le c_2 n$ 。

于是 $\frac{k\ln k}{c_2}\le n\le \frac{k\ln k}{c_1}$ ，

从而 $\ln k + \ln^{(2)} k - \ln c_2 \le \ln n \le \ln k + \ln^{(2)} k - \ln c_1$ 。

不难发现 $\ln n = \Theta(\ln k)$ ，不妨设 $c_3 \ln k \le \ln n \le c_4 \ln k$ ，于是

$$
\frac{\frac{k\ln k}{c_2}}{c_4 \ln k} \le \frac{n}{\ln n} \le \frac{\frac{k\ln k}{c_1}}{c_3 \ln k}
$$

即 $\frac{k}{c_2c_4} \le n / \ln n \le \frac{k}{c_1c_3}$ ，简单变形有：

$$
c_1c_3 (n /\ln n) \le k \le c_2c_4 (n / \ln n)
$$

因此 $k = \Theta(n / \ln n)$ 。

 
