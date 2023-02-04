---
title: 练习 8-1 解答
date: 2023-2-3 01:40:00
description: 顺序统计量相关的习题解答
---

#### Problem 1 (教材习题 9.1-1)

证明：可以用最坏情况下 $n + \lceil \log n \rceil - 2$ 次比较，找到 $n$ 个元素中的第二小的元素。（提示：可以同时找最小元素。）

##### Solution

证明：可以使用锦标赛的方式来进行比较，胜者（更小的那一个）晋级，败者淘汰，记录下每个选手的手下败将有哪些。这个两两比较晋级再两两比较最终到达决赛的过程形成了一棵自底向上的二叉树。

我们可以在 $n - 1$ 次比较中选出最小元素，第二小的元素一定在这个最小元素的手下败将中，因为能够打败第二小元素的只可能是最小的元素。最小元素最多有 $\lceil \log n \rceil$ 个手下败将，因为有 $n$ 个叶结点的二叉树的高度不超过 $\lceil \log n \rceil$ 。

接下来，我们可以在这 $\lceil \log n \rceil$ 个最小元素的手下败将中再进行一轮锦标赛，使用 $\lceil \log n \rceil - 1$ 次比较找到其中的最小元素，这就是全部 $n$ 个元素中的第 2 小元素。

上述算法一共使用了 $n - 1 + \lceil \log n \rceil - 1 = n + \lceil \log n \rceil - 2$ 次比较。


#### Problem 2 (教材习题 9.1-2)

证明：在最坏情况下，同时找到 $n$ 个元素中最大值和最小值的比较次数的下界是 $\lceil 3n/2\rceil - 2$ 。（提示：考虑有多少个数有成为最大值或者最小值的潜在可能，然后分析一下每一次比较会如何影响这些计数）

##### Solution

证明：用 $MAX$ 表示所有可能成为最大值的元素的集合， $MIN$ 表示可能所有可能成为最小值的元素的集合。起初，没有进行任何比较的时候，这 $n$ 个元素都有可能是最大值或者最小值，从而 $MAX$ 和 $MIN$ 里面都是全部的 $n$ 个元素。于是，寻找最大最小元素就相当于将 $MAX$ 和 $MIN$ 变成单元集。

比较操作可能会有三种情况：

1. $a \in MAX$ 和 $b \in MIN$ 比较得到 $a < b$ ，则 $MAX = MAX - \{a\}$ ， $MIN = MIN - \{b\}$ ；

2. $a, b \in MAX$ 比较得到 $a < b$ ，则 $MAX = MAX - \{a\}$ ；

3. $a, b \in MIN$ 比较得到 $a < b$ ，则 $MIN = MIN - \{b\}$ 。

不难看出，第 1 种比较是最优的，因为它能够通过一次比较同时减小 $MIN$ 和 $MAX$ 两个集合的大小。至少进行 $\lceil n / 2\rceil$ 次第 1 种比较就能使得 $MIN \cap MAX = \emptyset$ ，两个集合的大小分别为 $\lfloor n / 2\rfloor$ 和 $\lceil n/2 \rceil$ 。

之后就只能进行第 2 种和第 3 种类型的比较了，它们只能让 $MAX$ 或者 $MIN$ 的大小减一。让大小为 $\lfloor n / 2\rfloor$ 的集合变成单元集至少需要 $\lfloor n / 2 \rfloor - 1$ 次比较；让大小为 $\lceil n / 2\rceil$ 的集合变成单元集至少需要 $\lceil n / 2 \rceil - 1$ 次比较 。

综上，同时寻找 $n$ 个元素的最大值和最小值所需要的比较次数的下界为

$$
\lceil \frac{n}{2} \rceil + \lfloor \frac{n}{2} \rfloor - 1 + \lceil \frac{n}{2} \rceil - 1 = \lceil \frac{n}{2} \rceil + n - 2 = \lceil\frac{3n}{2}\rceil - 2
$$


#### Problem 3 (教材习题 9.2-2)

请讨论：指示器随机变量 $X_k$ 和 $T(\max(k-1, n-1))$ 是独立的。（变量定义见[第8讲PPT第11页](/slides/lec08-medians-and-order-statistics.pdf#page=11)）

##### Solution

即使我们知道 $k - 1$ 和 $\max(k-1, n-1)$ ， $X_k = 1$ 的概率也是不变的，依旧是 $1 / n$ ，因为 RANDOMIZED-PARTITION 的结果不受 $k$ 的影响。也就是说，对于 $a = 0,1$ ， $m = k - 1, n - k$ ，有

$$
Pr\{X_k = a | \max(k - 1, n - k) = m\} = Pr\{X_k = a\}
$$

因此 $X_k$ 和 $\max(k - 1, n - k)$ 是独立的。又因为独立随机变量的函数依旧是独立的，所以 $X_k$ 和 $T(\max(k - 1, n - k))$ 也是独立的。


#### Problem 4 (教材习题 9.2-3)

给出 RANDOMIZED-SELECT （详见[第8讲PPT第10页](/slides/lec08-medians-and-order-statistics.pdf#page=10)）算法的迭代版本。

##### Solution

RANDOMIZED-SELECT 算法是一个尾递归算法，它可以很容易优化成一个只需要常数项额外空间的迭代算法。

<iframe src="/pseudocode/lec8/iterative-randomized-select.html" frameborder="no" marginwidth="0" width="100%" height="360px" marginheight="0" scrolling="auto"></iframe>


#### Problem 5 (教材习题 9.3-1)

在算法 SELECT （见[第8讲PPT第14页](/slides/lec08-medians-and-order-statistics.pdf#page=14)）中，输入元素被分为每组 5 个元素。如果它们被分为每组 7 个元素，该算法仍会是线性时间吗？证明：如果分成每组 3 个元素， SELECT 的运行时间不是线性的。

##### Solution

分为每组 7 个元素，该算法仍会是线性的。和每组 5 个元素类似的，除了 $x$ 所在的组和不能整除剩余的组以外，至少有一半的组中有 4 个元素大于 $x$ ，因此大于 $x$ 的元素个数至少为

$$
4(\lceil\frac{1}{2}\lceil \frac{n}{7}\rceil \rceil - 2) \ge \frac{2n}{7} - 8
$$

于是，子问题规模最多为 $n - (2n/7 - 8) = 5n/7 + 8$ ，从而有递归式

$$
T(n) \le T(\lceil \frac{n}{7} \rceil) + T(\frac{5n}{7} + 8) + O(n)
$$

通过代入法不难证明 $T(n) = O(n)$ 。因此分成每组 7 个，该算法仍然是线性时间。

不过，如果分成每组 3 个的话就不是线性时间了。

证明：除了 $x$ 所在的组和不能整除剩余的组以外，至少有一半的组中有 2 个元素大于 $x$ ，因此大于 $x$ 的元素个数至少为

$$
2(\lceil\frac{1}{2}\lceil \frac{n}{3}\rceil \rceil - 2) \ge \frac{n}{3} - 4
$$

于是，子问题规模最多为 $n - (n/3 - 4) = 2n/3 + 4$ 。从而有递归式

$$
T(n) \le T(\lceil\frac{n}{3}\rceil) + T(\frac{2n}{3} + 4) + O(n)
$$

考虑类似的递归式 $T(n) = T(n/3) + T(2n/3) + O(n)$ ，根据[练习3-2](/solution3/exe3-2/)问题2，其解为 $T(n) = \Theta(n\log n)$ 。因此， $T(n)$ 的最坏情况超过线性时间。

综上，如果分成每组 3 个元素， SELECT 的运行时间不是线性的。

