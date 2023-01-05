---
title: 练习 4-2 解答
date: 2023-1-5 23:53:00
description: 概率分析和随机算法相关的习题解答
---

#### Problem 1 (教材习题 5.3-3)

假设我们不是将元素 $A[i]$ 与子数组 $A[1..n]$ 中的一个随机元素交换，而是将它与数组任何位置上的随机元素交换：

<iframe src="/pseudocode/lec4/permute-with-all.html" frameborder="no" marginwidth="0" width="100%" height="160px" marginheight="0" scrolling="auto"></iframe>

这段代码会产生一个均匀随机排列吗？为什么会或为什么不会？

##### Solution



#### Problem 2 (教材习题 5.3-5)

证明：在过程 PERMUTE-BY-SORTING （见[第4讲PPT第16页](/slides/lec04-probabilistic-analysis-and-randomized-algorithms.pdf#page=16)）的数组 $P$ 中，所有元素都唯一的概率至少是 $1 - 1/n$ 。

##### Solution



#### Problem 3 (教材习题 5.3-7)

假设我们希望创建集合 $\{1, 2, 3, \cdots, n\}$ 的一个 **随机样本** ，即一个具有 $m$ 个元素的集合 $S$ ，其中 $0 \le m \le n$ ，使得每个 $m$ 集合能够等可能地创建。

一种方法是对 $i = 1, 2, ..., n$ 设 $A[i] = i$ ，调用 $\text{RANDOMIZE-IN-PLACE}(A)$ ，然后取最前面的 $m$ 个元素。这种方法会对 $\text{RANDOM}$ 过程调用 $n$ 次。

如果 $n$ 比 $m$ 大很多，我们希望能够创建一个随机样本，但是对 $\text{RANDOM}$ 调用更少的次数。请说明下面的递归过程返回 $\{1, 2, 3, \cdots, n\}$ 的一个随机 $m$ 子集 $S$ ，其中每个 $m$ 子集是等可能的，然而只对 $\text{RANDOM}$ 调用 $m$ 次。

<iframe src="/pseudocode/lec4/random-sample.html" frameborder="no" marginwidth="0" width="100%" height="360px" marginheight="0" scrolling="auto"></iframe>

##### Solution



#### Problem 4 (教材习题 5.4-2)

假设我们将球投入到 $b$ 个箱子里，直到某个箱子中有两个球。每一次投掷都是独立的，并且每个球落入任何箱子的机会均等。请问投球次数期望是多少？

##### Solution



#### Problem 5 (教材习题 5.4-4)

一次聚会需要邀请多少人，才能期望其中有 $3$ 人的生日相同？

##### Solution



#### Problem 6 (教材习题 5.4-5)

在大小为 $n$ 的集合中，一个 $k$ 字符串构成一个 $k$ 排列的概率是多少？这个问题和生日悖论有什么关系？

##### Solution


#### Problem 7 (教材习题 5.4-6)

假设将 $n$ 个球投入 $n$ 个箱子里，其中每次投球独立，并且每个球等可能落入任何箱子。空箱子的数目期望是多少？正好有一个球的箱子的数目期望是多少？

##### Solution


