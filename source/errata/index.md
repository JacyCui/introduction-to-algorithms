---
title: 中文版教材勘误
date: 2023-2-6 12:54:54
---

### 中文版教材勘误

> 本页是笔者在阅读中文版原书第3版教材的过程中发现的一些错误的合集（目前全部是翻译错误，英文原版没有错），罗列如下，不定期更新。


- 第 85 页第 17 行倒数第3个字：将“队”改为“堆”

- 第 88 页第 2 行：将“高度为 $h$ 的堆最多包含 $\lceil n/2^{h+1} \rceil$ 个结点”改为“堆中至多有 $\lceil n/2^{h+1} \rceil$ 个高度为 $h$ 的结点” 。

- 第 93 页习题 6.5-8 第 1 行最倒数第 2 个字：将“堆”改为“最大堆”。

- 第 93 页习题6.5-9：原书是将 $k$ 个有序的 list 合并为一个有序的 list ，list准确翻译应该是线性表，包括顺序表和链表两种，这里翻译成链表虽然题目本身依旧可做，但特化了原本的题目。

- 第 104 页上半页算法第 10 行：将 $A[j] \ge x$ 改成 $A[i] \ge x$ ，否则算法错误。

- 第 105 页习题 7-5 第 b 问：将“这一概率”改为“两种实现概率的比值”，这道题问的是平凡实现和非平凡实现下，两种概率比值的极限值；而不是题目中这种非平凡的实现的概率的极限值，这个概率值的极限是不存在的。

    - 英文版题目：Assume that $n \to \infty$ , and give the limiting ratio of these probabilities.

- 第 114 页习题 8.4-4 第 2 行第 16 个字：将“元”改为“圆”。

- 第 114 页习题 8-1 第 d 问第 1 行第 4 个字：将“d”删去。

- 第 115 页习题 8-2 第 d 问第 1 行：将“你设计的”四个字删去，英文版中没有这几个字，前面三问的算法不一定需要你自己设计，直接给书上已经有的算法就可以了。

    - 英文原文：Can you use any of your sorting algorithms from parts (a)–(c) as the sorting method used in line 2 of RADIX-SORT, so that RADIX-SORT sorts n records with b-bit keys in $O(bn)$ time? Explain how or why not.

- 第 115 页习题 8-2 第 e 问第 2 行最后：将“ $O(k)$ 使用”改成“使用 $O(k)$ ” ，翻译语序有问题。

- 第 116 页倒数第 5 行第 5 个字：将“反例”改成“逆否命题”，英文版中 contrapositive 意思是逆否命题，不是反例。

- 第 117 页习题 8-7 第 a 问：将“当 $A[q] > A[p]$ 时”中的“当”和“时”去掉，$A[q] > A[p]$ 是需要证明的结论，不是可以使用的前提条件，有了 $A[q] > A[p]$ 之后， $B[p] = 0$ 和 $B[q] = 1$ 其实就显然了。

    - 英文原文： Argue that $A[q] > A[p]$ , so that $B[p] = 0$ and $B[q] = 1$ .

- 第 120 页习题 9.1-1 ：翻译语序有问题，整道题除了“证明：”和“（提示：...）”以外的其他部分改为“可以用最坏情况下 $n + \lceil \log n \rceil - 2$ 次比较，找到 $n$ 个元素中的第二小的元素。”，这题只用证明“可以”，给出算法即可。如果像中文版中翻译的，要证明“需要”，光给出算法是不够的，还要证明没有办法更快了。

    - 英文原文：Show that the second smallest of $n$ elements can be found with $n + \lceil \log n \rceil - 2$ comparisons in the worst case.

- 第 124 页习题 9.3-4 第 2 行：要寻找的是“前” $i-1$ 小，不是“第” $i - 1$ 小；“前” $n-i$ 大，不是“第” $n - i$ 大，也就是要证明找到顺序统计量的同时可以不需要额外的比较操作就能够以这个顺序统计量为主元划分数组。

    - 英文原文：Show that it can also find the $i - 1$ smaller elements and the $n - i$ larger elements without performing any additional comparisons.



