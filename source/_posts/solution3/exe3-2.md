---
title: 练习 3-2 解答
date: 2023-1-2 00:03:00
description: 递归式相关的习题解答
---

#### Problem 1 (教材 4.3 节习题节选)

1. 使用代入法证明 $T(n) = 4T(n/3) + n$ 的解为 $T(n) = \Theta(n^{\log_3 4})$ 。（提示：需要在假设中减去一个低阶项以完成归纳）

2. 利用换元法求解递归式 $T(n) = 3T(\sqrt{n}) + \log n$ 。你的解应该是渐近紧确的，不必担心数值是否是整数。

##### Solution

1. 先证上界。假设 $T(m) \le cm^{\log_34} - dm$ 对 $m < n$ 成立，则 

$$
T(n) \le 4(c(\frac{n}{3})^{\log_34} - d\frac{n}{3}) + n = cn^{\log_34} - (\frac{4d}{3} - 1)n \le cn^{\log_34} - dn
$$

其中，最后一步在 $d \ge 3$ 时成立。于是 $T(n) = O(n^{\log_34})$ 。

再证下界。假设 $T(m) \ge cm^{\log_34}$ 对 $m < n$ 成立，则 

$$
T(n) \ge 4c(\frac{n}{3})^{\log_34} + n = cn^{\log_34} + n \ge cn^{\log_34}
$$

于是，$T(n) = \Omega(n^{\log_34})$ ；综上， $T(n) = \Theta(n^{\log_34})$ 。

2. 令 $k = \log n$ ，则 $T(2^k) = 3T(2^{k/2}) + k$ 。

令 $S(k) = T(2^k)$ ，则 $S(k) = 3S(k/2) + k$ 。

不难得到 $S(k) = \Theta(k^{\log_23})$ ，从而 $T(n) = \Theta((\log n)^{\log_23})$ 。


#### Problem 2 (教材 4.4 节习题节选)

1. 对递归式 $T(n) = T(n - 1) + T(n/2) + n$ ，利用递归树确定一个好的渐近上界，用代入法进行验证。

2. 对递归式 $T(n) = T(\alpha n) + T((1-\alpha)n) + cn$ ，利用递归树给出一个渐近紧确界，其中 $0 < \alpha < 1$ 和 $c > 0$ 是常数。

##### Solution

1. $T(n) = O(2^n)$ 。

代入法验证：假设对于 $m < n$ 有 $T(m) \le 2^m$ ，则 $T(n) \le 2^{n-1} + 2^{n/2} + n \le 2^n$ ，最后一步在 $n$ 较大时成立。

为了说明 $2^n$ 是一个好的渐近上界，我们下面证明 $T(n)$ 并不是多项式有界的。

反证法。若存在 $c, k$ 使得 $T(m) \le cm^k + o(m^k)$ ，使用代入法，应该有

$$
T(n) \le c(n-1)^k + c(\frac{n}{2})^k + n = c(1 + \frac{1}{2^k})n^k + o(n^k) \le cn^k + o(n^k)
$$

而 $c(1 + \frac{1}{2^k})n^k \le cn^k$ 是不可能成立的，因此不存在这样的 $c, k$ ，从而 $T(n)$ 不是多项式有界的。

2. 两个子问题的规模之和为 $\alpha n + (1-\alpha)n = n$ ，这和归并排序是类似的，画递归树也能够看出这一点。于是，可以猜测 $T(n) = \Theta(n\log n)$ 。

先证下界。假设对 $m < n$ 有 $T(m) \ge c_1m\log m$ ，则

$$
\begin{aligned}
T(n) &\ge c_1\alpha n\log(\alpha n) + c_1(1-\alpha)n\log((1-\alpha)n) + cn \\
&= c_1n\log n + n[c + c_1(\alpha\log\alpha + (1-\alpha)\log(1-\alpha))]\\
&\ge c_1n\log n
\end{aligned}
$$

其中，最后一步需要 $c_1 \le \frac{-c}{\alpha\log\alpha + (1-\alpha)\log(1-\alpha)}$ 。于是 $T(n) = \Omega(n\log n)$ 。

再证上界。假设对 $m < n$ 有 $T(m) \le c_2m\log m$ ，则

$$
\begin{aligned}
T(n) &\le c_2\alpha n\log(\alpha n) + c_2(1-\alpha)n\log((1-\alpha)n) + cn \\
&= c_2n\log n + n[c + c_2(\alpha\log\alpha + (1-\alpha)\log(1-\alpha))]\\
&\le c_2n\log n 
\end{aligned}
$$

其中，最后一步需要 $c_2 \ge \frac{-c}{\alpha\log\alpha + (1-\alpha)\log(1-\alpha)}$ 。于是 $T(n) = O(n\log n)$ 。

综上， $T(n) = \Theta(n\log n)$ ，这是一个渐近紧确界。


#### Problem 3 (教材习题 4.5-1)

对下列递归式，使用主方法求出渐近紧确界。

1. $T(n) = 2T(n/4) + 1$

2. $T(n) = 2T(n/4) + \sqrt{n}$

3. $T(n) = 2T(n/4) + n$

4. $T(n) = 2T(n/4) + n^2$

##### Solution

1. 主定理情况 1 ， $T(n) = \Theta(\sqrt{n})$ 。

2. 主定理情况 2 ， $T(n) = \Theta(\sqrt{n}\log n)$ 。

3. 主定理情况 3 ， $T(n) = \Theta(n)$ 。

4. 主定理情况 3 ， $T(n) = \Theta(n^2)$ 。


#### Problem 4 (教材习题 4.5-2)

熊教授想设计一个渐近快于 Strassen 算法的矩阵相乘算法。他的算法使用分治方法，将每个矩阵分解为 $n/4 \times n/4$ 的子矩阵，分解和合并步骤共花费 $\Theta(n^2)$ 时间。他需要确定，他的算法需要创建多少个子问题，才能击败 Strassen 算法。如果他的算法创建 $a$ 个子问题，则描述运行时间 $T(n)$ 的递归式为 $T(n) = aT(n/4) + \Theta(n^2)$ 。 熊教授的算法如果要渐近快于 Strassen 算法， $a$ 的最大整数值应是多少？

##### Solution

Strassen 算法的复杂度为 $\Theta(n^{\log_27})$ 。因为要求 $a$ 的最大值，考虑 $a > 16$ 的情况，用主方法可求得熊教授算法的复杂度为 $\Theta(n^{\log_4a})$ 。如果熊教授的算法要渐近快于 Strassen ，那么需要 $\log_4a < \log_27$ ，解得 $a < 49$ ，于是 $a$ 的最大整数值为 $48$ 。


#### Problem 5 (教材习题 4.5-5)

考虑主定理情况 3 的一部分：对某个常数 $c < 1$ ，正则条件 $af(n/b) \le cf(n)$ 是否成立。给出一个例子，其中常数 $a \ge 1, b > 1$ 且函数 $f(n)$ 满足主定理情况 3 中除正则条件外的所有条件。

##### Solution

考虑 $T(n) = T(n/3) + f(n)$ ，其中 

$$
f(n) = \begin{cases}
3n + 2^{3n}, &\text{if } n = 2^i, i\in\mathbb{N}\\
3n, &\text{otherwise}
\end{cases}
$$

满足 $f(n) = \Omega(n^{\log_31+\varepsilon}) = \Omega(n^{\varepsilon})$ 的条件，但是不满足正则条件 $f(n/3) \le cf(n), c<1$ 。

取 $n = 3\cdot 2^{i}, i\in\mathbb{N}$ ，有

$$
f(n/3) = n + 2^n > 3n = f(n)
$$

是不满足正则条件的反例。


#### Problem 6 (教材习题 4.6-2)

证明：如果 $f(n) = \Theta(n^{\log_b a}\log^k n)$ ，其中 $k \ge 0$ ，那么主递归式的解为 $T(n) = \Theta(n^{\log_b a}\log^{k+1} n)$ 。为简单起见，假定 $n$ 是 $b$ 的幂。

##### Solution

证明：根据引理4.2（见[第3讲PPT第44页](/slides/lec03-divide-and-conquer.pdf#page=44)，教材4.6节），有

$$
T(n) = \Theta(n^{\log_ba}) + \sum_{j = 0}^{\log_bn-1}a^jf(n/b^j)
$$

考虑和式

$$
g(n) = \sum_{j = 0}^{\log_bn-1}a^jf(n/b^j)
$$

由 $f(n) = \Theta(n^{\log_b a}\log^k n)$ 有 

$$
f(n/b^j) = \Theta((n/b^j)^{\log_b a}\log^k(n/b^j)) = \Theta((n^{\log_b a} / a^j)(\log b\log_b(n/b^j))^k)
$$

于是

$$
a^jf(n/b^j) = \Theta(n^{\log_b a}\log^kb\log_b^k(n/b^j)) = \Theta(n^{\log_b a}(\log_b(n) - j)^k) = \Theta(n^{\log_b a}\log^k_b(n))
$$

其中，最后一步用到了 $j < \log_b(n)$ 。

继而

$$
\begin{aligned}
g(n) &= \sum_{j = 0}^{\log_bn-1}a^jf(n/b^j) = \Theta(\sum_{j = 0}^{\log_bn-1} n^{\log_b a}\log^k_b(n))\\
&= \Theta(n^{\log_b a}\log^{k+1}_b(n)) = \Theta(n^{\log_b a}\log^{k+1}(n))
\end{aligned}
$$

所以， $T(n) = \Theta(n^{\log_b a}\log^{k+1} n)$ 。


#### Problem 7 (教材习题 4.6-3)

证明：主定理中的情况 3 被过分强调了，从某种意义上来说，对于某个常数 $c < 1$ ，正则条件 $af(n/b) \le cf(n)$ 成立本身就意味着存在常数 $\varepsilon > 0$ ，使得 $f(n) = \Omega(n^{\log_b a + \varepsilon})$ 。

##### Solution

证明：根据正则条件，不断迭代，有

$$
f(n)\ge \frac{a}{c} f(\frac{n}{b}) \ge (\frac{a}{c})^2 f(\frac{n}{b^2}) \ge \cdots \ge (\frac{a}{c})^i f(\frac{n}{b^i}) \ge \cdots \ge (\frac{a}{c})^{\log_bn} f(1)
$$

则 $f(n) = \Omega((a/c)^{\log_bn}) = \Omega(n^{\log_b(a/c)}) = \Omega(n^{\log_ba + \log_b(1/c)})$ 。

取 $\varepsilon = \log_b(1/c) > 0, c<1$ ，则 $f(n) = \Omega(n^{\log_b a + \varepsilon})$ 。

