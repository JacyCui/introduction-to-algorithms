---
title: 练习 7-2 解答
date: 2023-1-30 20:34:00
description: 基数排序和桶排序相关的习题解答
---

#### Problem 1 (教材习题 8.3-3)

利用循环不变式来证明基数排序（详见[第7讲PPT第17页](/slides/lec07-sorting-in-linear-time.pdf#page=17)）是正确的。在你所给出的证明中，在哪里需要假设所用的底层排序算法是稳定的？

##### Solution

证明：循环不变式：在算法第 1 到 2 行的 **for** 循环每次迭代开始前，数组 $A$ 已经根据低 $i-1$ 位排好序了。

初始化：第一次迭代开始前，$i = 1$ ，数组已经 $A$ 平凡地根据低 $1 - 1 = 0$ 位排好序了，不变式显然成立。

保持：假设迭代开始前，数组 $A$ 已经根据低 $i - 1$ 位排好序了。在算法第 2 行运行结束后，数组会根据从低往高第 $i$ 位排好序。显然，第 $i$ 位不同的数字之间已经根据低 $i$ 位大小有序了，因为第 $i$ 位不同的数字之间根据低 $i$ 位比较大小只需要看最高的第 $i$ 位即可。

在第 $i$ 位相同的一组数字当中，由于第 $i$ 位相同时，根据低 $i$ 位比较大小只需要看低 $i - 1$ 位。而迭代开始前，低 $i-1$ 位已经有序，并且我们使用的是 **稳定** 排序，所以现在第 $i$ 位相同的这一组数字当中，他们的低 $i-1$ 位依旧是有序的，从而这组数字本身是根据低 $i$ 位有序的。

综上，下一次迭代开始前，数组 $A$ 已经根据低 $i$ 位排好序了，循环保持了不变式。

终止：在循环终止时， $i = d + 1$ ，根据循环不变式，数组 $A$ 已经根据低 $i - 1 = d$ 位排好序了。

而 $A$ 本身就是由 $n$ 个 $d$ 位的元素组成的，所以数组 $A$ 也已经排好序了，基数排序的算法是正确的。


#### Problem 2 (教材习题 8.3-4)

说明如何在 $O(n)$ 的时间内，对 $0$ 到 $n^3 - 1$ 区间内的 $n$ 个整数进行排序。

##### Solution

首先，将这 $n$ 个整数全部写成 $n$ 进制的形式，由于所有的整数都在 $0$ 到 $n^3 - 1$ 的区间内，所以它们都可以写作 $n$ 进制下的 $3$ 位数（可以有前导 $0$ ）。

接下来，对这个具有 $n$ 个 $3$ 位数（其中每一位数由 $0$ 到 $n - 1$ 这 $n$ 种可能）的序列调用基数排序，基数排序的内部稳定排序选用计数排序即可。

根据引理8.3（见[第7讲PPT第18页](/slides/lec07-sorting-in-linear-time.pdf#page=18)）运行时间为 $\Theta(d(n+k)) = \Theta(3(n + n)) = \Theta(n)$ 。


#### Problem 3 (教材习题 8.4-2)

解释为什么桶排序在最坏情况下的运行时间为 $\Theta(n^2)$ ？我们应该如何修改算法，使其在保持平均情况为线性时间代价的同时，最坏情况下代价为 $O(n\log n)$ ？

##### Solution

如果所有的元素都落在了一个桶中，并且在桶中是逆序的，这是我们的最坏情况，我们需要对整个长度为 $n$ 的逆序的线性表调用插入排序，时间为 $\Theta(n^2)$ 。

我们可以使用归并排序或者堆排序来代替插入排序，从而改进最坏情况的运行时间。

选择插入排序是因为它可以很好地运行在链表上，只需要常数项的额外空间。

如果选择堆排序或者插入排序，我们则需要先花 $O(n)$ 的时间将链表转化成数组，然后对数组花 $O(n\log n)$ 排序，然后花 $O(n)$ 将数组转回链表。这需要非常数项的额外空间，并且虽然这样做渐近意义上更快，但实际运行的时候可能更慢，因为到达渐近意义需要的数据规模 $n_0$ 是大的。


#### Problem 4 (教材习题 8.4-4)

在单位圆内给定 $n$ 个点， $p_i = (x_i, y_i)$ ，对所有 $i = 1, 2,\cdots , n$ ，有 $0 < x_i^2 + y_i^2 \le 1$ 。假设所有的点服从均匀分布，即在单位圆的任一区域内找到给定点的概率与该区域的面积成正比。请设计一个在平均情况下有 $\Theta(n)$ 时间代价的算法，它能够按照点到原点之间的距离 $d_i = \sqrt{x_i^2 + y_i^2}$ 对这 $n$ 个点进行排序。（提示：在 BUCKET-SORT 中，设计适当的桶大小，用以反应各个点在单位圆中的均匀分布情况。）

##### Solution

想要让桶排序的平均情况运行时间达到线性时间，需要一个条件：输入数据在概率上均匀地分布在所有的桶中。

我们的输入数据是 $n$ 个单位圆内均匀分布的点，每个桶对应着单位圆内部的一个圆环，因为到原点的距离在一定范围内的点组成的集合是一个圆环。我们需要让每个圆环的面积相等，这样单位圆内均匀分布的点才会均匀的落在每个桶中。

记从内到外的第 $i$ 个圆的半径为 $r_i$ ，则这个圆的面积应该是前 $i$ 个圆环的面积之和，即整个单位圆面积的 $i / n$ ，于是我们有

$$
\pi r_i^2 = \frac{i}{n} \pi 1^2 \Leftrightarrow r_i = \sqrt{\frac{i}{n}}
$$

因此，每个桶为 $c_i = \{(x, y) | r_{i-1} \le \sqrt{x^2 + y^2}\le r_i \}$ 。

输入数据在概率上是均匀分布在每个桶中的，因此使用桶排序就可以实现平均情况线性时间的排序了。


#### Problem 5 (教材习题 8.4-5)

定义随机变量 $X$ 的概率分布函数 $P(x)$ 为 $P(x) = Pr\{X \le x\}$ 。假设有 $n$ 个随机 $X_1, X_2, \cdots ,X_n$ 服从一个连续概率分布函数 $P$ ，且它可以在 $O(1)$ 时间内被计算得到。设计一个算法，使其能够在平均情况下在线性时间内完成这些数的排序。

##### Solution

使用桶排序。对于 $n$ 个输入数据，我们只需要构造 $n$ 个桶，使得输入数据在概率上是均匀分布在每个桶中的即可。

定义 $p_i$ 满足

$$
P(p_i) = \frac{i}{n}
$$

构造 $n$ 个桶为

$$
[p_0, p_1), [p_1, p_2), \cdots , [p_{n-1}, p_n)
$$

这样，输入数据落在任意桶 $[p_i, p_{i+1})$ 中的概率都是

$$
P(p_{i+1}) - P(p_{i}) = \frac{i+1}{n} - \frac{i}{n} = \frac{1}{n}
$$

从而桶排序算法可以在平均情况下线性时间内完成排序。

这里我们会发现，这 $n$ 个桶的大小是不一定一样的，因为分布函数不一定是线性函数（也就是输入不一定是均匀分布的）。

桶排序并不需要每个桶大小相同，只需要输入数据能够均匀地分布在每个桶中就可以了。

