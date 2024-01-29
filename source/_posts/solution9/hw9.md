---
title: 作业 9 解答
date: 2024-1-28 22:00:00
description: 基本数据结构课后作业题解答
---

#### Problem 1 (教材习题 10-2)

**（利用链表实现可合并堆）** **可合并堆（Mergeable Heap）** 支持以下操作： MAKE-HEAP （创建一个空的可合并堆）、 INSERT 、 MINIMUM 、 EXTRAC-MIN 和 UNION 。说明在下列前提下如何利用链表实现可合并堆。试着使各种操作尽可能高效。分析每个操作关于动态集合规模的运行时间。

1. 链表是已排序的。

2. 链表是未排序的。

3. 链表是未排序的，且带合并的动态集合是不相交的。

##### Solution



#### Problem 2 (教材习题 10-3)

**（搜索已排序的紧凑链表）** [练习9-2](solution9/exe9-2/)问题2讨论了如何将 $n$ 个元素的链表紧凑地维持在数组的前 $n$ 个位置。假设所有的关键字均不相同，且紧凑链表是已排序的，即对所有的 $i = 1, 2, \cdots , n$ 且 $next[i] \ne NIL$ ，有 $key[i] < key[next[i]]$ 。又假设有一个变量 $L$ 存放链表的首元素的下标。在这些假设下，试说明可以利用下列随机算法在 $O(\sqrt{n})$ 的期望时间内搜索链表。

<img src="/assets/compact-list-search.png" alt="compact-list-search" style="zoom:16%;" />

如果忽略过程中第 3 ~ 7 行，就得到一个普通的搜索已排序链表的算法，其中下标 $i$ 依次指向链表的各个位置。当下标 $i$ 越出表的末端或 $key[i] \ge k$ 时，搜索终止。在后一种情况中，如果 $key[i] = k$ ，显然，我们已找到值为 $k$ 的关键字。但如果 $key[i] > k$ ，则我们永远也找不到值为 $k$ 的关键字，因而终止查找是正确的。

第 3 ~ 7 行意图向前跳至某个随机选择的位置 $j$ 。当 $key[j]$ 大于 $key[i]$ 而不大于 $k$ 时，这种跳跃是有益的。因为这种情况下， $j$ 在链表中标识了一个正常搜索中 $i$ 将要到达的位置。由于该链表是紧凑的，所以在 $1$ 到 $n$ 中任意选择一个 $j$ 都会指向链表中的某个对象，而不会是自由表中的某个位置。

我们不直接分析 COMPACT-LIST-SEARCH 的性能，而是要分析一个相关的算法 COMPACT-LIST-SEARCH' ，该算法执行两个独立的循环。该算法增加了一个参数 $t$ ，用来决定第一个循环迭代次数的上限。

<img src="/assets/compact-list-search-prime.png" alt="compact-list-search-prime" style="zoom:16%;" />

为了比较算法 COMPACT-LIST-SEARCH$(L, n, k)$ 和 COMPACT-LIST-SEARCH'$(L, n, k, t)$ 的执行过程，假定调用 RAMDON$(1, n)$ 所返回的整数序列在两个算法中是一样的。

1. 假设 COMPACT-LIST-SEARCH$(L, n, k)$ 中第 2 ~ 8 行的 **while** 循环经过了 $t$ 次迭代。论证 COMPACT-LIST-SEARCH'$(L, n, k, t)$ 会返回同样的结果，且 COMPACT-LIST-SEARCH' 中的 **for** 循环和 **while** 循环的迭代次数之和至少为 $t$ 。

    在 COMPACT-LIST-SEARCH'$(L, n, k, t)$ 的调用中，设随机变量 $X_t$ 描述了第 2 ~ 7 行的 **for** 循环经 $t$ 次迭代后链表中从位置 $i$ 到目标关键字 $k$ 之间的距离（即通过 $next$ 指针链的次数）。

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



