---
title: 练习 2-1 解答
date: 2022-12-17 21:17:00
description: 渐近记号相关的习题解答
---

#### Problem 1 (教材习题 3.1-1)

假设 $f(n)$ 与 $g(n)$ 都是渐近非负函数。使用 $\Theta$ 记号的基本定义来证明

$$
\max(f(n), g(n)) = \Theta(f(n) + g(n))
$$

##### Solution

$$
\max(f(n), g(n)) = \frac{f(n) + g(n)}2 + \frac{|f(n) - g(n)|}2 \ge \frac12(f(n) + g(n))
$$

且显然有 

$$
\max(f(n), g(n)) \le f(n) + g(n)
$$

所以 $\max(f(n), g(n)) = \Theta(f(n) + g(n))$ 。

#### Problem 2 (教材习题 3.1-5)

证明定理3.1（见[第2讲PPT第6页](/slides/lec02-growth-of-functions.pdf#page=6)或者教材3.1节）。

##### Solution

证明：先证充分性。由 $f(n) = \Theta(g(n))$ ，有

$$
\exists c_1 > 0, c_2 > 0, n_0 > 0, \forall n \ge n_0, 0 \le c_1g(n) \le f(n) \le c_2g(n)
$$

从而有 $\exists c_2 > 0, n_0 > 0, \forall n \ge n_0, 0 \le f(n) \le c_2g(n)$ ，即 $f(n) = O(g(n))$ ；

且 $\exists c_1 > 0, n_0 > 0, \forall n \ge n_0, 0 \le c_1g(n) \le f(n)$ ，即 $f(n) = \Omega(g(n))$ 。

再证必要性。

由 $f(n) = \Omega(g(n))$ 有 $\exists c_1 > 0, n_1 > 0, \forall n \ge n_1, 0 \le c_1g(n) \le f(n)$ 。

由 $f(n) = O(g(n))$ 有 $\exists c_2 > 0, n_2 > 0, \forall n \ge n_2, 0 \le f(n) \le c_2g(n)$ 。

取 $n_0 = \max(n_1, n_2) > 0$ ，则

$$
\exists c_1 > 0, c_2 > 0, n_0 > 0, \forall n \ge n_0, 0 \le c_1g(n) \le f(n) \le c_2g(n)
$$

从而 $f(n) = \Theta(g(n))$ 。

#### Problem 3 (教材习题 3.1-7)

证明： $o(g(n)) \cap \omega(g(n))$ 为空集。

##### Solution

证明：反证法，假设存在 $f(n)$ ， $f(n) \in o(g(n)) \cap \omega(g(n))$ ，则

$$
f(n) \in o(g(n)) \Rightarrow \lim_{n\to\infty} \frac{f(n)}{g(n)} = 0
$$

$$
f(n) \in \omega(g(n)) \Rightarrow \lim_{n\to\infty} \frac{f(n)}{g(n)} = \infty
$$

从而 $0 = \infty$ ，矛盾。所以不存在这样的 $f(n)$ ，即 $o(g(n)) \cap \omega(g(n))$ 为空集。

#### Problem 4 (教材习题 3.1-8)

可以扩展我们的记号到有两个参数 $n$ 和 $m$ 的情形，其中的 $n$ 和 $m$ 可以按不同速率独立地趋于无穷。对于给定的函数 $g(n, m)$ ，用 $O(g(n, m))$ 来表示以下函数集：

$$
O(g(n, m)) = \{f(n, m) | \exists c > 0, n_0 > 0 , m_0 > 0, \\
\forall n \ge n_0 \vee m \ge m_0, 0\le f(n, m) \le cg(n, m)\}
$$

对 $\Omega(g(n, m))$ 和 $\Theta(g(n, m))$ 给出相应的定义。

##### Solution

$$
\Omega(g(n, m)) = \{f(n, m) | \exists c > 0, n_0 > 0 , m_0 > 0, \\
\forall n \ge n_0 \vee m \ge m_0, 0\le cg(n, m) \le f(n, m) \}
$$

$$
\Theta(g(n, m)) = \{f(n, m) | \exists c_1 > 0, c_2 > 0, n_0 > 0 , m_0 > 0, \\
\forall n \ge n_0 \vee m \ge m_0, 0\le c_1g(n, m) \le f(n, m) \le c_2g(n, m)\}
$$



