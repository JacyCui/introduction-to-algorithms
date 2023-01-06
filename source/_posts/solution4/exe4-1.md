---
title: 练习 4-1 解答
date: 2023-1-5 23:50:00
description: 概率分析和随机算法相关的习题解答
---

#### Problem 1 (教材习题 5.1-2)

请描述 $RANDOM(a, b)$ 过程的一种实现，它只调用 $RANDOM(0, 1)$ 。作为 $a$ 和 $b$ 的函数，你的过程的期望运行时间是多少？

##### Solution

<iframe src="/pseudocode/lec4/random.html" frameborder="no" marginwidth="0" width="100%" height="300px" marginheight="0" scrolling="auto"></iframe>

算法第4到7行是利用 $RANDOM(0,1)$ 随机生成一个 $n$ 位二进制数的过程，生成每个二进制数的概率都是 $1 / 2^n$ ，算法第8到10行检查随机获得的二进制数大小是否符合要求，不难看出，这个算法的随机性是公平的。

记算法第3到11行 **while** 循环的次数为 $k$ ，则算法整体的运行时间为 $\Theta(kn)$ ，下面只需要求 $k$ 的期望值即可。

**while** 循环每次有 $(b-a+1) / 2^n$ 的概率终止， $k$ 是其终止所需的循环次数，故而不难看出 $k$ 服从参数为 $(b-a+1) / 2^n$ 的几何分布，即 $k\thicksim g((b-a+1) / 2^n)$ ，于是 $E[k] = 2^n / (b-a+1)$ 。

又因为 $n = \Theta(\log(b-a+1))$ ，所以上述算法的期望运行时间为：

$$
\Theta(kn) = \Theta(n\cdot \frac{2^n}{b - a + 1}) = \Theta(\log(b-a+1) \frac{2^{\log(b-a+1)}}{b-a + 1}) = \Theta(\log(b-a + 1))
$$

即 $\Theta(\log(b-a))$ 。


#### Problem 2 (教材习题 5.1-3)

假设你希望以 $1 / 2$ 的概率输出 $0$ 与 $1$ 。你可以自由使用一个输出 $0$ 或 $1$ 的过程 $\text{BIASED-RANDOM}$ 。它以某概率 $p$ 输出 $1$ ，概率 $1 - p$ 输出 $0$ ，其中 $0 < p < 1$ ，但是 $p$ 的值未知。

请给出一个利用 $\text{BIASED-RANDOM}$ 作为子程序的算法，返回一个无偏的结果，能以概率 $1 / 2$ 返回 $0$ ，以概率 $1 / 2$ 返回 $1$ 。作为 $p$ 的函数，你的算法的期望运行时间是多少？

##### Solution

<iframe src="/pseudocode/lec4/unbiased-random.html" frameborder="no" marginwidth="0" width="100%" height="195px" marginheight="0" scrolling="auto"></iframe>

考虑算法第2到3行两次调用得到的 $a$ 和 $b$ 的值的概率：

- $Pr\{a = 1, b = 1\} = p^2$ ，算法进入下一次循环；

- $Pr\{a = 0, b = 0\} = (1-p)^2$ ，算法进入下一次循环；

- $Pr\{a = 1, b = 0\} = p(1-p)$ ，算法返回 1 ；

- $Pr\{a = 0, b = 1\} = (1-p)p$ ，算法返回 0 ；

因此，当算法结束时，会返回一个无偏的结果。并且，每次循环有 $2p(1-p)$ 的概率算法会返回，于是循环次数服从参数为 $2p(1-p)$ 的 **几何分布** ，从而期望的循环次数为 $\frac{1}{2p(1-p)}$ 。

综上，算法2能够无偏地返回随机的 0 和 1 ，期望运行时间为 $\Theta(\frac{1}{2p(1-p)})$ 。


#### Problem 3 (教材习题 5.2-1 和 5.2-2)

在 $\text{HIRE-ASSISTANT}$ 中，假设应聘者以随机顺序出现，你正好雇佣一次的概率是多少？正好雇佣 $n$ 次的概率是多少？正好雇佣两次的概率是多少？

##### Solution

- 正好雇佣一次相当于最好的应聘者就是第一个，其概率为 $\frac{1}{n}$ ；

- 正好雇佣 $n$ 次相当于应聘者是按照质量严格递增的顺序应聘的，其概率为 $\frac{1}{n!}$ ；

- 正好雇佣两次稍微复杂一些：

    - 考虑到第一个面试的人一定会被雇佣，质量最高的人也一定会被雇佣，正好雇佣两次应该正好雇佣这两个人，且质量最高的人不能是第一个面试的人（否则就只会雇佣一个人了）。

    - 不妨设 $rank(1) = i$ （ $rank$ 含义见[第4讲PPT第6页](/slides/lec04-probabilistic-analysis-and-randomized-algorithms.pdf#page=6)），$rank(j) = n$ ，则对于所有的 $rank(x) > i$ ，都应该有 $x > j$ 。

        - 也就是说，比第一个雇佣者优秀的人都应该排在 $rank$ 为 $n$ （即质量最高）的雇佣者的后面，这样才能保证恰好雇佣两次。
    
    - 记 $rank(1) = i$ 为事件 $E_i$ ，我们不难发现， $P\{E_i\} = 1/n, 1 \le i \le n$ 。

    - 设 $rank(a_k) = i + k, k = 1, 2, ..., n - i - 1$ 。
        
        - 这里 $a_1$ 到 $a_{n - i - 1}$ 代表了所有比 $1$ 优秀但不是最优秀的人，则所有的 $a_k$ 都应该排在 $j$ 的后面。
        
        - 即 $j$ 应该排在 $a_1, a_2, ..., a_{n - i - 1}, j$ 这 $n - i$ 个应聘者组成的排列的第一个，记为事件 $F_i$ ，不难看出， $P\{F_i\} = 1 / (n - i)$ 。

    - 记第一个雇用者是 $rank$ 为 $i$ 的人时雇佣两次为事件 $T_i$ ，则从上面的分析中，可以发现 $P\{T_n\} = 0$ ，$P\{T_i\} = P\{E_i\}\cdot P\{F_i\} = \frac{1}{n}\cdot\frac{1}{n-i}, 1\le i \le n - 1$ 。

    - 记正好雇佣两次为事件 $T$ ，我们有

$$
Pr\{T\} = \sum_{i=1}^{n} Pr\{T_i\} = \sum_{i=1}^{n-1} Pr\{T_i\} = \sum_{i=1}^{n-1}\frac{1}{n}\cdot\frac{1}{n-i} =\\
\frac{1}{n}\sum_{i=1}^{n-1}\frac{1}{n-i} = \frac{1}{n}\sum_{i=1}^{n-1}\frac{1}{i} = \frac{1}{n}\Theta(\log(n-1)) = \Theta(\frac{\log n}{n})
$$


#### Problem 4 (教材习题 5.2-4)

利用指示器随机变量来解决如下的 **帽子核对问题** （hat-heck problem）： $n$ 位顾客，他们每个人给餐厅核对帽子的服务生一顶帽子。服务生以随机顺序将帽子还给顾客。请问拿到自己帽子的客户的期望数是多少？

##### Solution

记第 $i$ 个人拿到属于自己的第 $i$ 个帽子为事件 $H_i$ ，则 $Pr\{H_i\} = 1 / n$ ，因为 $i$ 会随机的拿到任何一个帽子。

记 $X_i = I\{H_i\}$ ，$X$ 为拿到自己帽子的客户的期望数，于是 $X = \sum_{i=1}^{n}X_i$ ，从而

$$
E[X] = E[\sum_{i=1}^{n}X_i] = \sum_{i=1}^{n}E[X_i] = \sum_{i=1}^{n}Pr\{H_i\} = \sum_{i=1}^{n}\frac{1}{n} = 1
$$

所以，拿到自己帽子的客户的期望数为 $1$ 。


#### Problem 5 (教材习题 5.2-5)

设 $A[1..n]$ 是由 $n$ 个不同数构成的数列。如果 $i < j$ 且 $A[i] > A[j]$ ，则称 $(i, j)$ 对为 $A$ 的一个 **逆序对(inversion)** 。（参看[作业1](/solution1/hw1/)问题4中更多关于逆序对的例子。）假设 $A$ 的元素构成 $\langle1, 2, \cdots, n\rangle$ 上的一个均匀随机排列。请用指示器随机变量来计算其中逆序对的数目期望。

##### Solution

记 $A[i] > A[j]$ 为事件 $H_{ij}$ ，由于是均匀随机排列，谁前谁后是等可能的，所以 $Pr\{H_{ij}\} = 1/2$ 。

记 $X_{ij} = I\{H_{ij}\}$ ，逆序对的总数目为 $X$ ，则显然有 $X = \sum_{i=1}^{n-1}\sum_{j=i+1}^{n} X_{ij}$ ，从而

$$
E[X] = E[\sum_{i=1}^{n-1}\sum_{j=i+1}^{n} X_{ij}] = \sum_{i=1}^{n-1}\sum_{j=i+1}^{n} E[X_{ij}] = \sum_{i=1}^{n-1}\sum_{j=i+1}^{n} Pr\{H_{ij}\}\\
= \sum_{i=1}^{n-1}\sum_{j=i+1}^{n} \frac{1}{2} = \frac{1}{2}\sum_{i=1}^{n-1}(n-i) = \frac{n(n-1)}{4}
$$

因此，期望的逆序对数目为 $n(n-1)/4$ 。


#### Problem 6 (教材习题 5.3-1)

熊大教授不同意引理5.5证明（见[第4讲PPT第19页](/slides/lec04-probabilistic-analysis-and-randomized-algorithms.pdf#page=19))中使用的循环不变式。他对第1次迭代之前循环不变式是否为真提出质疑。他的理由是，我们可以很容易宣称一个空数组不包含0排列。因此，一个空的子数组包含一个0排列的概率是0，从而第1次迭代之前循环不变式无效。

请重写算法 $\text{RANDOMIZE-IN-PLACE}$ ，使得相关循环不变式适用于第1次迭代之前的非空子数组，并为你的算法修改引理5.5的证明。

##### Solution

将原本第1次循环单独提出来做，作为“初始化”，然后把原本的第2次循环当成现在的第1次循环，从它开始“保持”即可。这样就解决了空数组是否包含 $0$ 排列的模糊问题。

<iframe src="/pseudocode/lec4/randomize-in-place.html" frameborder="no" marginwidth="0" width="100%" height="180px" marginheight="0" scrolling="auto"></iframe>

修改引理5.5的证明中“初始化”的部分：

- 初始化：第一次循环开始前， $i = 2$ ，对于每个可能的 $1$ 排列（一共有 $n$ 种）， $A[1]$ 包含其中任意一种的概率为 $1 / n$ ，不变式成立。

原证明的其余部分都不变。


#### Problem 7 (教材习题 5.3-2)

熊二教授决定写一个过程来随机产生除恒等排列（identity permutation）外的任意排列。他提出了如下算法：

<iframe src="/pseudocode/lec4/permute-without-identity.html" frameborder="no" marginwidth="0" width="100%" height="160px" marginheight="0" scrolling="auto"></iframe>

这个算法实现了熊二教授的意图吗？

##### Solution

这个算法并没有实现熊二教授的意图。

反例：$A = [1, 2, 3]$ ，算法3不可能产生排列 $[3, 2, 1]$ ，因此算法3无法产生除恒等排列外的任意排列。


#### Problem 8 (教材习题 5.3-4)

熊翠花教授建议用下面的过程来产生一个均匀随机排列：

<iframe src="/pseudocode/lec4/permute-by-cyclic.html" frameborder="no" marginwidth="0" width="100%" height="300px" marginheight="0" scrolling="auto"></iframe>

请说明每个元素 $A[i]$ 出现在 $B$ 中任何特定位置的概率是 $1 / n$ 。然后通过说明排列结果不是均匀随机排列，表明熊翠花教授错了。

##### Solution

算法3相当于将原排列随机循环右移了 $offset$ 位，对于某个 $A[i]$ ，如果它出现在特定的 $B[j]$ 位置，说明 $j - i \equiv offset \pmod{n}$ ，其中 $offset$ 是 $1$ 到 $n$ 之间的随机数，$j - i$ 是一个特定的值。因此该事件发生的概率为 $1 / n$ 。

算法3不可能产生均匀随机排列，考虑 $A = [1, 2, 3]$ ，算法3无法产生 $B = [3, 2, 1]$ ，因此算法3的排列结果不是均匀随机排列。

> 这个问题告诉我们，原本的每个元素都等可能地出现在新排列中的任何特定位置并不意味着排列结果就是均匀随机排列了。因为各个元素之间是相互影响的，一个萝卜占了一个坑之后另外的萝卜就不能占这个坑了。

