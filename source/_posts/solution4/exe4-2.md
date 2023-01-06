---
title: 练习 4-2 解答
date: 2023-1-5 23:53:00
description: 概率分析和随机算法相关的习题解答
---

#### Problem 1 (教材习题 5.3-3)

假设我们不是将元素 $A[i]$ 与子数组 $A[i..n]$ 中的一个随机元素交换，而是将它与数组任何位置上的随机元素交换：

<iframe src="/pseudocode/lec4/permute-with-all.html" frameborder="no" marginwidth="0" width="100%" height="160px" marginheight="0" scrolling="auto"></iframe>

这段代码会产生一个均匀随机排列吗？为什么会或为什么不会？

##### Solution

不会。反例：例如 $n = 3$ 的情况，从古典概型的角度考虑：

- 由于每次和整个数组中的一个任意随机元素交换，所以共有 $3^3 = 27$ 种等可能的基本事件（不同基本事件的排列结果可重复）；

- 但是 $n = 3$ 时只会有 $3! = 6$ 种排列， $6$ 并不整除 $27$ ，因此所有排列结果分到的基本事件不可能一样多，也就不可能等可能，从而不是均匀随机排列。


#### Problem 2 (教材习题 5.3-5)

证明：在过程 PERMUTE-BY-SORTING （见[第4讲PPT第16页](/slides/lec04-probabilistic-analysis-and-randomized-algorithms.pdf#page=16)）的数组 $P$ 中，所有元素都唯一的概率至少是 $1 - 1/n$ 。

##### Solution

记 $P[i] = P[j]$ 为事件 $X_{ij}$ ，由于 $P[i]$ 和 $P[j]$ 是 $1$ 到 $n^3$ 之间的随机数，我们有：

$$
Pr\{X_{ij}\} = \sum_{r = 1}^{n^3}Pr\{P[i] = r, P[j] = r\} = \sum_{r=1}^{n^3}Pr\{P[i] = r\}Pr\{P[j] = r\}\\
= \sum_{r=1}^{n^3}\frac{1}{n^3}\cdot\frac{1}{n^3} = \frac{1}{n^3}
$$

记 $P$ 中存在某两个相等的元素为事件 $X$ ，则 $X = \bigcup_{i<j}X_{ij}$ ，且任意两个 $X_{ij}$ 之间不相交，故而

$$
Pr\{X\} = Pr\{\bigcup_{i<j}X_{ij}\} = \sum_{i=1}^{n-1}\sum_{j=i+1}^{n}Pr\{X_{ij}\} = \sum_{i=1}^{n-1}\sum_{j=i+1}^{n}\frac{1}{n^3}\\
=\frac{n(n-1)}{2n^3} = \frac{n-1}{2n^2} < \frac{n}{n^2} = \frac{1}{n}
$$

因此，所有元素都唯一的概率为 $Pr\{\overline{X}\} = 1 - Pr\{X\} > 1 - 1/n$ 。

#### Problem 3 (教材习题 5.3-7)

假设我们希望创建集合 $\{1, 2, 3, \cdots, n\}$ 的一个 **随机样本** ，即一个具有 $m$ 个元素的集合 $S$ ，其中 $0 \le m \le n$ ，使得每个 $m$ 集合能够等可能地创建。

一种方法是对 $i = 1, 2, ..., n$ 设 $A[i] = i$ ，调用 $\text{RANDOMIZE-IN-PLACE}(A)$ ，然后取最前面的 $m$ 个元素。这种方法会对 $\text{RANDOM}$ 过程调用 $n$ 次。

如果 $n$ 比 $m$ 大很多，我们希望能够创建一个随机样本，但是对 $\text{RANDOM}$ 调用更少的次数。请说明下面的递归过程返回 $\{1, 2, 3, \cdots, n\}$ 的一个随机 $m$ 子集 $S$ ，其中每个 $m$ 子集是等可能的，然而只对 $\text{RANDOM}$ 调用 $m$ 次。

<iframe src="/pseudocode/lec4/random-sample.html" frameborder="no" marginwidth="0" width="100%" height="360px" marginheight="0" scrolling="auto"></iframe>

##### Solution

记算法2在接受输入 $m, n$ 时调用 $T(m, n)$ 次 $\text{RANDOM}$ ，我们不难看出：

- $T(0,0) = 1$ ， $T(m, n) = T(m - 1, n-1) + 1$ ；

- 解这个递归式有 $T(m, n) = m$ ，因此算法2只对 $\text{RANDOM}$ 调用 $m$ 次。

下面我们使用数学归纳法来证明 $\text{RandomSample}(m, n)$ 的正确性：

对 $m$ 进行归纳，证明对于所有的 $n \ge m$ ，任意 $1 \le j \le n$ ， $Pr\{j \in \text{RandomSample}(m, n)\} = m / n$ 。

- 基础情况：$m = 0$ 时，$Pr\{j \in \text{RandomSample}(0, n)\} = Pr\{j \in \emptyset\} = 0 = 0 / n$ 显然成立；

- 归纳假设：假设 $m - 1$ 时，结论成立。记 $S = \text{RandomSample}(m - 1, n - 1)$ ，则有 $\forall 1 \le j \le n - 1$ ，$Pr\{j \in S\} = (m - 1) / (n - 1)$ 。

- 归纳步骤：记 $\text{RandomSample}(m, n)$ 最终返回的集合为 $S'$ ，下面证明 $\forall 1 \le j \le n$ ，$Pr\{j \in S'\} = m / n$ 。

    - 考虑任意一个给定的 $j$ 满足 $1 \le j \le n$ ，由于 $i$ 是 $1$ 到 $n$ 之间的随机数（算法2第6行），因此 $Pr\{i = j\} = 1 / n$ 。

    - 先证明 $1 \le j \le n - 1$ 时， $Pr\{j \in S'\} = m / n$ ：

        - 根据算法7到10行，$j \in S'$ 等价于 $j \in S$ 或者 $j \notin S \wedge i = j$ ，因为 $j \ne n$ 。

            - $Pr\{j \in S'\} = Pr\{j \in S\} + Pr\{j \notin S\}\cdot Pr\{i = j\}\\ = \frac{m-1}{n-1} + (1-\frac{m-1}{n-1})\cdot\frac{1}{n} = \frac{m}{n}$ 。
    
    - 最后证明 $Pr\{n \in S'\} = m / n$ 。

        - 根据算法第7到12行，$n \in S'$ 等价于 $i \in S$ 或者 $i = n$ ；

        - 其中， $Pr\{i \in S\} = \frac{m-1}{n}$ ，因为 $i$ 是 1 到 n 的随机数， $S$ 是一个 1 到 n 之间的 $m - 1$ 元子集；

        - 所以 $Pr\{n \in S'\} = Pr\{i \in S\} + Pr\{i = n\} = \frac{m - 1}{n} + \frac{1}{n} = \frac{m}{n}$ 。

综上，对于所有的 $n \ge m$ ，任意 $1 \le j \le n$ ， $Pr\{j \in \text{RandomSample}(m, n)\} = m / n$ 。

因此，算法2返回了 $n$ 的一个均匀随机的 $m$ 子集。


#### Problem 4 (教材习题 5.4-2)

假设我们将球投入到 $b$ 个箱子里，直到某个箱子中有两个球。每一次投掷都是独立的，并且每个球落入任何箱子的机会均等。请问投球次数期望是多少？

##### Solution

把将球投入到箱子里视为“球在这个箱子里出生”，箱子就是球的“生日”，问题可以重新表述为：一共有 $b$ 个箱子，房间里需要有多少个球，才能期望有两个球的“生日”相同？

所以这个问题其实就是将“生日悖论”换了个场景而已，本质不变，根据[第4讲PPT第23页](/slides/lec04-probabilistic-analysis-and-randomized-algorithms.pdf#page=23)，不难得到投球次数的期望为 $\Theta(\sqrt{b})$ 。


#### Problem 5 (教材习题 5.4-4)

一次聚会需要邀请多少人，才能期望其中有 $3$ 人的生日相同？

##### Solution

假设邀请了 $m$ 个人，一年有 $n$ 天。记其中第 $i, j, k$ 个人生日 $b_i, b_j, b_k$ 相同为事件 $H_{ijk}$ ，和[第4讲PPT第22页](/slides/lec04-probabilistic-analysis-and-randomized-algorithms.pdf#page=22)类似，有

$$
Pr\{H_{ijk}\} = \sum_{r=1}^{n}Pr\{b_i = b_j = b_k = r\} = n\cdot\frac{1}{n^3} = \frac{1}{n^2}
$$

记 $X_{ijk} = I\{H_{ijk}\}$ ，设生日相同的三人组的个数为 $X$ ，则

$$
E[X] = E[\sum_{i=1}^{m-2}\sum_{j=2}^{m-1}\sum_{k=3}^m X_{ijk}] = \sum_{i=1}^{m-2}\sum_{j=2}^{m-1}\sum_{k=3}^m E[X_{ijk}] = \sum_{i=1}^{m-2}\sum_{j=2}^{m-1}\sum_{k=3}^m Pr\{H_{ijk}\}\\
= \sum_{i=1}^{m-2}\sum_{j=2}^{m-1}\sum_{k=3}^m \frac{1}{n^2} = \frac{m(m-1)(m-2)}{6n^2} \ge 1 
$$

不难看出 $m = \Theta(n^{2/3})$ 。

具体地，假设一年有 $n=365$ 天，代入有 $m(m-1)(m-2) \ge 6\times 365^2$ ，解得 $m \ge 94$ 。


#### Problem 6 (教材习题 5.4-5)

在大小为 $n$ 的集合中，一个 $k$ 字符串构成一个 $k$ 排列的概率是多少？这个问题和生日悖论有什么关系？

##### Solution

$k$ 字符串构成 $k$ 排列相当于 $k$ 字符串中的每个字符都不相同，记为事件 $E$ 。考虑后一个字符和前面所有的字符都不相同，应用乘法原理有：

$$
Pr\{E\} = \frac{n}{n} \cdot \frac{n-1}{n} \cdot \frac{n-2}{n} \cdots \frac{n-k+1}{n} = \frac{n!}{n^k(n-k)!}
$$

这是生日悖论的补问题，生日悖论相当于是希望一个 $k$ 字符串中存在两个相同的字符（$k$ 个人中有两个生日相同），本题是希望一个 $k$ 字符串中不存在两个相同的字符。

#### Problem 7 (教材习题 5.4-6)

假设将 $n$ 个球投入 $n$ 个箱子里，其中每次投球独立，并且每个球等可能落入任何箱子。空箱子的数目期望是多少？正好有一个球的箱子的数目期望是多少？

##### Solution

记第 $i$ 个箱子为空为事件 $E_i$ ，相当于每次投球都没有落入这个箱子，所以 $Pr\{E_i\} = ((n-1) /n)^n$ 。

设 $X_i = I\{E_i\}$ ，空箱子的总数目为 $X$ ，则 $X = \sum_{i=1}^{n}X_i$ ，所以

$$
E[X] = E[\sum_{i=1}^{n}X_i] = \sum_{i=1}^{n}E[X_i] = \sum_{i=1}^{n}Pr\{E_i\} = \sum_{i=1}^{n}(\frac{n-1}{n})^n = n(\frac{n-1}{n})^n
$$

所以，空箱子的数目期望为 $n(\frac{n-1}{n})^n$ 。

记第 $i$ 个箱子恰好有一个球为事件 $F_i$ ，相当于 $n$ 次投球中有 1 次落入这个箱子， $n - 1$ 次没有落入这个箱子，所以 $Pr\{F_i\} = C_n^1 (1/n) ((n-1) /n)^{n-1} = ((n-1) /n)^{n-1}$ （二项分布） 。

设 $Y_i = I\{F_i\}$ ，恰有一个球的箱子的总数目为 $Y$ ，则 $Y = \sum_{i=1}^{n}Y_i$ ，所以

$$
E[Y] = E[\sum_{i=1}^{n}Y_i] = \sum_{i=1}^{n}E[Y_i] = \sum_{i=1}^{n}Pr\{F_i\} = \sum_{i=1}^{n}(\frac{n-1}{n})^{n-1} = n(\frac{n-1}{n})^{n-1}
$$

所以，恰有一个球的箱子的数目期望为 $n(\frac{n-1}{n})^{n-1}$ 。


