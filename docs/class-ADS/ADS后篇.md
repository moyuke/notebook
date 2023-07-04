---
title: ADS后篇
date: 2023-07-01
tags: class
---

# NP完全

* NP完全问题：找不到多项式算法，也无法证明不存在多项式时间算法
  * 最短路径判定版本
  * 哈密顿圈
  * 3-CNF可满足性问题
* P: 能在多项式时间O($ n^k $) 内解决的问题
* NP: 不能在多项式时间内解决或不确定能不能在多项式时间内解决，但能在多项式时间验证（检验一组解是否满足）的问题，P$\subseteq $NP
* NPC: NP完全问题，所有NP问题在多项式时间内都能约化(Reducibility)到它 的NP问题，即解决了此NPC问题，所有NP问题也都得到解决。
* NP hard: NP难问题，所有NP问题在多项式时间内都能约化(Reducibility)到它 的问题(不一定是NP问题)。
  * 先证明它至少是一个NP问题，再证明其中一个已知的NPC问题能约化到它（由约化的传递性，则NPC问题定义的第二条也得以满足；至于第一个NPC问题是怎么来的，下文将介绍），这样就可以说它是NPC问题了。
  * 已知的NPC：SAT问题，Vertex cover，TSP判定版本（求最短回路的是NPhard但不是NPC，一般说TSP都指的是NPC的TSP）
* ![img](https://img-blog.csdn.net/20151015164207766)
* reduction(规约)：如果能找到这样一个变化法则，对任意一个程序A的输入，都能按这个法则变换成程序B的输入，使两程序的输出相同，那么我们说，问题A可约化为问题B。
* x在多项式时间规约到y （x $ \leq_p $y）

* 例子：

  * 停机问题
  * 最短路问题
    * (G,s,t,k)：s到t是否有＜=k长的路径
    * decision问题 -> 等价于一个集合
      * instance:<G,s,t,k>  -> String
  * 3-CNF问题
    * satisfability问题（SAT）
    * 对一组赋值，证明可满足
    * 3-SAT：有k个clause，the MAX-3SAT problem is to find a truth assignment that satisfies as many clauses as possible.
      * 每一个clause都是 a || b || c 的形式
    * B() is an efficient verifier(验证器) for problem X if
      * B为多项式时间算法
      * P() is a poly function且满足对任意s，s属于X当且仅当存在string t使得B(s,t) = yes，其中|t|<=P(|s|)
    * B(s,t)：在t下计算s，若s满足，返回yes
    * 只要求存在性，yes-certificate
  * 哈密顿圈（HCP）
    * hint：一组圈
    * B：按照hint走一遍，检查是否每个点都走了一次
  * Travelling Salesman Problem（TSP）
    * 给一张完全图G和整数k，问是否存在简单环使得每个点走一次且cost<=k
    * HCP $ \leq_p $TSP
      * 补成完全图，原来的边设为1，补上的边设为2，若HCP成立，则TSP的k取为|v|即可
      * 实例的转化为多项式时间
  * 最大团问题（clique problem）
    * 给出G和k
    * 问是否能选出至少k个点使得两两之间都有边相连（为团）
  * 顶点覆盖问题（vertex cover problem）
    * 给出G和k
    * 是否有一个点集保证每条边至少有一个端点被选中
    * clique problem $ \leq_p $ vertex cover problem
      * 边集互补
      * 点集C在G里是团当且仅当在V-C在G'里是顶点覆盖

* 题目：

  * 1.If L1 ≤p L2 and L2∈NP, then L1∈NP.
    T
    注意<=p等价于reduce to，复杂的如果是Np，那么简单的也是NP

    2.All NP-complete problems are NP problems.
    T

    3.All the languages can be decided by a non-deterministic machine.
    F
    不确定图灵机可以用来验证NP问题的解是否是正确的，确定图灵机可以用来求解P问题。

    NP hard问题无法通过不确定图灵机验证

    4.All NP problems can be solved in polynomial time in a non-deterministic machine.
    T

    5.If a problem can be solved by dynamic programming, it must be solved in polynomial time.
    F

    0-1背包问题可以用DP解，但是复杂度不是多项式的, 原因是输入的数据不是多项式的。

    6.Among the following problems, __ is NOT an NP-complete problem.

    A.Vertex cover problem

    B.Hamiltonian cycle problem

    C.Halting problem

    D.Satisfiability problem

    D SAT问题是第一个被证明的NPC问题，A是NPC问题，B是汉密尔顿回路，NPC问题。C停机问题是不可解的，选C

    7.Suppose Q is a problem in NP, but not necessarily NP-complete. Which of the following is FALSE?

    A.A polynomial-time algorithm for SAT would sufficiently imply a polynomial-time algorithm for Q.

    B.A polynomial-time algorithm for Q would sufficiently imply a polynomial-time algorithm for SAT.

    C.If Q ∉P, then P≠NP.

    D.If Q is NP-hard, then Q is NP-complete.

    看上面的图，SAT是NPC问题，如果解决了，可以解决所有NP问题

    B， Q不一定是NPC的，所以不对，C，如果Q不是P，那么说明NP没有被解决，D，NP-hard和NP交集是NPC

    8.A language L belongs to NP iff there exist a two-input polynomial-time algorithm A that verifies language L in polynomial time.

    T， 这是ppt上的

    9.Given that problem A is NP-complete. If problem B is in NP and can be polynomially reduced to problem A, then problem B is NP-complete.

    B<= A，但是A是NPC问题，A<=B才能说明B也是NPC问题。

    10.All decidable problems are NP problems.

    F，还有NP hard问题

    11.All NP problems are decidable.

    T, 可以通过不确定图灵机判断

    12.To prove problem B is NP-complete, we can use a NP-complete problem A and use a polynomial-time reduction algorithm to transform an instance of problem B to an instance of problem A.

    F, 应该不是一个实例，而是整个问题

    13.If P = NP then the Shortest-Path (finding the shortest path between a pair of given vertices in a given graph) problem is NP-complete.

    T, P=NP说明所有的NP问题均可解，所有的NPC问题可解，NP=NPC

# 近似

* 近似比：

  * max(A(I)/opt(I) , opt(I)/A(I)) <= $ \rho $(|I|)，则称其为$\rho$(n)近似的算法

* A polynomial-time approximation scheme(PTAS)

  * PTAS：关于n为多项式
  * FPTAS：关于1/ϵ也为多项式

* 例子：

  * Binpack problem（NPhard）

    * input：n items with sizes s1~sn
    * output：用尽可能少的箱子装（箱子容量固定）
    * Next fit：顺序装，装不下封箱下一个
      * NF用的箱子数，opt最优解箱子数
      * NF/opt <= 2：近似比
      * 2-approximation算法
    * Any fit：for一遍，当前打开的箱子可以装就装，不能就开一个新的
      * First fit：找第一个
      * Best fit：找装的最满的
      * BF(I)&FF(I) <= 1.7opt(I)，即近似比为1.7
        * 绝对近似比
    * First/Best fit decreasing:
      * 先对item排序
      * BFD(I)&FFD(I) <= 11/9 opt(I) + 6/9
        * 渐进近似比为11/9
        * 绝对近似比，在 opt(I) 取2时得，为1.5
    * NP复杂度最优近似比1.5，要求online则最优5/3

  * Knapsack problem(背包问题)

    * Input：n items (v1,w1)~(vn,wn)，容量C
    * output：最大化总价值的背包装法
      * O(nC)或O(nV_sum)，伪多项式
    * 分数版本：可以选零点几个物品
      * 按性价比贪心
    * 整数版本（NPhard）
      * 贪心算法
        * on vi/wi（性价比）
          * 被小物件卡，选不了高价值大物件
          * OPT/A>=(C-1)/2
        * on vi（价值）
          * 被大物件卡，选不了高性价比小物件
          * OPT/A>=C-1
        * 两种算法存在缺点，但互补
      * A*：A1和A2各跑一遍选最优
        * A1 >= OPT_分数版本 - Vmax
        * A2 >= Vmax
        * 则2A* >= OPT_frac >= OPT
        * A* >= OPT/2
      * 优化：所有v除以一个d
        * 原本O($n^2V_{sum}$)
        * d=gcd(v1...vn)，则不影响结果
        * d= $ \lceil nV_{sum}/\delta\rceil$ ，则O($ n^3 / \delta $)
        * 求出近似比为$ 1/1-\delta $ 
    * K-center problem
      * Input：n site s1...sn，整数k
      * output：找到k个center，盖住所有sites并使得半径最小
      * dist(x,c)=$min_{y\sub C}$ (dist(x,y))
      * k=1：随便选一个site作为center，近似比为2
      * 已知最优解：
        * 若存在未覆盖site，选为site，然后去掉覆盖的site
        * 循环最多进行k次
        * 所以假定一个解（二分）
      * 贪心
        * 选一个site作为center
        * 一直选择距离center最远的site作为新的center
        * 得到最终的center集合Ck
        * r(Ck)<=2r*

  * 题目：

    * 1.Suppose ALG is an α-approximation algorithm for an optimization problem Π whose approximation ratio is tight. Then for every ϵ>0 there is no (α−ϵ)-approximation algorithm for Π unless P = NP.
      F, 按照我的理解，可能会有近似比更小的算法。

      2.As we know there is a 2-approximation algorithm for the Vertex Cover problem. Then we must be able to obtain a 2-approximation algorithm for the Clique problem, since the Clique problem can be polynomially reduced to the Vertex Cover problem.
      T， reduce to 就算<=，如果CP<=VC, VC有近似比为2的算法，那么CP也有

      3.For the bin-packing problem: let S=∑Si. Which of the following statements is FALSE?

      A.The number of bins used by the next-fit heuristic is never more than ⌈2S⌉

      B.The number of bins used by the first-fit heuristic is never more than ⌈2S⌉

      C.The next-fit heuristic leaves at most one bin less than half full

      D.The first-fit heuristic leaves at most one bin less than half full

      NF近似比是2，其他的近似比都比2小。Next fit可能有多个半空的bit，因为如果永远往前放，不会回头放之前的，所以是C，而FF会检查之前所有位，因此如果有两个半空的，它们会放在一起。

      4.To approximate a maximum spanning tree T of an undirected graph G=(V,E) with distinct edge weights w(u,v) on each edge (u,v)∈E, let’s denote the set of maximum-weight edges incident on each vertex by S. Also let w(E′)=∑(u,v)∈E′， w(u,v) for any edge set E′. Which of the following statements is TRUE?

      A.S=T for any graph G

      B.S≠T for any graph G

      C.w(T)≥w(S)/2 for any graph G

      D.None of the above

      C, 题目的意思是，如果把每个点最大权值的边加入一个集合，那么这个集合的权值和最大生成树权值之比是多少。注意，点的最大权值边集合意味着集合里相同的边最多出现一次。

      很容易证明，S里面不存在环，因此T一定包含S.所以w(T)>=w(S)

      假如存在环，设边为e1,e2,e3,…ej, 点为p1, …pj

      由于e1在S中，因此w(e1)>w(ej)，由于e2在S中，因此w(e2)>w(e1),…，最后得到的是w(ej)>w(e1)，矛盾。

      5.Assume that you are a real world Chinese postman, which have learned an awesome course “Advanced Data Structures and Algorithm Analysis” (ADS). Given a 2-dimensional map indicating N positions pi(xi ,yi) of your post office and all the addresses you must visit, you’d like to find a shortest path starting and finishing both at your post office, and visit all the addresses at least once in the circuit. Fortunately, you have a magic item “Bamboo copter & Hopter” from “Doraemon”, which makes sure that you can fly between two positions using the directed distance (or displacement).

      Bamboo.jpg (“Bamboo copter & Hopter”, japan12.com/bamboo-copter-hopter)

      However, reviewing the knowledge in the ADS course, it is an NPC problem! Wasting too much time in finding the shortest path is unwise, so you decide to design a 2−approximation algorithm as follows, to achieve an acceptable solution.

      Compute a minimum spanning tree T connecting all the addresses.
      Regard the post office as the root of T.
      Start at the post office.
      Visit the addresses in order of a _____ of T.
      Finish at the post office.
      There are several methods of traversal which can be filled in the blank of the above algorithm. Assume that P≠NP, how many methods of traversal listed below can fulfill the requirement?

      Level-Order Traversal
      Pre-Order Traversal
      Post-Order Traversal

      A.0

      B.1

      C.2

      D.3

      C，不知道题目再说什么

      6.An approximation scheme that runs in *O*(*n*^2/*ϵ*) for any fixed *ϵ*>0 is a fully polynomial-time approximation scheme.

      T, 如果1/ϵ也是多项式级别的，那么就算是full

      7.An approximation scheme that runs in *O*(*n*^2 3^*ϵ*) for any fixed *ϵ*>0 is a polynomial-time approximation scheme.

      T, 只要是n是多项式级别的就可以。

      8.In the bin packing problem, we are asked to pack a list of items L to the minimum number of bins of capacity 1. For the instance L, let FF(L) denote the number of bins used by the algorithm First Fit. The instance L′ is derived from L by deleting one item from L. Then FF(L′) is at most of FF(L).

      F, 如果是NF则是F, yds说的。

      9.For the 0-1 version of the Knapsack problem, if we are greedy on taking the maximum profit or profit density, then the resulting profit must be bounded below by the optimal solution minus the maximum profit.

      Popt<Pfrac<Pgre+pmax，最优解一定小于物体可分情况下的解。而物体可分情况下的解，可以看成greedy的解+一部分不完整的物体。不完整的物体权值一定小于最大权值。

      (感觉证明有问题)

      10.An (1+ϵ)-approximation scheme of time complexity (n+1/ϵ)^3 is a PTAS but not an FPTAS.

      F

# 外部排序

1.Suppose we have the internal memory that can handle 12 numbers at a time, and the following two runs on the tapes:

Run 1: 1, 3, 5, 7, 8, 9, 10, 12

Run 2: 2, 4, 6, 15, 20, 25, 30, 32

Use 2-way merge with 4 input buffers and 2 output buffers for parallel operations. Which of the following three operations are NOT done in parallel?

(3分)

A.1 and 2 are written onto the third tape; 3 and 4 are merged into an output buffer; 6 and 15 are read into an input buffer

B.3 and 4 are written onto the third tape; 5 and 6 are merged into an output buffer; 8 and 9 are read into an input buffer

C.5 and 6 are written onto the third tape; 7 and 8 are merged into an output buffer; 20 and 25 are read into an input buffer

D.7 and 8 are written onto the third tape; 9 and 15 are merged into an output buffer; 10 and 12 are read into an input buffer

工作原理：buffer 一个一个按顺序被写。两个run轮流对buffer进行写。

需要注意的是：如果之前有没有merge完成的，比较复杂，需要等待。

一共4+2个buffer, 内存有12个数，因此每个buffer2个数。六个buffer,后两个是输出的

![image-20230625194217783](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230625194217783.png)

![image-20230625194259189](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230625194259189.png)

这题A描述的是3->4, B描述的是4->5，C描述的是5->6, D错在不是9和15 merge, 9和10 merge
