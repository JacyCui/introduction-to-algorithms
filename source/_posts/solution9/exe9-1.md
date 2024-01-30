---
title: 练习 9-1 解答
date: 2024-1-29 17:00:00
description: 栈、队列和链表相关的习题解答
---

#### Problem 1 (教材习题 10.1-4)

重写 ENQUEUE 和 DEQUEUE 的代码（见[第9讲PPT第13页](/slides/lec09-elementary-data-structures.pdf#page=13)或教材10.1节），使之能处理队列的下溢和上溢。

##### Solution

<iframe src="/pseudocode/lec9/queue-operation-handling-overflow-underflow.html" frameborder="no" marginwidth="0" width="100%" height="940px" marginheight="0" scrolling="auto"></iframe>

#### Problem 2 (教材习题 10.1-5)

栈插入和删除元素只能在同一端进行，队列的插入和删除操作分别在两端进行，与它们不同的是，有一种 **双端队列** （Deque, Double Ended Queue），其插入和删除操作都可以在两端进行。写出 $4$ 个时间均为 $O(1)$ 的过程，分别实现在双端队列的两端插入和删除元素的操作，该队列是用一个数组实现的。

##### Solution

<iframe src="/pseudocode/lec9/deque.html" frameborder="no" marginwidth="0" width="100%" height="1220px" marginheight="0" scrolling="auto"></iframe>

其中， QUEUE-EMPTY 和 QUEUE-FULL 过程见算法 1 。

#### Problem 3 (教材习题 10.1-6)

说明如何用两个栈实现一个队列，并分析相关队列操作的运行时间。

##### Solution

<iframe src="/pseudocode/lec9/two-stack-queue.html" frameborder="no" marginwidth="0" width="100%" height="350px" marginheight="0" scrolling="auto"></iframe>

其中， STACK-EMPTY 、 PUSH 和 POP 过程见[第9讲PPT第10页](/slides/lec09-elementary-data-structures.pdf#page=10)或教材10.1节。

- ENQUEUE 的运行时间为 $O(1)$ ；

- DEQUEUE 最坏情况运行时间为 $O(n)$ （其中 $n$ 是队列中的元素个数），平摊情况（Amortized）运行时间为 $O(1)$ 。

    - 平摊分析的技巧将会在第16讲介绍，读者若感兴趣可提前预习。

#### Problem 4 (教材习题 10.1-7)

说明如何用两个队列实现一个栈，并分析相关栈操作的运行时间。

##### Solution

<iframe src="/pseudocode/lec9/two-queue-stack.html" frameborder="no" marginwidth="0" width="100%" height="670px" marginheight="0" scrolling="auto"></iframe>

其中， ENQUEUE 和 DEQUEUE 过程见算法 1 。

- PUSH 的运行时间为 $O(1)$ ；

- POP 的运行时间为 $\Theta(n)$ （其中 $n$ 为栈中元素的个数）。

#### Problem 5 (教材习题 10.2-5)

使用单向循环链表实现字典操作 INSERT 、 DELETE 和 SEARCH ，并给出所写过程的运行时间。

##### Solution

<iframe src="/pseudocode/lec9/singly-circular-linked-list.html" frameborder="no" marginwidth="0" width="100%" height="530px" marginheight="0" scrolling="auto"></iframe>

- INSERT 的运行时间为 $O(1)$ ；

- DELETE 的最坏情况运行时间为 $O(n)$ ；

- SEARCH 的最坏情况运行水岸为 $O(n)$ 。

其中， $n$ 是链表中的元素个数。

#### Problem 6 (教材习题 10.2-6)

动态集合操作 UNION 以两个不相交的集合 $S_1$ 和 $S_2$ 作为输入，并返回集合 $S = S_1 \cup S_2$ ，包含 $S_1$ 和 $S_2$ 的所有元素。该操作通常会破坏集合 $S_1$ 和 $S_2$ 。试说明如何选用一种合适的表类数据结构，来支持 $O(1)$ 时间的 UNION 操作。

##### Solution

选用有哨兵的双向循环链表示，$O(1)$ 时间的 UNION 操作如下：

<iframe src="/pseudocode/lec9/union-of-circular-doubly-linked-list.html" frameborder="no" marginwidth="0" width="100%" height="200px" marginheight="0" scrolling="auto"></iframe>

#### Problem 7 (教材习题 10.2-7)

给出一个 $\Theta(n)$ 时间的非递归过程，实现对一个含 $n$ 个元素的单链表的逆转。要求除存储链表本身所需的空间外，该过程只能使用固定大小的的存储空间。

##### Solution

<iframe src="/pseudocode/lec9/reverse-singly-linked-list.html" frameborder="no" marginwidth="0" width="100%" height="280px" marginheight="0" scrolling="auto"></iframe>

> 这是一道经典的链表面试题，这里给出[LeetCode链接](https://leetcode.cn/problems/UHnkqh/description/)。


#### Problem 8 (教材习题 10.2-8)

说明如何在每个元素仅使用一个指针 $x.np$ （而不是通常的两个指针 $next$ 和 $prev$ ）的情况下实现双链表。假设所有指针的值都可视为 $k$ 位的整型数，且定义

$$
x.np = x.next \oplus x.prev
$$

即 $x.next$ 和 $x.prev$ 的 $k$ 位异或。（ $NIL$ 的值用 $0$ 表示。）

注意要说明获取表头所需的信息，并说明如何在该表上实现 SEARCH 、 INSERT 和 DELETE 操作，以及如何在 $O(1)$ 时间内实现该表的逆转。

##### Solution

先简单解释一下原理，对于异或操作，恒有 $A \oplus (A \oplus B) = B$ ，于是:

- 当我们知道 $x.prev$ 和 $x.np$ 时，很容易得出

$$
x.next = x.prev \oplus (x.prev \oplus x.next) = x.prev \oplus x.np
$$

- 类似地，当我们知道 $x.next$ 和 $x.np$ 时，很容易得出

$$
x.prev = x.next \oplus (x.next \oplus x.prev) = x.next \oplus x.np
$$

也就是说，$x.prev$ 、 $x.np$ 和 $x.next$ 三者知二求一。

比如说我知道 $L.head.prev = L.nil$ 和 $L.head.np$ 之后就可以得到 $L.head.next = L.nil \oplus L.head.np$ 了，依此类推便可遍历整个链表；想要常数项时间翻转链表也就只需要让 $L.head = L.nil.prev$ 即可，这一点也可以通过异或操作完成。

具体的算法如下：

<iframe src="/pseudocode/lec9/xor-linked-list.html" frameborder="no" marginwidth="0" width="100%" height="970px" marginheight="0" scrolling="auto"></iframe>

其中，

- SEARCH 的最坏情况运行时间为 $O(n)$ ；

- INSERT 的运行时间为 $O(1)$ ；

- DELETE 的最坏情况运行时间为 $O(n)$ ；

- REVERSE 的运行时间为 $O(1)$ 。

