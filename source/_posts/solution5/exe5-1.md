---
title: 练习 5-1 解答
date: 2023-1-22 11:12:00
description: 堆和堆排序相关的习题解答
---

#### Problem 1 (教材习题 6.1-1 和 6.1-2)

证明：含 $n$ 个元素的堆的高度为 $\lfloor\log n\rfloor$ 。

##### Solution

证明：设含 $n$ 个元素的堆的高度为 $h$ 。

考虑高度为 $h$ 的堆，它的结点数

- 最多是一个满二叉树的情况，有 $1 + 2 + \cdots + 2^h = 2^{h + 1} - 1$ 个结点；

- 最少是一个高度为 $h - 1$ 的满二叉树再多 $1$ 个元素在第 $h$ 层的情况，有 $1 + 2 + \cdots + 2^{h-1} + 1 = 2^{h}$ 个结点。

因此，我们找出了结点数和高度之间的不等式关系：

$$
n \le 2^{h+1} - 1 \Rightarrow h \ge \log(n+1) - 1 > \log n - 1
$$

$$
n \ge 2^{h} \Rightarrow h \le \log n
$$

即 $\log n - 1 < h \le \log n$ ，也就是 $h = \lfloor\log n\rfloor$ 。


#### Problem 2 (教材习题 6.1-7)

证明：当用数组表示存储 $n$ 个元素的堆时，叶结点下标分别是

$$
\lfloor n/2\rfloor + 1, \lfloor n/2\rfloor + 2, \cdots, n
$$

##### Solution

证明：根据完全二叉树的定义，叶结点的下标连续是显然的。我们只需要证明叶结点的下标最小是 $\lfloor n/2\rfloor + 1$ 即可。

假设最小的叶结点的下标是 $k$ 则

- 由于这是叶结点——没有子结点，我们有 $LEFT(k) \ge n + 1$ ，即 

$$
k \ge (n + 1) / 2 > n / 2
$$

- 由于这是最小的叶结点，则 $k - 1$ 不是叶结点，因此 $LEFT(k - 1) \le n$ ，即

$$
k \le n / 2 + 1
$$

综上，我们有 $n / 2 - 1 < k - 1 \le n / 2$ ，即 $k - 1 = \lfloor n / 2 \rfloor$ ，也就是最小的叶结点下标为 $k = \lfloor n / 2 \rfloor + 1$ 。


#### Problem 3 (教材习题 6.2-2)

参考过程 $\text{MAX-HEAPIFY}$ （见[第3讲PPT第13页](/slides/lec05-heapsort.pdf#page=13)），写出能够维护相应最小堆的 $\text{MIN-HEAPIFY}(A, i)$ 的伪代码，并比较 $\text{MIN-HEAPIFY}$ 与 $\text{MAX-HEAPIFY}$ 的运行时间。

##### Solution

<iframe src="/pseudocode/lec5/min-heapify.html" frameborder="no" marginwidth="0" width="100%" height="380px" marginheight="0" scrolling="auto"></iframe>

不难看出， $\text{MIN-HEAPIFY}$ 的运行时间和 $\text{MAX-HEAPIFY}$ 是一样的，都是 $O(h) = O(\log n)$ ，其中 $h$ 是以 $A[i]$ 为根结点的子树高度。


#### Problem 4 (教材习题 6.2-6)

证明：对一个大小为 $n$ 的堆， $\text{MAX-HEAPIFY}$ 的最坏情况运行时间为 $\Omega(\log n)$ 。（提示：对于 $n$ 个结点的堆，可以通过对每个结点设定恰当的值，使得从根结点到叶结点路径上的每个结点都会递归调用 $\text{MAX-HEAPIFY}$ 。）

##### Solution

证明：考虑情况 $A[1] = 0$ ， $A[i] = 1, 2 \le i \le n$ 。

由于 $0$ 是 $A[1..n]$ 中最小的元素，所以调用 $\text{MAX-HEAPIFY}(A, 1)$ 时，它需要和堆的每一层都交换，从而到达一个叶结点（这也是满足最大堆性质的情况下它应该在的位置）。

而堆的高度为 $\lfloor \log n \rfloor$ ，因此 $\text{MAX-HEAPIFY}$ 在最坏情况下的运行时间为 $\Omega(\log n)$ 。

> 因此，我们在[第5讲PPT第13页](/slides/lec05-heapsort.pdf#page=13)给出的 $\text{MAX-HEAPIFY}(A, 1)$ 的上界 $O(\log n)$ 是一个紧确的界。


#### Problem 5 (教材习题 6.3-2)

对于 $\text{BUILD-MAX}$ 中第 2 行的循环控制变量 $i$ 来说，为什么我们要求它是从 $\lfloor A.length / 2\rfloor$ 到 $1$ 递减，而不是从 $1$ 到 $\lfloor A.length / 2 \rfloor$ 递增呢？

##### Solution

这是因为 $\text{MAX-HEAPIFY}$ 算法的输入 $i$ 能够维护最大堆性质的前提是 $LEFT(i)$ 和 $RIGHT(i)$ 已经满足最大堆性质。从后往前迭代是因为最后的叶结点本身就是平凡的最大堆，能够满足让 $\text{MAX-HEAPIFY}$ 成立的输入条件。

基于循环不变式的算法正确性证明详见[第5讲PPT第18页](/slides/lec05-heapsort.pdf#page=18)。


#### Problem 6 (教材习题 6.3-3)

证明：对于任一包含 $n$ 个元素的堆中，至多有 $\lceil n / 2^{h+1}\rfloor$ 个高度为 $h$ 的结点。

##### Solution

证明：记高度为 $h$ 的结点有 $n_h$ 个，下面证明 $n_h \le \lceil n / 2^{h+1}\rfloor$ 。对 $h$ 进行归纳。

基础情况： $h = 0$ 时显然成立，根据[练习5-1](/solution5/exe5-1/)问题2，一个包含 $n$ 个元素的堆有 $\lceil n / 2\rceil$ 个叶结点，也就是 $n_0 \le \lceil n / 2^{0 + 1}\rceil$ 。

归纳假设：假设高度为 $n_{h-1} \lceil n / 2^h\rceil$ 。

归纳步骤：下面证明 $n_h \le \lceil n / 2^{h+1}\rceil$ 。

- 如果 $n_{h-1}$ 是偶数，则 $n_h = n_{h-1} / 2 = \lceil n_{h-1} / 2 \rceil$ ；

    - 高度为 $h$ 的结点中，每个结点都有两个孩子。

- 如果 $n_{h-1}$ 是奇数，则 $n_h = \lfloor n_{h-1} / 2 \rfloor + 1 = \lceil n_{h-1} / 2\rceil$ ；

    - 高度为 $h$ 的结点中 $n_h - 1$ 个结点有两个孩子， $1$ 个结点有一个孩子。

结合上述两种情况，我们有 $n_h = \lceil n_{h-1} / 2\rceil$ ，于是

$$
n_h = \lceil \frac{n_{h-1}}{2} \rceil \le \lceil \frac{1}{2}\cdot\lceil\frac{n}{2^{h}}\rceil \rceil = \lceil\lceil \frac{n}{2^{h + 1}} \rceil\rceil = \lceil \frac{n}{2^{h + 1}} \rceil
$$

综上， $n_h \le \lceil n / 2^{h+1}\rceil$ 。

#### Problem 7 (教材习题 6.4-2)

试分析在使用下列循环不变式时， $\text{HEAPSORT}$ （详见[第5讲PPT第21页](/slides/lec05-heapsort.pdf#page=21)）的正确性：

在算法的第 2 到 5 行 **for** 循环每次迭代开始时，子数组 $A[1..i]$ 是一个包含了数组 $A[1..n]$ 中前 $i$ 小元素的最大堆，而子数组 $A[i+1..n]$ 包含了数组 $A[1..n]$ 中已排好序的前 $n - i$ 大元素。

##### Solution

证明：采用“初始化-保持-终止”的方法来证明不变式，并说明堆排序的正确性。

初始化：第一次迭代之前，$i = n$ ，根据算法第 1 行 $\text{BUILD-MAX-HEAP}(A)$ 的正确性，显然有子数组 $A[1..n]$ 包含了数组 $A[1..n]$ 中前 $n$ 小元素的最大堆，而子数组 $A[n+1..n]$ 包含了数组 $A[1..n]$ 中已经排好序的前 $n - n = 0$ 大元素。

保持：假设迭代开始前，子数组 $A[1..i]$ 是一个包含了数组 $A[1..n]$ 中前 $i$ 小元素的最大堆，而子数组 $A[i+1..n]$ 包含了数组 $A[1..n]$ 中已排好序的前 $n - i$ 大元素。

- $A[1]$ 是 $A[1..i]$ 中的最大元素，但是比 $A[i+1..n]$ 都小，算法第3行将其与 $A[i]$ 交换，此时 $A[i]$ 比 $A[i+1..n]$ 都小且是 $A[1..i]$ 中的最大元素。而 $A[i+1..n]$ 本身是排好序的，因此，在前面多缀了一个更小元素 $A[i]$ 的 $A[i..n]$ 依旧是排好序的，且是前 $n - i + 1$ 大元素。

- 算法第 4 行将堆的大小减 1 ，得到了新的堆 $A[1..i-1]$ 。之前交换 $A[1]$ 和 $A[i]$ 的操作并没有破坏 $A[2]$ 和 $A[3]$ 在 $A[1..i-1]$ 中对应子树的最大堆性质，因此算法第 5 行的 $\text{MAX-HEAPIFY}(A, 1)$ 能够维护 $A[1..i-1]$ 的最大堆性质。同时，由于我们踢出堆的是原本前 $i$ 小的元素 $A[1..i]$ 中的最大元素，因此现在的 $A[1..i-1]$ 中是前 $i-1$ 小元素。

- 综上，下一次迭代开始前，子数组 $A[1..i-1]$ 是一个包含了数组 $A[1..n]$ 中前 $i-1$ 小元素的最大堆，而子数组 $A[i..n]$ 包含了数组 $A[1..n]$ 中已排好序的前 $n - i + 1$ 大元素。循环保持了不变式。

终止：最后一次迭代结束后，$i = 1$ ，根据循环不变式，我们有 $A[2..n]$ 包含了数组 $A[1..n]$ 中已经排好序的前 $n - 1$ 大元素，$A[1]$ 是 $A[1..n]$ 中第 1 小，也就是最小的元素。

综上，算法结束时 $A[1..n]$ 已经排好了序，堆排序算法的正确性得证。

