---
title: 练习 9-2 解答
date: 2024-1-30 02:11:00
description: 指针、对象和有根树相关的习题解答
---

#### Problem 1 (教材习题 10.3-2)

对一组同构对象用单数组表示法实现，写出过程 ALLOCATE-OBJECT 和 FREE-OBJECT 。 

##### Solution

单数组表示法的示意图见[第9讲PPT第29页](/slides/lec09-elementary-data-structures.pdf#page=29)或教材10.3节，结合图示更容易理解下面的算法。

<iframe src="/pseudocode/lec9/single-array-allocate-free.html" frameborder="no" marginwidth="0" width="100%" height="370px" marginheight="0" scrolling="auto"></iframe>

#### Problem 2 (教材习题 10.3-5)

设 $L$ 是一个长度为 $n$ 的双向链表，存储于长度为 $m$ 的数组 $key$ 、 $prev$ 和 $next$ 中。假设这些数组由维护双链自由表 $F$ 的两个过程 ALLOCATE-OBJECT 和 FREE-OBJECT 进行管理。又假设 $m$ 个元素中，恰有 $n$ 个元素在链表 $L$ 上， $m - n$ 个在自由表上。

给定链表 $L$ 和自由表 $F$ ，试写出一个过程 COMPACTIFY-LIST$(L, F)$ ，用来移动 $L$ 中的元素使其占用数组中 $1, 2, \cdots , n$ 的位置，调整自由表 $F$ 以保持其正确性，并且占用数组中 $n + 1, n + 2, \cdots, m$ 的位置。要求所写的过程运行时间应为 $\Theta(n)$ ，且只使用固定量的额外存储空间。请证明所写的过程是正确的。

##### Solution

基本思路是通过交换元素位置的方式将 $L$ 的元素挪到前 $n$ 个位置。

<iframe src="/pseudocode/lec9/compactify-list.html" frameborder="no" marginwidth="0" width="100%" height="460px" marginheight="0" scrolling="auto"></iframe>

增量算法正确性分析找循环不变式即可，上述算法的循环不变式是：第 11 到 17 行 **while** 每次迭代开始前，$prev[1..i-1]$ 、 $key[1..i-1]$ 和 $next[1..i-1]$ 按顺序依次存储着链表 $L$ 的前 $i - 1$ 个元素， $F$ 指向自由表的表头。正确性不难理解。

#### Problem 3 (教材习题 10.4-2)

给定一个 $n$ 个结点的二叉树，写出一个 $O(n)$ 时间的递归过程，将该树每个结点的关键字输出。

##### Solution

<iframe src="/pseudocode/lec9/binary-tree-traversal-recursive.html" frameborder="no" marginwidth="0" width="100%" height="290px" marginheight="0" scrolling="auto"></iframe>

以上是二叉树递归版本的前序遍历，你可以调整算法第 5 到 7 行代码的顺序来实现中序遍历和后序遍历。

#### Problem 4 (教材习题 10.4-3)

给定一个 $n$ 个结点的二叉树，写出一个 $O(n)$ 时间的非递归过程，将该树每个结点的关键字输出。可以使用一个栈作为辅助数据结构。

##### Solution

<iframe src="/pseudocode/lec9/binary-tree-traversal-nonrecursive.html" frameborder="no" marginwidth="0" width="100%" height="320px" marginheight="0" scrolling="auto"></iframe>

以上是二叉树非递归版本的前序遍历，中序遍历和后序遍历的非递归版本就不是简单调整第 8 到 10 行代码就能实现的了，感兴趣的读者可以自行搜索相关的算法。

其中栈相关实现详见[第9讲PPT第10页](/slides/lec09-elementary-data-structures.pdf#page=10)或教材10.1节。

#### Problem 5 (教材习题 10.4-4)

对于一个含 $n$ 个结点的任意有根树，写出一个 $O(n)$ 时间的过程，输出其所有关键字。该树以左孩子右兄弟表示法存储。

##### Solution

<iframe src="/pseudocode/lec9/tree-traversal-recursive.html" frameborder="no" marginwidth="0" width="100%" height="350px" marginheight="0" scrolling="auto"></iframe>

以上是递归版本的任意有根树的前序遍历算法，读者可自行思考非递归的版本应当怎样实现。


#### Problem 6 (教材习题 10.4-5)

给定一个 $n$ 结点的二叉树，写出一个 $O(n)$ 时间的非递归过程，将该树每个结点的关键字输出。要求除该树本身的存储空间外只能使用固定量的额外存储空间，且在过程中不得修改该树，即使是暂时的修改也不允许。

##### Solution

<iframe src="/pseudocode/lec9/binary-tree-traversal-nonrecursive-with-constant-space.html" frameborder="no" marginwidth="0" width="100%" height="520px" marginheight="0" scrolling="auto"></iframe>

#### Problem 7 (教材习题 10.4-6)

任意有根树的左孩子右兄弟表示法中每个结点用到三个指针： $left\text{-}child$ 、 $right\text{-}sibling$ 和 $parent$ 。对于任何结点，都可以在常数时间到达其父结点，并在与其孩子数呈线性关系的时间内到达所有孩子结点。说明如何在每个结点中只使用两个指针和一个布尔值的情况下，使结点的父结点或者其所有孩子结点可以在与其孩子数呈线性关系的时间内到达。

##### Solution

两个指针是 $left\text{-}child$ 、 $right\text{-}sibling$ ，一个布尔值为 $right\text{-}sibling\text{-}to\text{-}parent$ ，规则如下：

- $x.left\text{-}child$ 指向 $x$ 的左子女；

- 当 $x$ 有右兄弟时， $x.right\text{-}sibling$ 指向 $x$ 的右兄弟，

$$
x.right\text{-}sibling\text{-}to\text{-}parent = \mathbf{false}
$$

- 当 $x$ 没有右兄弟时， $x.right\text{-}sibling$ 指向 $x$ 的父结点， 

$$
x.right\text{-}sibling\text{-}to\text{-}parent = \mathbf{true}
$$

于是，我们可以在与 $x$ 的孩子数呈线性关系的时间内到达 $x$ 的所有孩子结点是显然的；在与 $x$ 的孩子数呈线性关系的时间内到达 $x$ 的父结点的算法如下：

<iframe src="/pseudocode/lec9/parent.html" frameborder="no" marginwidth="0" width="100%" height="200px" marginheight="0" scrolling="auto"></iframe>

