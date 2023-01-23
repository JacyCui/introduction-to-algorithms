---
title: 练习 5-2 解答
date: 2023-1-22 23:50:00
description: 优先队列相关的习题解答
---

#### Problem 1 (教材习题 6.5-3)

要求用最小堆实现最小优先队列，请写出 HEAP-MINIMUM 、 HEAP-EXTRACT-MIN 、 HEAP-DECREASE-KEY 、 MIN-HEAP-INSERT 的伪代码。其中，你可以直接调用 MIN-HEAPIFY （详见[练习5-1](/solution5/exe5-1/)算法1）来维护最小堆的性质。

##### Solution

<iframe src="/pseudocode/lec5/minimum-priority-queue.html" frameborder="no" marginwidth="0" width="100%" height="680px" marginheight="0" scrolling="auto"></iframe>


#### Problem 2 (教材习题 6.5-5)

试分析在使用下列循环不变式时，HEAP-INCREASE-KEY（详见[第5讲PPT第42页](/slides/lec05-heapsort.pdf#page=42)）的正确性：

在算法的第 4 到 6 行 **while** 循环每次迭代开始的时候，子数组 $A[1..A.\text{heap-size}]$ 要满足最大堆的性质。如果有违背，只有一个可能： $A[i] > A[PARENT(i)]$ 。

这里，你可以假定在调用 HEAP-INCREASE-KEY 时， $A[1...A.\text{heap-size}]$ 是满足最大堆性质的。

##### Solution

证明：采用“初始化-保持-终止”的方法来证明不变式，并说明 HEAP-INCREASE-KEY 的正确性。

初始化：第一次迭代开始前， $A$ 是一个最大堆，除非 $A[i] > A[PARENT(i)]$ ，因为算法第1-3行只是在一个原本的最大堆基础上增大了 $A[i]$ 的值，所以 $A[i]$ 依旧会比它的孩子们大，唯一可能破坏最大堆性质的就是 $A[i]$ 过于大，使得 $A[i] > A[PARENT(i)]$ 了。

保持：如果迭代开始前，$A$ 是一个最大堆，除非 $A[i] > A[PARENT(i)]$ ，根据算法第 4 行的判断条件，

- 如果 $A$ 是一个最大堆，有 $A[i] \le A[PARENT(i)]$ ，则循环终止，我们已经得到了一个最大堆。

- 如果 $A[i] > A[PARENT(i)]$ ，则进入循环体，算法第 5 行交换了 $A[i]$ 与 $A[PARENT(i)]$ 的值，此时 $A[i] < A[PARENT(i)]$ 满足最大堆性质，只不过 $A[PARENT(i)]$ 的增大可能会使得

$$
A[PARENT(i)] > A[PARENT(PARENT(i))]
$$

- 所以 $A$ 是最大堆，除非 $A[PARENT(i)] > A[PARENT(PARENT(i))]$ 。循环保持了不变式，因为根据算法第 6 行，下一次循环的 $i = PARENT(i)$ 。

终止：最后一次迭代结束时，根据不变式，$A$ 是一个最大堆，除非 $A[i] > A[PARENT(i)]$ 。

- 如果是因为 $A[i] \le A[PARENT(i)]$ 结束的迭代，根据循环不变式，我们有 $A$ 是一个最大堆；

- 如果是因为 $i = 1$ 结束的不变式，由于不存在 $PARENT(1)$ ，所以不可能 $A[1] > A[PARENT(1)]$ ，因此 $A$ 是一个最大堆。

综上，首先算法第 1 到 3 行显然增加了 $A[i]$ 的关键字值到 $key$ ，其次我们已经论证了算法的第 4 到 6 行保持了最大堆性质，因此，HEAP-INCREASE-KEY 算法在保持了最大堆性质的前提下增加了 $A[i]$ 的关键字值到 $key$ ，它是正确的。


#### Problem 3 (教材习题 6.5-6)

在 HEAP-INCREASE-KEY 的第5行的交换操作中，一般需要通过三次赋值来完成。想一想如何利用 INSERTION-SORT (见[第1讲PPT第9页](/slides/lec01-getting-started.pdf#page=9)）内循环部分的思想，只用一次赋值就完成这一交换操作？

##### Solution

和插入排序类似的思路：先腾出一个关键字为 $key$ 的元素的位置，然后再赋 $A[i] = key$ 。

<iframe src="/pseudocode/lec5/heap-increase-key.html" frameborder="no" marginwidth="0" width="100%" height="260px" marginheight="0" scrolling="auto"></iframe>


#### Problem 4 (教材习题 6.5-7)

试说明如何使用优先队列来实现一个先进先出队列，以及如何使用优先队列来实现栈？（先进先出队列和栈的定义见教材10.1节）

##### Solution

实现思路如下：

- 将元素按照优先级递减的顺序插入最大优先队列就可以实现先进先出队列了；

- 将元素按照优先级递增的顺序插入最大优先队列就可以实现栈了。

不过这种实现先进先出队列和栈的方式是不高效的（因为所有操作都是 $O(\log n)$ 的，而我们完全可以很轻松地实现 $O(1)$ 操作的先进先出队列和栈）；并且，如果优先级可以上溢或者下溢的话，我们可能还需要在优先级溢出的时候为所有元素重新分配优先级。


#### Problem 5 (教材习题 6.5-8)

$\text{HEAP-DELETE}(A, i)$ 操作能够将结点 $i$ 从堆 $A$ 中删除。对于一个包含 $n$ 个元素的最大堆，请设计一个能够在 $O(\log n)$ 时间内完成的 $\text{HEAP-DELETE}$ 操作。

##### Solution

下面给出两种可能的实现方式，复杂度都是 $O(\log n)$ 。区别是，

- 第一种直接复用已有的算法，不需要什么额外的代码，但是复杂度中的常数系数会更大一些；

- 第二种需要多写一些代码和判断逻辑，但是复杂度中的常数系数会小一些。

<iframe src="/pseudocode/lec5/max-heap-delete.html" frameborder="no" marginwidth="0" width="100%" height="380px" marginheight="0" scrolling="auto"></iframe>


#### Problem 6 (教材习题 6.5-9)

请设计一个时间复杂度为 $O(n\log k)$ 的算法，它能够将 $k$ 个有序链表合并为一个有序链表，这里 $n$ 是所有输入链表包含的总的元素个数。（提示：使用最小堆来完成 $k$ 路归并。）

##### Solution

<iframe src="/pseudocode/lec5/merge-sorted-lists.html" frameborder="no" marginwidth="0" width="100%" height="380px" marginheight="0" scrolling="auto"></iframe>

算法思路：

1. 用所有有序链表的第 1 个元素建立大小为 $k$ 的最小堆，需要 $O(k)$ 的时间；

2. 从最小堆中取出最小元素放入结果链表，需要 $O(\log k)$ 的时间；如果这个最小元素的来源链表非空，则将该链表现在的头部元素插入最小堆，需要 $O(\log k)$ 的时间；

3. 直到最小堆为空为止，一共需要重复第 2 步 $n$ 次。

综上，该算法的运行时间为 $O(n\log k)$ 。

> 其实这里不一定非得是链表，顺序表（数组的数据结构叫法）也行。如果是顺序表的话可以用下标操作来表示取走元素的操作，能够在常数项时间内完成。



