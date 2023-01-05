---
title: 练习 4-1 解答
date: 2023-1-4 23:53:00
description: 概率分析和随机算法相关的习题解答
---

#### Problem 1 (教材习题 5.1-2)

请描述 $RANDOM(a, b)$ 过程的一种实现，它只调用 $RANDOM(0, 1)$ 。作为 $a$ 和 $b$ 的函数，你的过程的期望运行时间是多少？

##### Solution




#### Problem 2 (教材习题 5.1-3)

假设你希望以 $1 / 2$ 的概率输出 $0$ 与 $1$ 。你可以自由使用一个输出 $0$ 或 $1$ 的过程 $\text{BIASED-RANDOM}$ 。它以某概率 $p$ 输出 $1$ ，概率 $1 - p$ 输出 $0$ ，其中 $0 < p < 1$ ，但是 $p$ 的值未知。

请给出一个利用 $\text{BIASED-RANDOM}$ 作为子程序的算法，返回一个无偏的结果，能以概率 $1 / 2$ 返回 $0$ ，以概率 $1 / 2$ 返回 $1$ 。作为 $p$ 的函数，你的算法的期望运行时间是多少？

##### Solution


#### Problem 3 (教材习题 5.2-1 和 5.2-2)

在 $\text{HIRE-ASSISTANT}$ 中，假设应聘者以随机顺序出现，你正好雇佣一次的概率是多少？正好雇佣 $n$ 次的概率是多少？正好雇佣两次的概率是多少？

##### Solution


#### Problem 4 (教材习题 5.2-4)

利用指示器随机变量来解决如下的 **帽子核对问题** （hat-heck problem）： $n$ 位顾客，他们每个人给餐厅核对帽子的服务生一顶帽子。服务生以随机顺序将帽子还给顾客。请问拿到自己帽子的客户的期望数是多少？

##### Solution


#### Problem 5 (教材习题 5.2-5)

设 $A[1..n]$ 是由 $n$ 个不同数构成的数列。如果 $i < j$ 且 $A[i] > A[j]$ ，则称 $(i, j)$ 对为 $A$ 的一个 **逆序对(inversion)** 。（参看[作业1](/solution1/hw1/)问题4中更多关于逆序对的例子。）假设 $A$ 的元素构成 $\langle1, 2, \cdots, n\rangle$ 上的一个均匀随机排列。请用指示器随机变量来计算其中逆序对的数目期望。

##### Solution


#### Problem 6 (教材习题 5.3-1)

熊大教授不同意引理5.5证明（见[第4讲PPT第19页](/slides/lec04-probabilistic-analysis-and-randomized-algorithms.pdf#page=19))中使用的循环不变式。他对第1次迭代之前循环不变式是否为真提出质疑。他的理由是，我们可以很容易宣称一个空数组不包含0排列。因此，一个空的子数组包含一个0排列的概率是0，从而第1次迭代之前循环不变式无效。

请重写算法 $\text{RANDOMIZE-IN-PLACE}$ ，使得相关循环不变式适用于第1次迭代之前的非空子数组，并为你的算法修改引理5.5的证明。

##### Solution


#### Problem 7 (教材习题 5.3-2)

熊二教授决定写一个过程来随机产生除恒等排列（identity permutation）外的任意排列。他提出了如下算法：

<iframe src="/pseudocode/lec4/permute-without-identity.html" frameborder="no" marginwidth="0" width="100%" height="160px" marginheight="0" scrolling="auto"></iframe>

这个算法实现了熊二教授的意图吗？

##### Solution


#### Problem 8 (教材习题 5.3-4)

熊翠花教授建议用下面的过程来产生一个均匀随机排列：

<iframe src="/pseudocode/lec4/permute-by-cyclic.html" frameborder="no" marginwidth="0" width="100%" height="300px" marginheight="0" scrolling="auto"></iframe>

请说明每个元素 $A[i]$ 出现在 $B$ 中任何特定位置的概率是 $1 / n$ 。然后通过说明排列结果不是均匀随机排列，表明熊翠花教授错了。

##### Solution


