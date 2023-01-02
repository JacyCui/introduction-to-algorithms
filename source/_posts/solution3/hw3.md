---
title: 作业 3 解答
date: 2023-1-2 01:07:00
description: 第3讲分治策略课后作业题解答
---

#### Problem 1 (教材习题 4-3)

**（更多的递归式例子）** 对下列每个递归式，给出 $T(n)$ 的渐近上界和下界。假定对足够小的 $n$ ， $T(n)$ 是常数。给出尽量紧确的界，并验证其正确性。

1. $T(n) = 4T(n/3) + n\log n$

2. $T(n) = 3T(n/3) + n / \log n$

3. $T(n) = 4T(n/2) + n^2\sqrt{n}$

4. $T(n) = 3T(n/3 - 1) + n/2$

5. $T(n) = 2T(n/2) + n/\log n$

6. $T(n) = T(n/2) + T(n/4) + T(n/8) + n$

7. $T(n) = T(n - 1) + 1/n$

8. $T(n) = T(n - 1) + \log n$

9. $T(n) = T(n - 2) + 1/\log n$

10. $T(n) = \sqrt{n} T(\sqrt{n}) + n$

##### Solution

1. 主定理情况 1 ， $T(n) = \Theta(n^{\log_3 4})$ 。

2. $T(n) = \stackrel{\sim}{\Theta}(n)$ ，$\stackrel{\sim}{\Theta}$ 定义见[作业2](/solution2/hw2/)问题2。

首先，用代入法证明 $T(n) \le cn\log n$ 。

假设 $T(m) \le cm\log m$ 对于 $m < n$ 成立，则

$$
T(n) \le 3c\frac{n}{3}\log(n/3) + \frac{n}{\log n} = cn\log n + (\frac{1}{\log n} - c\log 3)n \le cn\log n
$$

最后一步需要 $c \ge 1 /\log 3$ 。

再用代入法证明，对于任意 $\varepsilon > 0$ ， $T(n) \ge cn^{1-\varepsilon}$ 。

假设 $T(m) \ge cm^{1-\varepsilon}$ 对于 $m < n$ 成立，则

$$
T(n) \ge 3c(\frac{n}{3})^{1-\varepsilon} + \frac{n}{\log n} \ge 3^{\varepsilon}cn^{1-\varepsilon} + \frac{n}{dn^{\varepsilon}} = (3^{\varepsilon}c + \frac{1}{d}) n^{1-\varepsilon} \ge cn^{1-\varepsilon}
$$

倒数第 3 步用的是 $\log n = o(n^\varepsilon)$ （见课本3.2节）；最后一步取 $d \le 1/c$ 即可。

综上： $T(n) = \stackrel{\sim}{\Theta}(n)$ 。

3. 主定理情况 3 ， $T(n) = \Theta(n^2\sqrt{n})$ 。

4. $T(n) = \Theta(n\log n)$ ，根据主定理情况 2 猜测，使用代入法证明。

5. 和第 2 问类似， $T(n) = O(n\log n)$ 且 $T(n) = \Omega(n^{1-\varepsilon})$ ，即 $T(n) = \stackrel{\sim}{\Theta}(n)$ 。

6. $T(n) = \Theta(n)$ ，用代入法即可证明。

7. 不妨 $T(1) = 1$ ，则

$$
T(n) = \sum_{i = 1}^{n} \frac{1}{i} \le 1 + \int_{1}^{n}\frac{1}{x}dx = 1 + \ln n
$$

$$
T(n) = \sum_{i = 1}^{n} \frac{1}{i} \ge \int_{1}^{n+1}\frac{1}{x}dx = \ln(n+1)
$$

于是 $T(n) = \Theta(\log n)$ 。

8. 不妨 $T(1) = 1$ ，则

$$
T(n) = 1 + \sum_{i = 1}^{n} \log i = 1 + \log(n!) = \Theta(n\log n)
$$

最后一步回忆[练习2-2](/solution2/exe2-2/)问题2。

9. 和前面两问类似，不难理解

$$
T(n) = \Theta(\int_{0}^{n} \frac{1}{log n}) = \Theta(li(n)) = \Theta(\frac{n}{\log n})
$$

其中， $li(n)$ 是[对数积分函数](https://en.wikipedia.org/wiki/Logarithmic_integral_function)。

10. 换元法。令 $n = 2^k$ ，有

$$
T(2^k) = 2^{k/2}T(2^{k/2}) + 2^k \Leftrightarrow
\frac{T(2^k)}{2^k} = \frac{T(2^{k/2})}{2^{k/2}} + 1
$$

$$
\Leftrightarrow \frac{T(2^k)}{2^k} = \Theta(\log k) \Leftrightarrow T(2^k) = \Theta(2^k\log k)
$$

于是不难得到， $T(n) = \Theta(n\log\log n)$ 。


#### Problem 2 (教材习题 4-4)

**（佩波那契数）** 本题讨论递归式 $F_0 = 0, F_1 = 1, F_i = F_{i-1} + F_{i-2}, i\ge 2$ 定义的佩波那契数的性质。我们将使用生成函数技术来求解佩波那契递归式。 **生成函数**（又称为 **形式幂级数** ）$\mathfrak{F}$ 定义为

$$
\mathfrak{F}(z) = \sum_{i = 0}^{\infty} F_i z^i = 0 + z + z^2 + 2z^3 + 3z^4 + 5z^5 + 8z^6 + 13z^7 + 21z^8 + ...
$$

其中 $F_i$ 为第 $i$ 个佩波那契数。

1. 证明：$\mathfrak{F}(z) = z + z\mathfrak{F}(z) + z^2\mathfrak{F}(z)$ 。

2. 证明：

$$
\mathfrak{F}(z) = \frac{z}{1 - z - z^2} = \frac{z}{(1 - \phi z)(1 - \hat{\phi} z)}
= \frac{1}{\sqrt{5}}(\frac{1}{1 - \phi z} - \frac{1}{1 - \hat{\phi} z})
$$

其中

$$
\phi = \frac{1 + \sqrt{5}}{2} = 1.61803\cdots, \hat{\phi} = \frac{1 - \sqrt{5}}{2} = -0.61803\cdots
$$

3. 证明：

$$
\mathfrak{F}(z) = \sum_{i = 0}^{\infty} \frac{1}{\sqrt{5}}(\phi^i - \hat{\phi}^i)z^i
$$

4. 利用上述结果证明： 对 $i > 0, F_i = \frac{\phi^i}{\sqrt{5}}$ ，结果舍入到最接近的整数。（提示：观察到 $|\hat{\phi}| < 1$ 。）

##### Solution

1. 证明：从右往左化简，利用递归式 $F_{i-1} + F_{i-2} = F_{i}$ 。

$$
\begin{aligned}
z + z \mathfrak{F}(z) + z^2 \mathfrak{F}(z) &=z + z \sum_{i = 0}^{\infty} F_i z^i + z^2 \sum_{i = 0}^{\infty} F_i z^i\\
&=z + \sum_{i = 1}^{\infty} F_{i - 1} z^i + \sum_{i = 2}^{\infty} F_{i - 2} z^i\\
&= 0 + z + \sum_{i = 2}^{\infty} (F_{i-1} + F_{i-2}) z^i\\
&= \sum_{i = 0}^{\infty} F_i z^i\\
&= \mathfrak{F}(z)
\end{aligned}
$$

2. 证明：基于第1问，从两边往中间化简。

$$
\mathfrak{F}(z) = z + z\mathfrak{F}(z) + z^2\mathfrak{F}(z) \Leftrightarrow
\mathfrak{F}(z) = \frac{z}{1 - z - z^2}
$$

$$
\frac{1}{\sqrt{5}} (\frac{1}{1 - \phi z} - \frac{1}{1 - \hat{\phi} z}) = \frac{(\phi - \hat{\phi})z}{\sqrt{5} (1 - \phi z)(1-\hat{\phi} z)}
$$

其中，$\phi + \hat{\phi} = 1, \phi - \hat{\phi} = \sqrt{5}, \phi\hat{\phi} = -1$ 。

于是

$$
\begin{aligned}
\frac{1}{\sqrt{5}}(\frac{1}{1 - \phi z} - \frac{1}{1 - \hat{\phi} z})
&=\frac{z}{(1 - \phi z)(1 - \hat{\phi} z)}\\
&=\frac{z}{1 - (\phi + \hat{\phi})z + \phi\hat{\phi}z^2}\\
&=\frac{z}{1 - z - z^2}\\
&=\mathfrak{F}(z)
\end{aligned}
$$

3. 证明：考虑几何级数，有

$$
\sum_{i=0}^{\infty} x^i = \frac{1}{1-x}
$$

于是

$$
\begin{aligned}
\sum_{i=0}^{\infty}\frac{1}{\sqrt{5}}(\phi^i - \hat{\phi}^i)z^i
&= \frac{1}{\sqrt{5}}(\sum_{i=0}^{\infty}(\phi z)^i - \sum_{i=0}^{\infty}(\hat{\phi} z)^i)\\
&= \frac{1}{\sqrt{5}}(\frac{1}{1 - \phi z} - \frac{1}{1 - \hat{\phi} z})\\
&= \mathfrak{F}(z)
\end{aligned}
$$

4. 证明：根据 $\mathfrak{F}(z)$ 的定义及第 3 问结论，

$$
\mathfrak{F}(z) = \sum_{i = 0}^{\infty} F_i z^i = \sum_{i=0}^{\infty}\frac{1}{\sqrt{5}}(\phi^i - \hat{\phi}^i)z^i
$$

于是 $F_i = (\phi^i - \hat{\phi}^i)/\sqrt{5}$ 。观察到 $|\hat{\phi}| < 1$ ，则 $|\hat{\phi} / \sqrt{5}| < 0.5$ 。于是，在就近舍入的意义下，$F_i = \phi^i/\sqrt{5}$ 。


#### Problem 3 (教材习题 4-5)

**（芯片检测）** 熊教授有 $n$ 片可能完全一样的集成电路芯片，原理上可以用来相互检测。教授的测试夹具同时只能容纳两块芯片。当夹具装载上时，每块芯片都检测另一块，并报告它是好是坏。一块好的芯片总能准确报告另一块芯片的好坏，但教授不能信任坏芯片报告的结果。因此，4种可能的测试结果如下：

|芯片A的结果|芯片B的结果|结论|
|:-:|:-:|:-:|
|B是好的|A是好的|两片都是好的，或都是坏的|
|B是好的|A是坏的|至少一块是坏的|
|B是坏的|A是好的|至少一块是坏的|
|B是坏的|A是坏的|至少一块是坏的|

1. 证明：如果超过 $n/2$ 块芯片是坏的，使用任何基于这种逐对检测操作的策略，教授都不能确定哪些芯片是好的。假定坏芯片可以合谋欺骗教授。

2. 考虑从 $n$ 块芯片中寻找一块好芯片的问题，假定超过 $n/2$ 块芯片是好的。证明：进行 $\lfloor n/2\rfloor$ 次逐对检测足以将问题规模减半。

3. 假定超过 $n / 2$ 块芯片是好的，证明：可以用 $\Theta(n)$ 次逐对检测找出好的芯片。给出描述检测次数的递归式，并求解它。

##### Solution

1. 证明：记好芯片的数量为 $g < n/2$ ，则坏芯片的数量 $n - g > g$ 。

考虑所有好芯片的集合 $G$ ，一定存在一个坏芯片的集合 $B$ ，满足 $|B| = |G|$ ，因为坏芯片的数量是比好芯片多的。下面证明我们无论如何都不能区分 $G$ 和 $B$ 中的芯片。

给出 $B$ 中坏芯片的合谋策略：如果被比较的芯片是 $B$ 中的，则报告好芯片；如果被比较的芯片是 $G$ 中的，则报告坏芯片。

于是， $G$ 和 $B$ 中的芯片就都说自己集合里面的是好芯片，对方集合里面的是坏芯片了。从而，无论怎么测试，对于 $G$ 和 $B$ 中的每个芯片都有 $g - 1$ 个芯片认为它是好的；都有 $g$ 个芯片认为它是坏的，因此大家的评价结果都一样，无法区分。

2. 证明：下面给出一个通过 $\lfloor n/2\rfloor$ 次检测将问题规模减半的算法。

- 逐对检测所有的芯片，共 $\lfloor n/2\rfloor$ 次检测；如果芯片总数是奇数，则随便将一块芯片放在一旁，最后再放进来即可。

    - 如果检测结果表明其中至少一块是坏的，则将这两块芯片都扔掉；

    - 否则，扔掉两块中的任意一块。

上述算法显然使得规模减半了，下面证明剩下的芯片依旧满足好的芯片比坏的芯片多这个性质，从而我们得到了一个规模减半的子问题。

原本是好芯片比坏芯片多的，在上述算法中我们进行的两种操作下：

- 第一种操作：如果检测结果表明其中至少一块是坏的，则将这两块芯片都扔掉；

    - 我们要么同时扔掉两个坏芯片，要么扔掉了一个坏芯片和一个好芯片，这两种情况都没有破坏“好芯片比坏芯片多”的性质。

- 第二种操作：如果检测结果表明要么是两个好芯片，要么是两个坏芯片，则随便扔掉一块；

    - 因为剩下的要么都是好的，要么都是坏的，所有检测对都随便扔掉一个，相当于好芯片和坏芯片都变成原来的一半，也没有破坏“好芯片比坏芯片多”的性质。

- 最后对奇数的情况补充一些接受，奇数个芯片，将一个芯片放在一旁之后：

    - 如果这是一个坏芯片，那么剩下的芯片一定是好的多，且好的比坏的至少多2个（否则和不是偶数），最后放回来还是好的多；

    - 如果这是一个好芯片，那么剩下的芯片好的不少于坏的，最后放回来，还是好的多。

综上，我们可以通过 $\lfloor n/2\rfloor$ 次检测将问题规模减半。

3. 证明：先给出一个找出一个好芯片的算法。

- 基础情况：$n = 1, 2$ 时，一定都是好芯片，直接返回即可（因为好芯片要比坏芯片多）；

- 递归情况：不断地重复问题 2 中的折半算法，直到问题规模缩小到 $1$ 或者 $2$ 为止。

该算法的递归式为 $T(n) \le T(n/2) + \lfloor n/2\rfloor$ ，根据主定理的情况 3 不难得出 $T(n) = O(n)$ 。

根据找到的这一个好的芯片和所有其他芯片比对，可以找出所有的好芯片，需要 $\Theta(n)$ 次逐对检测。

所以，可以用 $O(n) + \Theta(n) = \Theta(n)$ 次逐对检测找出所有的好芯片。


#### Problem 4 (教材习题 4-6)

**（Monge 阵列）** 对一个 $m\times n$ 的实数阵列 $A$ ，若对所有满足 $1 \le i < k \le m$ 和 $1 \le j < l \le n$ 的 $i, j, k, l$ 有

$$
A[i, j] + A[k, l] \le A[i, l] + A[k, j]
$$

则称 $A$ 是 **Monge 阵列** （Monge Array）。换句话说，无论何时选出 $Monge$ 阵列的两行和两列，对于交叉点上的 $4$ 个元素，左上和右下两个元素之和总是小于等于左下和右上元素之和。例如，下面就是一个 Monge 阵列：

$$
\begin{array}{rrrrr}
10 & 17 & 13 & 28 & 23\\
17 & 22 & 16 & 29 & 23\\
24 & 28 & 22 & 34 & 24\\
11 & 13 & 6 & 17 & 7\\
45 & 44 & 32 & 37 & 23\\
36 & 33 & 19 & 21 & 6\\
75 & 66 & 51 & 53 & 34\\
\end{array}
$$

1. 证明：一个数组是 Monge 阵列当且仅当对所有 $i = 1, 2, ..., m - 1$ 和 $j = 1, 2, ..., n - 1$ ，有

$$
A[i, j] + A[i + 1, j + 1] \le A[i, j + 1] + A[i + 1, j]
$$

（提示：对于“当”的部分，分别对行和列使用归纳法。）

2. 下面数组不是 Monge 阵列。改变一个元素使其变成 Monge 阵列。（提示：利用第 1 问的结果。）

$$
\begin{array}{rrrr}
37 & 23 & 22 & 32\\
21 & 6 & 7 & 10\\
53 & 34 & 30 & 31\\
32 & 13 & 9 & 6\\
43 & 21 & 15 & 8\\
\end{array}
$$

3. 令 $f(i)$ 表示第 $i$ 行的最左最小元素的列下标。证明：对任意 $m \times n$ 的 Monge 阵列， $f(1) \le f(2) \le ... \le f(m)$ 。

4. 下面是一个计算 $m \times n$ 的 Monge 阵列 $A$ 每一行最左最小元素的分治算法的描述：

> 提取 $A$ 的偶数行构造其子矩阵 $A'$ 。递归地确定 $A'$ 每行的最左最小元素。然后计算 $A$ 的奇数行的最左最小元素。

解释如何在 $O(m + n)$ 时间内计算 $A$ 的奇数行的最左最小元素（在偶数行的最左最小元素已知的情况下）。

5. 给出第 4 问中描述的算法的运行时间的递归式。证明其解为 $O(m + n\log m)$ 。

##### Solution

1. 证明：充分性显然，取 $k = i + 1, l = j + 1$ 即可。下面证明必要性。

分别对行和列进行归纳以拓展 $A[i, j] + A[i + 1, j + 1] \le A[i, j + 1] + A[i + 1, j]$ 。

固定 $i$ 和 $j$ ，先进行行拓展，证明： $A[i, j] + A[i + r, j + 1] \le A[i, j + 1] + A[i + r, j]$ 。

- 基础情况： $r = 1$ 时显然成立。

- 归纳假设：假设 $A[i, j] + A[i + r, j + 1] \le A[i, j + 1] + A[i + r, j]$ 。

- 归纳步骤：下面证明 $A[i, j] + A[i + r + 1, j + 1] \le A[i, j + 1] + A[i + r + 1, j]$

$$
\begin{aligned}
&\quad A[i, j] + A[i + r + 1, j + 1]\\
&= (A[i, j] + A[i + r, j + 1]) + (A[i + r, j] + A[i + r + 1, j + 1])\\
&\quad\quad\quad - A[i + r, j + 1] - A[i + r, j]\\
&\le (A[i, j + 1] + A[i + r, j]) + (A[i + r, j + 1] + A[i + r + 1, j])\\
&\quad\quad\quad - A[i + r, j + 1] - A[i + r, j]\\
&= A[i, j + 1] + A[i + r + 1, j]
\end{aligned}
$$

固定 $i$ ，$j$ 和 $k$ ，再进行列拓展，证明： $A[i, j] + A[i + r, j + c] \le A[i, j + c] + A[i + r, j]$ 。

- 基础情况： $c = 1$ 时已经证毕，显然成立。

- 归纳假设：假设 $A[i, j] + A[i + r, j + c] \le A[i, j + c] + A[i + r, j]$ 。

- 归纳步骤：下面证明 $A[i, j] + A[i + r, j + c + 1] \le A[i, j + c + 1] + A[i + r, j]$

$$
\begin{aligned}
&\quad A[i, j] + A[i + r, j + c + 1]\\
&= (A[i, j] + A[i + r, j + c]) + (A[i, j + c] + A[i + r, j + c + 1])\\
&\quad\quad\quad - A[i + r, j + c] - A[i, j + c]\\
&\le (A[i, j + c] + A[i + r, j]) + (A[i + r, j + c] + A[i, j + c + 1])\\
&\quad\quad\quad - A[i + r, j + c] - A[i, j + c]\\
&= A[i, j + c + 1] + A[i + r, j]
\end{aligned}
$$

综上，我们证明了 $A[i, j] + A[i + r, j + c] \le A[i, j + c] + A[i + r, j]$ ，令 $k = i + r, l = j + c$ ，即证明了 $A[i, j] + A[k, l] \le A[i, l] + A[k, j]$ 。必要性得证。

2. 将第 2 行第 3 列的 7 改成 5。

3. 证明：反证法。若存在 $f(i) > f(i+1)$ ，令 $k = f(i), j = f(i + 1)$ ，有 $j < k$ 。

由于 $f(i)$ 表示的是第 $i$ 行最左最小元素的列下标，我们有 $A[i, j] > A[i, k], A[i + 1, k] > A[i + 1, j]$ ，于是 $A[i, j] + A[i + 1, k] > A[i, k] + A[i + 1, j]$ ，与 Monge 阵列定义矛盾。

4. 以 $m$ 是奇数为例说明， $m$ 是偶数的情况也是类似的。

线性扫描 $A[i, f(i - 1)..f(i+1)]$ 取最小值即可得到 $f(i)$ ，需要访问数组 $A$ $f(i + 1) - f(i - 1) + 1$ 次，其中 $i = 1, 3, 5, 7, ...$ 。

记 $f(0) = 1$ 表示第一行从最左边开始扫描， $f(m + 1) = n$ 表示最后一行一直扫描到最后。于是，总的访问次数为：

$$
\sum_{i = 1, 3, 5, 7, ..., m} f(i + 1) - f(i - 1) + 1 = f(m + 1) - f(0) + \frac{m}{2} \\
= n + \frac{m}{2} - 1 = O(m + n)
$$

所以上述扫描行为的运行时间为 $O(m + n)$ 。

5. 第 4 问中的算法对应的递归式为 $T(m, n) = T(m/2, n) + c(m+n)$ ，下面用代入法证明 $T(m, n) = O(m + n\log m)$ 。

假设 $T(m, n) \le d(m + n\log m)$ 对于较小的 $m$ 成立，则

$$
T(m, n) \le d(m/2 + n\log(m/2)) + c(m + n)\\
= (c + d/2)m + dn\log m + (c - d)n \le d(m + n\log m)
$$

其中，最后一步需要 $c \le d/2$。 $T(m, n) = O(m + n\log m)$ 证毕。

