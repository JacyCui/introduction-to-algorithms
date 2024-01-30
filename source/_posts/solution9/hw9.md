---
title: 作业 9 解答
date: 2024-1-31 2:00:00
description: 基本数据结构课后作业题解答
---

#### Problem 1 (教材习题 10-2)

**（利用链表实现可合并堆）** **可合并堆（Mergeable Heap）** 支持以下操作： MAKE-HEAP （创建一个空的可合并堆）、 INSERT 、 MINIMUM 、 EXTRACT-MIN 和 UNION 。说明在下列前提下如何利用链表实现可合并堆。试着使各种操作尽可能高效。分析每个操作关于动态集合规模的运行时间。

1. 链表是已排序的。

2. 链表是未排序的。

3. 链表是未排序的，且待合并的动态集合是不相交的。

##### Solution

用已排序链表实现的算法如下：

<iframe src="/pseudocode/lec9/mergable-heap-sorted.html" frameborder="no" marginwidth="0" width="100%" height="1450px" marginheight="0" scrolling="auto"></iframe>

用未排序的链表实现的算法如下（待合并的动态集合不相交的时候也可以用下面的算法）：

<iframe src="/pseudocode/lec9/mergable-heap-unsorted.html" frameborder="no" marginwidth="0" width="100%" height="930px" marginheight="0" scrolling="auto"></iframe>

运行时间（其中 $n$ 为链表内的元素个数）：

|操作|已排序（算法1）|未排序（算法2）|
|:-:|:-:|:-:|
|MAKE-HEAP| $O(1)$ | $O(1)$ |
|INSERT| $O(n)$ | $O(1)$ |
|MINIMUM| $O(1)$ | $O(n)$ |
|EXTRAC-MIN| $O(1)$ | $O(n)$ |
|UNION| $O(n)$ | $O(1)$ |

#### Problem 2 (教材习题 10-3)

**（搜索已排序的紧凑链表）** [练习9-2](solution9/exe9-2/)问题2讨论了如何将 $n$ 个元素的链表紧凑地维持在数组的前 $n$ 个位置。假设所有的关键字均不相同，且紧凑链表是已排序的，即对所有的 $i = 1, 2, \cdots , n$ 且 $next[i] \ne NIL$ ，有 $key[i] < key[next[i]]$ 。又假设有一个变量 $L$ 存放链表的首元素的下标。在这些假设下，试说明可以利用下列随机算法在 $O(\sqrt{n})$ 的期望时间内搜索链表。

<img src="/assets/compact-list-search.png" alt="compact-list-search" style="zoom:16%;" />

如果忽略过程中第 3 ~ 7 行，就得到一个普通的搜索已排序链表的算法，其中下标 $i$ 依次指向链表的各个位置。当下标 $i$ 越出表的末端或 $key[i] \ge k$ 时，搜索终止。在后一种情况中，如果 $key[i] = k$ ，显然，我们已找到值为 $k$ 的关键字。但如果 $key[i] > k$ ，则我们永远也找不到值为 $k$ 的关键字，因而终止查找是正确的。

第 3 ~ 7 行意图向前跳至某个随机选择的位置 $j$ 。当 $key[j]$ 大于 $key[i]$ 而不大于 $k$ 时，这种跳跃是有益的。因为这种情况下， $j$ 在链表中标识了一个正常搜索中 $i$ 将要到达的位置。由于该链表是紧凑的，所以在 $1$ 到 $n$ 中任意选择一个 $j$ 都会指向链表中的某个对象，而不会是自由表中的某个位置。

我们不直接分析 COMPACT-LIST-SEARCH 的性能，而是要分析一个相关的算法 COMPACT-LIST-SEARCH' ，该算法执行两个独立的循环。该算法增加了一个参数 $t$ ，用来决定第一个循环迭代次数的上限。

<img src="/assets/compact-list-search-prime.png" alt="compact-list-search-prime" style="zoom:16%;" />

为了比较算法 COMPACT-LIST-SEARCH$(L, n, k)$ 和 COMPACT-LIST-SEARCH'$(L, n, k, t)$ 的执行过程，假定调用 RAMDON$(1, n)$ 所返回的整数序列在两个算法中是一样的。

1. 假设 COMPACT-LIST-SEARCH$(L, n, k)$ 中第 2 ~ 8 行的 **while** 循环经过了 $t$ 次迭代。论证 COMPACT-LIST-SEARCH'$(L, n, k, t)$ 会返回同样的结果，且 COMPACT-LIST-SEARCH' 中的 **for** 循环和 **while** 循环的迭代次数之和至少为 $t$ 。

在 COMPACT-LIST-SEARCH'$(L, n, k, t)$ 的调用中，设随机变量 $X_t$ 描述了第 2 ~ 7 行的 **for** 循环经 $t$ 次迭代后链表中从位置 $i$ 到目标关键字 $k$ 所在位置之间的距离（即通过 $next$ 指针链的次数）。

2. 论证 COMPACT-LIST-SEARCH'$(L, n, k, t)$ 的期望运行时间为 $O(t + E[X_t])$ 。

3. 证明： $E[X_t] \le \sum_{r = 1}^{n} (1 - r / n)^t$ 。提示：当随机变量 $X$ 可在自然数集 $\mathbb{N} = \{0, 1, 2, \cdots\}$ 中取值时，有一个很好的期望计算公式：

    $$
        \begin{aligned}
            E[X] &= \sum_{i = 0}^{\infty} i \cdot Pr\{X = i\} = \sum_{i = 0}^{\infty} i \cdot (Pr\{X \ge i\} - Pr\{X \ge i + 1\})\\
            & = \sum_{i=1}^{\infty} Pr\{X \ge i\}
        \end{aligned}
    $$

4. 证明： $\sum_{r=0}^{n - 1} r^t \le n^{t+1} / (t + 1)$ 。

5. 证明： $E[X_t] \le n / (t + 1)$ 。

6. 证明： COMPACT-LIST-SEARCH'$(L, n, k, t)$ 的期望运行时间为 $O(t + n/t)$ 。

7. 证明： COMPACT-LIST-SEARCH 的期望运行时间为 $O(\sqrt{n})$ 。

8. 为什么要假设 COMPACT-LIST-SEARCH 中的所有关键字均不相同？论证当链表中包含重复的关键字时，随机跳跃不一定能降低渐近时间。

##### Solution

1. COMPACT-LIST-SEARCH 和 COMPACT-LIST-SEARCH' 的区别是：

- COMPACT-LIST-SEARCH$(L, n, k)$ 轮流执行“随机步”（算法第 3 ～ 7 行）和“正常步”（算法第 8 行）直到找到或者搜索完为止；

    - $t$ 轮迭代则一共执行了 $t$ 轮“随机步” 和 $t - 1$ 或者 $t$ 轮“正常步”（取决于 while 循环是因为第 7 行的 return 语句终止还是因为循环条件不满足终止）；

- COMPACT-LIST-SEARCH'$(L, n, k, t)$ 先执行 $t$ 次“随机步”（算法第 3 ～ 7 行），然后再执行“正常步”（算法第 8 ~ 9 行）直到找到或者搜完为止。

这两个算法显然都是正确的，因为它们的“随机步”和“正常步”都没有错失需要寻找的 $k$ ，而链表的所有关键字各不相同，因而如果能找到的话，只会有一个结点的关键字是 $k$ ，从而两个正确的算法会返回同样的结果。

我们已经假设了调用 RANDOM$(1, n)$ 所返回的整数序列在两个算法中是一样的，因此两个算法当中随机步所随机出的位置都是一样的。

- 如果 COMPACT-LIST-SEARCH 是通过第 7 行的 return 语句跳出循环的，也就是通过第 $t$ 次“随机步”找到目标的，那么 COMPACT-LIST-SEARCH' 也会在第 $t$ 次“随机步”找到目标，从而也会通过第 7 行的 return 语句终止，从而 for 循环迭代了 $t$ 次， $while$ 循环迭代了 $0$ 次，一共迭代了 $t$ 次， $t \ge t$ 。

- 如果 COMPACT-LIST-SEARCH 是通过第 2 行的 while 循环条件跳出循环的，也就是通过第 $t$ 次“正常步”找到目标的，那么说明目标处于第 $t$ 次“随机步”对应位置的下一个位置，因此 COMPACT-LIST-SEARCH' 在 for 循环处运行了 $t$ 次“随机步”之后，在第 8 ～ 9 行的 while 循环处只会运行 $1$ 次“正常步”，从而一共迭代了 $t + 1$ 次， $t + 1 \ge t$ 。

综上，COMPACT-LIST-SEARCH' 中的 for 循环和 while 循环的迭代次数之和至少为 $t$ 。

2. 从第 1 问的分析中我们已经知道，算法 COMPACT-LIST-SEARCH'$(L, n, k, t)$ 先执行 $t$ 轮“随机步”，然后再不断执行“正常步”从 $t$ 轮“随机步”给出的离目标最近的位置 $i$ 的位置到目标关键字 $k$ ，也就是 $X_t$ 步。因此该算法 for 循环和 while 循环 一共执行了 $t + X_t$ 轮迭代，每轮迭代都是常数项时间，所以运行时间为 $O(t + X_t)$ ，从而期望运行时间为

$$
O(E[t + X_t]) = O(t + E[X_t])
$$

3. $X_t$ 是 for 循环结束后 $i$ 到目标 $k$ 所在位置的距离，

所以其取值范围为 $[0, n - 1]$ ，根据提示的公式不难有

$$
E[X_t] = \sum_{r=1}^{n}Pr\{X_t\ge r\}
$$

因此，只需要说明 $Pr\{X_t \ge r\} \le (1 - r / n)^t$ 即可。

$X_t \ge r$ 说明每次随机选择的位置都不在 $k$ 之前的 $r$ 个位置上，一共 $n$ 个位置，随机选择不在其中 $r$ 个固定位置的概率为 $1 - r / n$ ，每次随机选择都是独立的，因此根据独立时间概率的乘法公式， $t$ 次随机选择都不在的概率为 $(1 - r / n)^t$ ，即

$$
Pr\{X_t \ge r\} = (1 - r / n)^t
$$

从而

$$
E[X_t] = \sum_{r=1}^{n}Pr\{X_t\ge r\} = \sum_{r=1}^{n}(1 - r / n)^t
$$

4. 当 $t = 0$ 时，式子左边第一项 $0^0$ 是没有意义的，因此 $t > 0$ ，于是 $\lfloor x\rfloor^t \le x^t$ ，所以

$$
\sum_{r = 0}^{n - 1} r^t = \int_{0}^{n} \lfloor r\rfloor^t dr 
\le \int_{0}^{n} r^t dr = \frac{n^{t+1}}{t+1}
$$

5. 根据第 3 问和第 4 问的结论，有

$$
E[X_t] \le \sum_{r=1}^{n}(1 - r / n)^t
= \sum_{r=1}^{n}\frac{(n - r)^t}{n^t}
= \frac{1}{n^t}\sum_{r=0}^{n-1}r^t
\le \frac{1}{n^t}\cdot \frac{n^{t+1}}{t+1}
=\frac{n}{t+1}
$$

6. 根据第 2 问有 COMPACT-LIST-SEARCH'$(L, n, k, t)$ 的期望运行时间为

$$
O(t + E[X_t])
$$

根据第 5 问有 $t + E[X_t] \le t + n / (t + 1) < t + n/t $ ，从而

$$
O(t + E[X_t]) = O(t + n/t)
$$

也就是说 COMPACT-LIST-SEARCH'$(L, n, k, t)$ 的期望运行时间为 $O(t + n/t)$ 。

7. 第 1 问我们论证了 COMPACT-LIST-SEARCH 算法是优于 COMPACT-LIST-SEARCH' 的；第 2 到 6 问我们论证了 COMPACT-LIST-SEARCH'$(L, n, k, t)$ 的期望运行时间为 $O(t + n/t)$ ；于是 COMPACT-LIST-SEARCH'$(L, n, k, \sqrt{n})$ 的期望运行时间为 $O(\sqrt{n} + n/\sqrt{n}) = O(\sqrt{n})$ ；从而，优于 COMPACT-LIST-SEARCH' 的 COMPACT-LIST-SEARCH 算法的期望运行时间也为 $O(\sqrt{n})$ 。

8. 当链表中有关键字相同的时候，我们可能会选择随机选择到比我们当前位置更靠近目标位置的结点但是却没有跳转过去，因为它和我们的当前位置的关键字是相同的，但我们只有在随机选择到关键字比我们当前位置更大且未超过目标位置的时候才会跳转（具体见算法第 4 行）。

