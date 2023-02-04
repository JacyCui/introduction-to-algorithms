---
title: 作业 8 解答
date: 2023-2-4 12:37:00
description: 中位数和顺序统计量课后作业题解答
---

#### Problem 1 (教材习题 9-1)

**（有序序列中的 $i$ 个最大数）** 给定一个包含 $n$ 个元素的集合，我们希望利用基于比较的算法找出按顺序排列的前 $i$ 个最大元素。请设计能实现下列每一项要求，并且具有最佳渐近最坏情况运行时间的算法，以 $n$ 和 $i$ 来表示算法的运行时间：

1. 对输入数据排序，并找出前 $i$ 个最大数；

2. 对输入数据建立一个最大优先队列，并调用 EXTRACT-MAX 过程 $i$ 次。

3. 利用一个顺序统计量算法来找到第 $i$ 大的元素，然后用它作为主元划分输入数组，再对前 $i$ 大的数排序。

##### Solution

1. 排序需要 $O(n\log n)$ ，列出其中前 $i$ 大的数需要 $O(i)$ ，总时间为 $O(n\log n + i)$ 。

2. 使用最大堆来建立最大优先队列需要 $O(n)$ 的时间，每次 EXTRACT-MAX 需要 $O(\log n)$ 的时间，共调用 $i$ 次，总时间为 $O(n + i\log n)$ 。

3. 通过 SELECT 算法（详见[第8讲PPT第14页](/slides/lec08-medians-and-order-statistics.pdf#page=14)）找到第 $i$ 大的元素并依此划分数组需要 $O(n)$ ，对前 $i$ 大的元素进行排序需要 $O(i\log i)$ ，总时间为 $O(n + i\log i)$ 。


#### Problem 2 (教材习题 9-2)

**（带权中位数）** 对分别具有正权重 $w_1, w_2, \cdots, w_n$ ，且满足 $\sum\limits_{i=1}^{n} w_i = 1$ 的 $n$ 个互异元素 $x_1, x_2, \cdots , x_n$ 来说，带权中位数 $x_k$ （较小中位数）是满足如下条件的元素：

$$
\sum_{x_i < x_k} w_i < \frac{1}{2}
$$

和

$$
\sum_{x_i > x_k} w_i \le \frac{1}{2}
$$

例如，如果元素是 $0.1, 0.35, 0.05, 0.1, 0.15, 0.05, 0.2$ ，并且每个元素的权重等于本身（即对所有 $i = 1, 2, \cdots, 7$ ，都有 $w_i = x_i$），那么中位数是 $0.1$ ，而带权中位数是 $0.2$ 。

1. 证明：如果对所有的 $i = 1, 2, \cdots, n$ ，都有 $w_i = 1 / n$ ，那么 $x_1, x_2, \cdots, x_n$ 的中位数就是 $x_i$ 的带权中位数。

2. 利用排序，设计一个最坏情况下 $O(n\log n)$ 时间的算法，可以得到 $n$ 个元素的带权中位数。

3. 说明如何利用像[第8讲PPT第14页](/slides/lec08-medians-and-order-statistics.pdf#page=14) 的 SELECT 这样的线性时间中位数算法，在 $\Theta(n)$ 最坏情况时间内求出带权中位数。

**邮局位置问题** 的定义如下：给定权重分别为 $w_1, w_2, \cdots, w_n$ 的 $n$ 个点 $p_1, p_2, \cdots, p_n$ ，我们希望找到一个点 $p$ （不一定是输入点中的一个），使得 $\sum\limits_{i=1}^{n}w_i d(p, p_i)$ 最小，这里 $d(a, b)$ 表示点 $a$ 与 $b$ 之间的距离。

4. 证明：对一维邮局位置问题，带权中位数是最好的解决方法，其中，每个点都是一个实数，点 $a$ 与 $b$ 之间的距离是 $d(a, b) = |a-b|$ 。

5. 请给出二维邮局位置问题问题的最好解决方法：其中的点是 $(x, y)$ 的二维坐标形式，点 $a=(x_1, y_1)$ 与 $b = (x_2, y_2)$ 之间的距离是 **Manhattan 距离** ，即 $d(a, b) = |x_1 - x_2| + |y_1 - y_2|$ 。

##### Solution

1. 若 $w_i = 1 / n$ ，则 $x_1, x_2, \cdots , x_n$ 的带权中位数 $x_k$ 满足

$$
\sum_{x_i < x_k} w_i = \sum_{x_i < x_k} \frac{1}{n} < \frac{1}{2} \Leftrightarrow \sum_{x_i < x_k} < \frac{n}{2} \le \frac{n}{2} - 1
$$

$$
\sum_{x_i > x_k} w_i = \sum_{x_i > x_k} \frac{1}{n} < \frac{1}{2} \Leftrightarrow \sum_{x_i > x_k} \le \frac{n}{2}
$$

于是

$$
n - 1 = \sum_{x_i < x_k} + \sum_{x_i > x_k} \le \frac{n}{2} - 1 + \frac{n}{2} = n - 1
$$

所以 $\sum\limits_{x_i < x_k} = n/2 - 1$ ， $\sum\limits_{x_i > x_k} = n/2$ ，因此 $x_i$ 就是中位数。

2. 首先，使用归并排序或者堆排序根据 $x_i$ 的大小对 $x_1, x_2, \cdots ,x_n$ 进行排序，排好序后的序列记为 $x'_1, x'_2, \cdots ,x'_n$，对应权重为 $w'_1, w'_2, \cdots ,w'_n$ 。然后计算这个排好序的数组的权重前缀和 $S_1, S_2, \cdots$ ，其中 $S_1 = w'_1, S_k = S_{k-1} + w'_k$ 。

    - 直到算到 $S_k$ 使得 $S_{k-1} < 1/2$ 且 $S_k \ge 1/2$ 为止。此时， $x'_k$ 就是带权中位数。 

3. 首先使用 SELECT 算法计算中位数 $x$ ，并根据 $x$ 划分数组。分别计算 $s_1 = \sum\limits_{x_i < x}w_i$ 和 $s_2 = \sum\limits_{x_i > x}w_i$ （递归调用的时候这两个和式也是对整个数组计算），这个过程需要 $O(n)$ 。之后，我们会遇到三种情况：

- 如果 $s_1 < 1/2$ 且 $s_2 \le 1/2$  ，则 $x$ 就是带权中位数，直接返回即可。

- 如果 $s_1 \ge 1/2$ ，则对于 $x$ 左侧的子数组递归寻找带权中位数。

- 如果 $s_2 > 1 / 2$ ，则对于 $x$ 右侧子数组递归寻找带权中位数。

- 不可能 $s_1 \ge 1/2$ 且 $s_2 > 1/2$ ，因为 $s_1 + s_2 < 1$ 。

上述算法的递归式为 $T(n) = T(n/2) + O(n)$ ，使用主定理可得， $T(n) = O(n)$ 。

4. 反证法。记 $p$ 是最好的解决方法，假设 $p$ 并不是 $p_1, p_2, \cdots, p_n$ 的带权中位数。令 $\varepsilon$ 是绝对值足够小的数，满足 $|\varepsilon| < \min\limits_{i \in \{k | p_k\ne p\}}(|p - p_i|)$ 。记带权中位数为 $p_m$ ，如果 $p < p_m$ ，取 $\varepsilon$ 为正数，否则取 $\varepsilon$ 为负数。我们有

$$
\sum_{i=1}^{n}w_id(p+\varepsilon,p_i) = \sum_{i=1}^{n}w_id(p,p_i) + \varepsilon(\sum_{p_i < p}w_i-\sum_{p_i>p}w_i) < \sum_{i=1}^{n}w_id(p,p_i)
$$

其中，第 1 个等号只是单纯的绝对值展开，其中用到了 $|\varepsilon|$ 足够小的条件 。第 2 个小于号用到了 $p$ 和 $p_m$ 的关系：

- 如果 $p < p_m$ ，则 $\sum\limits_{p_i < p}w_i < \sum_{p_i>p}w_i, \varepsilon > 0$ ，于是 $\varepsilon(\sum\limits_{p_i < p}w_i - \sum_{p_i>p}w_i) < 0$ ；

- 如果 $p > p_m$ ，则 $\sum\limits_{p_i < p}w_i > \sum_{p_i>p}w_i, \varepsilon < 0$ ，于是 $\varepsilon(\sum\limits_{p_i < p}w_i - \sum_{p_i>p}w_i) < 0$ ；

综上，我们找到了比 $p$ 更优的位置 $p + \varepsilon$ ，这与 $p$ 是最好的解决方法是矛盾的。因此，$p$ 不是带权中位数的假设不成立， $p$ 只能是带权中位数。

5. 观察到（其中 $x$ 下标表示点的横坐标， $y$ 下标表示点的纵坐标）：

$$
\sum_{i=1}^{n}w_id(p,p_i) = \sum_{i=1}^{n}w_i|p_x - (p_i)_x| + \sum_{i=1}^{n}w_i|p_y - (p_i)_y|
$$

我们只需要让拆分下来的两个和式分别最小即可。根据第 4 问的结论，取 $p = (p_x, p_y)$ 使得 $p_x$ 是所有点横坐标的带权中位数， $p_y$ 是所有点纵坐标的带权中位数， $p$ 就是最好的解决方案。


#### Problem 3 (教材习题 9-3)

**（小顺序统计量）** 要在 $n$ 个数中选出第 $i$ 个顺序统计量， SELECT （详见[第8讲PPT第14页](/slides/lec08-medians-and-order-statistics.pdf#page=14)）在最坏情况下需要的比较次数 $T(n)$ 满足 $T(n) = \Theta(n)$ 。但是，隐含在 $\Theta$ 记号中的常数项是非常大的。当 $i$ 相对 $n$ 来说很小时，我们可以实现一个不同的算法，它以 SELECT 作为子程序，但在最坏情况下所做的比较次数要更少。

1. 设计一个能用 $U_i(n)$ 次比较在 $n$ 个元素中找出第 $i$ 小元素的算法。其中，
$$
U_i(n) = \begin{cases}
T(n) & \text{if } i \ge n / 2\\
\lfloor n/2\rfloor + U_i(\lceil n/2 \rceil) + T(2i) & \text{otherwise}
\end{cases}
$$
    
    （提示：从 $\lfloor n/2 \rfloor$ 个不相交对的两两比较开始，然后对由每对中的较小元素构成的集合进行递归。）

2. 证明：如果 $i < n/2$ ，则有 $U_i(n) = n + O(T(2i)\log(n/i))$ 。

3. 证明：如果 $i$ 是小于 $n / 2$ 的常数，则有 $U_i(n) = n + O(\log n)$ 。

4. 证明：如果对所有 $k \ge 2$ 有 $i = n/k$ ，则 $U_i(n) = n + O(T(2n/k)\log k)$ 。

##### Solution

1. 如果 $i \ge n/2$ ，直接用 SELECT 算法即可，需要 $T(n)$ 次比较。

- 如果 $i < n/2$ ，成对地比较输入元素，需要 $\lfloor n / 2\rfloor$ 次比较，形成了 $\lceil n/2 \rceil$ 组元素（可能有一个落单的）；

- 由于 $i < n/2$ ，递归地在 $\lceil n/2 \rceil$ 个组的较小元素中寻找第 $i$ 小的元素，并据此划分这 $\lceil n/2 \rceil$ 个组（让组内较大数作为较小数的卫星数据跟着一起移动即可），需要 $U_i(\lceil n/2 \rceil)$ 次比较；

- 整个数组的第 $i$ 小元素一定在 $\lceil n/2 \rceil$ 个组的较小元素的前 $i$ 个较小元素所在的组中。对于这 $i$ 个组， $2i$ 个元素调用 SELECT 算法寻找第 $i$ 小的元素，需要 $T(2i)$ 次比较。

    - 剩余的 $\lceil n/2\rceil - i$ 个组中不可能有第 $i$ 小的元素，里面最小也只能有第 $i + 1$ 小的元素。因为前面 $i$ 个组的 $i$ 个较小元素已经比这些组中的所有元素都小了。

上述算法的比较次数 $U_i(n)$ 的递归式为：

$$
U_i(n) = \begin{cases}
T(n) & \text{if } i \ge n / 2\\
\lfloor n/2\rfloor + U_i(\lceil n/2 \rceil) + T(2i) & \text{otherwise}
\end{cases}
$$

2. 使用代入法证明。假设对于更小的 $n$ ，有 $U_i(n) \le n + cT(2i)\log(n/i)$ ，取决于是否 $i < n/4$ ，有两种情况：

- 如果 $i < n/4$ ，则
$$
\begin{aligned}
U_i(n) &= \lfloor n/2\rfloor + U_i(\lceil n/2 \rceil) + T(2i)\\
&\le n/2 + n/2 + cT(2i)\log(n/2i) + T(2i)\\
&= n + cT(2i)\log(n/i) - (c-1)T(2i)
\end{aligned}
$$

    其中，最后一步需要 $c \ge 1$ 。

- 如果 $n/4 \le i < n/2$ （此时有 $n/2 \le 2i$），则 
$$
\begin{aligned}
U_i(n) &= \lfloor n/2\rfloor + U_i(\lceil n/2 \rceil) + T(2i)\\
&\le n/2 + T(n/2) + T(2i)\\
&\le n/2 + 2T(2i)\\
&\le n/2 + cT(2i)\log(n/2i)
\end{aligned}
$$

    其中，最后一步需要 $c \ge 2$ 。

综上，取 $c = 2$ 即可， $U_i(n) \le n + cT(2i)\log(n/i)$ ，即 $U_i(n) = n + O(T(2i)\log(n/i))$ 。

3. 基于第 2 问结论，如果 $i$ 是常数， $O(T(2i)\log(n/i))$ 就变成了 $O(\log n)$ ，于是 $U_i(n) = n + O(\log n)$ 。

4. 基于第 2 问结论，将 $i = n / k$ 代入，有 $U_i(n) =  n + O(T(2i)\log(n/i)) = n + O(T(2n/k)\log k)$ 。


#### Problem 4 (教材习题 9-4)

**（随机化选择的另一种分析方法）** 在这个问题中，我们用指示器随机变量来分析 RANDOMIZED-SELECT ，这一方法类似于[第6讲PPT第27页](/slides/lec06-quicksort.pdf#page=27) 中所用的对 RANDOMIZED-QUICKSORT 的分析方法。

与快速排序中的分析一样，我们假设所有的元素都是互异的，输入数组 $A$ 的元素被重命名为 $z_1, z_2, \cdots , z_n$ ，其中 $z_i$ 是第 $i$ 小的元素。因此，调用 RANDOMIZED-SELECT($A, 1, n, k$) 返回 $z_k$ 。

对所有 $1 \le i < j \le n$ ，设

$$
X_{ijk} = I\{\text{在执行算法查找 }z_k\text{ 期间，} z_i\text{ 与 }z_j\text{ 进行过比较}\}
$$

1.  给出 $E[X_{ijk}]$ 的准确表达式。（提示：你的表达式可能有不同的值，依赖于 $i, j, k$ 的值。）

2. 设 $X_k$ 表示在找到 $z_k$ 时 $A$ 中元素的总比较次数，证明：

$$
E[X_k] \le 2(\sum_{i=1}^{k}\sum_{j=k}^{n}\frac{1}{j-i+1} + \sum_{j=k+1}^{n}\frac{j-k-1}{j-k+1} + \sum_{i=1}^{k-2}\frac{k-i-1}{k-i+1})
$$

3. 证明： $E[X_k]\le 4n$ 。

4. 假设 $A$ 中的元素都是互异的，证明： RANDOMIZED-SELECT 的期望运行时间是 $O(n)$ 。

##### Solution

1. 我们只需要关心当我们选择一个在 $\min(z_i, z_j, z_k)$ 和 $\max(z_i, z_j, z_k)$ 之间的主元的情况。因为此时我们

- 要么选择 $z_i$ 或者 $z_j$ 作为主元，并比较它们两个；

- 要么选择 $z_i$ 和 $z_j$ 之间的元素作为主元，并永远不比较它们两个；

- 要么选择 $z_k$ 和 $[z_i, z_j]$ 区间之间的元素作为主元，并永远不会再选择包含 $z_i$ 和 $z_j$ 的范围中的元素。

为了让 $z_i$ 和 $z_j$ 进行比较，应该选择 $z_i$ 或者 $z_j$ 作为主元，考虑主元选取是随机的，我们有

$$
E(X_{ijk}) = \begin{cases}
\frac{2}{j-k+1} & z_k \le z_i < z_j\\
\frac{2}{j-i+1} & z_i \le z_k < z_j\\
\frac{2}{k-i+1} & z_i < z_j \le z_k
\end{cases}
$$

2. $E[X_k]$ 最多就是所有可能的元素对比较的期望之和：

$$
\begin{aligned}
E[X_k] &\le \sum_{1\le i < j \le n}E[X_{ijk}]\\
&=\sum_{i=1}^{k}\sum_{j=k}^{n}\frac{2}{j-i+1} + \sum_{i=k+1}^{n-1}\sum_{j=i+1}^n\frac{2}{j-k+1} + \sum_{i=1}^{k-2}\sum_{j=i+1}^{k-1}\frac{2}{k-i+1}\\
&=2(\sum_{i=1}^{k}\sum_{j=k}^{n}\frac{1}{j-i+1} + \sum_{j=k+1}^{n}\frac{j-k-1}{j-k+1} + \sum_{i=1}^{k-2}\frac{k-i-1}{k-i+1})
\end{aligned}
$$

其中，最后一步是一个简单的和式变换，将行优先求和转化成列优先求和，类似于[第6讲PPT第29页](/slides/lec06-quicksort.pdf#page=29)中涉及的和式变换。

3. 由 $\frac{j-k-1}{j-k+1} < 1$ 以及 $\frac{k-i-1}{k-i+1} < 1$ 有

$$
\sum_{j=k+1}^{n}\frac{j-k-1}{j-k+1} + \sum_{i=1}^{k-2}\frac{k-i-1}{k-i+1} \le n - k + k - 2 = n - 2
$$

考虑使得 $\frac{1}{j-i+1} = \frac{1}{c}$ 的项，其中 $c$ 是常数。这相当于 $j - i = c - 1$ ，因此这样的项最多有 $c$ 项，$c$ 的范围是 $[1, n]$ ，于是

$$
\sum_{i=1}^{k}\sum_{j=k}^{n}\frac{2}{j-i+1} \le \sum_{c=1}^{n}c\cdot\frac{1}{c} = n
$$

综上， $E[X_k] \le 2(n + n - 2) \le 4n$ 。

4. RANDOMIZED-SELECT 算法中执行次数最多的关键操作就是输入数组中元素的比较操作，根据第 3 问结果， RANDOMIZED-SELECT 过程中输入数组元素间的期望比较次数不超过 $4n$ ，因此 RANDOMIZED-SELECT 的期望运行时间为 $O(n)$ 。

