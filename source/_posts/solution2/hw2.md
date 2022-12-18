---
title: 作业 2 解答
date: 2022-12-18 12:17:00
description: 第2讲函数的增长课后作业题答案
---

#### Problem 1 (教材习题 3-4)

**（渐近记号的性质）** 假设 $f(n)$ 和 $g(n)$ 为渐近正函数。证明或反驳下面的每个猜测。

1. $f(n) = O(g(n)) \Rightarrow g(n) = O(f(n))$ 。

2. $f(n) + g(n) = \Theta(\min(f(n), g(n)))$ 。

3. $f(n) = O(g(n))\Rightarrow \log(f(n)) = O(\log(g(n)))$ ，其中对所有足够大的 $n$ ，有 $\log(g(n)) \ge 1$ 且 $f(n) \ge 1$ 。

4. $f(n) = O(g(n)) \Rightarrow 2^{f(n)} = O(2^{g(n)})$ 。

5. $f(n) = O((f(n))^2)$ 。

6. $f(n) = O(g(n)) \Rightarrow g(n) = \Omega(f(n))$ 。

7. $f(n) = \Theta(f(n/2))$ 。

8. $f(n) + o(f(n)) = \Theta(f(n))$ 。

##### Solution

1. 假。反例： $n = O(n^2)$ 但 $n^2 \ne O(n)$ 。

2. 假。反例： $n + n^2 \ne \Theta(n)$ 。

3. 真。$f(n) = O(g(n)) \Rightarrow f(n) \le cg(n) \Rightarrow \log(f(n)) \le \log(cg(n)) = \log(g(n)) + \log(c) \Rightarrow \log(f(n)) = O(\log(g(n)))$ 。

4. 假。反例： $2n = O(n)$ ，但是 $2^{2n} = 4^n \ne O(2^n)$ 。

5. 假。反例： $\frac1n \ne O(\frac1{n^2})$ 。

6. 真。$f(n) = O(g(n)) \Rightarrow f(n) \le cg(n) \Rightarrow g(n) \ge \frac1cf(n) \Rightarrow g(n) = \Omega(f(n))$ 。

7. 假。反例： $4^n \ne \Theta(2^n) = \Theta(4^{n/2})$ 。

8. 真。

$$
\lim_{n \to \infty}\frac{f(n) + o(f(n))}{f(n)} = \lim_{n\to\infty} 1 + \frac{o(f(n))}{f(n)} = 1 + 0 = 1 \in (0, +\infty)
$$

所以 $f(n) + o(f(n)) = \Theta(f(n))$ 。

#### Problem 2 (教材习题 3-5)

**（ $O$ 与 $\Omega$ 的一些变形）** 某些作者用一种与我们稍微不同的方式来定义 $\Omega$ ：假设我们使用 $\stackrel{\infty}{\Omega}$ （读作“ $\Omega$ 无穷”）来表示这种可选的定义。若存在常量 $c$ ，使得对无穷多个整数 $n$ ，有 $f(n)\ge cg(n) \ge 0$ ，则称 $f(n) = \stackrel{\infty}{\Omega}(g(n))$ 。

1. 证明：对渐近非负的任意两个函数 $f(n)$ 和 $g(n)$ ，或者 $f(n) = O(g(n))$ 或者 $f(n) = \stackrel{\infty}{\Omega}(g(n))$ 或者二者均成立，然而，如果使用 $\Omega$ 来代替 $\stackrel{\infty}{\Omega}$ ，那么该命题并不为真。

2. 描述用 $\stackrel{\infty}{\Omega}$ 代替 $\Omega$ 来刻画程序运行时间的潜在优点与缺点。

某些作者也用一种稍微不同的方式来定义 $O$ ；假设使用 $O'$ 来表示这种可选的定义。我们称 $f(n) = O'(g(n))$ 当且仅当 $|f(n)| = O(g(n))$ 。

3. 如果使用 $O'$ 代替 $O$ 但仍然使用 $\Omega$ ，定理3.1（见[PPT第2讲第6页](/slides/lec02-growth-of-functions.pdf#page=6)或者教材3.1节）中的“当且仅当”的每个方向将出现什么情况？

有些作者定义 $\stackrel{\sim}{O}$ （读作“软O“）来意指忽略对数因子的 $O$ ：

$$
\stackrel{\sim}{O} = \{f(n) | \exists c > 0, k > 0, n_0 > 0, \forall n \ge n_0, 0 \le f(n) \le cg(n)\log^k(n)\}
$$

4. 用一种类似的方式定义 $\stackrel{\sim}{\Omega}$ 和 $\stackrel{\sim}{\Theta}$ 。证明与定理3.1（见[PPT第2讲第6页](/slides/lec02-growth-of-functions.pdf#page=10)或者教材3.1节）相对应的类似结论。

##### Solution

1. 反证法。假设存在两个函数 $f(n), g(n)$ ，$f(n) = O(g(n))$ 与 $f(n) = \stackrel{\infty}{\Omega}(g(n))$ 都不成立。

    - 由 $f(n) = O(g(n))$ 不成立可知，$\forall c > 0, n_0 > 0, \exists n \ge n_0, f(n) > cg(n)$ 。

    - 任取一个正常数 $c$ ，考虑 $n_0 = 1$ 的时候，即 $\exists n \ge n_0, f(n) > cg(n)$ 中对应的 $n$ 为 $a_1$ ；再考虑 $n_0 = a_1 + 1$ 的时候，记对应的 $n$ 为 $a_2$ 。

    - 更一般地，记 $n_0 = a_i + 1$ 时，使得 $f(n) > cg(n)$ 的 $n$ 的值为 $a_{i+1}$ ，于是我们得到了一个无限集 $\{a_1, a_2, a_3, \cdots\}$ ，对于这个无限集上的整数 $n$ ，均有 $f(n) > cg(n)$ 。

    - 于是有 $f(n) = \stackrel{\infty}{\Omega}(g(n))$ 成立，这与假设矛盾，故而原命题成立。

如果使用 $\Omega$ 来代替 $\stackrel{\infty}{\Omega}$ ，则命题为假，反例：取 $f(n) = n^{\sin n}$ ， $g(n) = n^{0.5}$ ， $f(n) = O(g(n))$ 与 $f(n) = \Omega(g(n))$ 均不成立。

2. 优点是我们得到了一个很漂亮的性质，任意两个函数都可以通过这个新的符号体系进行比较了；缺点是得到的结论不够“强”，对于这个无限集以外的世界一无所知。

    - $\stackrel{\infty}{\Omega}$ 所描述的比较关系时很暧昧的，意思是我有无限多的时刻比你大，但是并不是所有时刻，也就是说 $f(n)$ 和 $g(n)$ 在这样的比较标准下并没有完全区分开，有可能是相互纠缠的。
        
        - 比如说奇数的时候 $f(n)$ 大，偶数的时候 $g(n)$ 大，此时既可以说 $f(n) = \stackrel{\infty}{\Omega}(g(n))$ ，也可以说 $g(n) = \stackrel{\infty}{\Omega}(f(n))$ 。

3. 没有发生变化。因为一个函数能够使用 $\Theta$ 记号就已经蕴含着它在 $n$ 充分大的渐近意义下是非负的，而我们讨论渐近复杂度的时候又不关心 $n$ 不充分大的情况，所以给一个渐近意义下非负的东西加绝对值并不能在渐近意义下改变什么。

4. 定义 $\stackrel{\sim}{\Omega}$ 和 $\stackrel{\sim}{\Theta}$ 如下：

$$
\stackrel{\sim}{\Omega} = \{f(n) | \exists c > 0, k > 0, n_0 > 0, \forall n \ge n_0, 0 \le \frac{cg(n)}{\log^k(n)} \le f(n)\}
$$

$$
\stackrel{\sim}{\Theta} = \{f(n) | \exists c_1 > 0, c_2 > 0, k_1 > 0, k_2 > 0, n_0 > 0,\\
 \forall n \ge n_0, 0 \le \frac{c_1g(n)}{\log^{k_1}(n)} \le f(n) \le c_2g(n)\log^{k_2}(n)\}
$$

与定理3.1类似的结论为：$f(n) = \stackrel{\sim}{\Theta}(g(n)) \Leftrightarrow f(n) = \stackrel{\sim}{O}(g(n)) \wedge f(n) = \stackrel{\sim}{\Omega}(g(n))$ ，证明过程类似于[练习2-1](/solution2/exe2-1/)问题2。

