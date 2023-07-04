---
title: DB后篇
date: 2023-06-20
tags: class
---

## 物理存储

* 分类：

  * 易失存储 volatile storage 
  * 非易失存储 non-volatile storage 
  * ![image-20230607021440123](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230607021440123.png)
  * NVM（non-volatile memory）: 掉电不丢

  * **primary storage**: Fastest media but volatile (cache, main memory).

  * **secondary storage**: next level in hierarchy, non-volatile, moderately fast access time

    also called **on-line storage** 

    E.g. flash memory, magnetic disks

  * **tertiary storage:** lowest level in hierarchy, non-volatile, slow access time

    also called **off-line storage** 

    E.g. magnetic tape, optical storage

* 磁盘 magnetic disks

  * tracks(磁道)  sectors(扇区)

  * Access Time 访问时间，毫秒级

    * Seek Time 寻道时间：找到对应磁道
    * Rotational latency 旋转延迟：转到对应扇区

  * Data-transfer rate 数据传输率

  * *数据库传输以block为单位* 

  * 访问模式：

    * Sequential access pattern(顺序访问模式)
      Successive requests are for successive disk blocks
      Disk seek required only for first block

    * Random access pattern（随机访问模式）
      Each access requires a seek
      *Transfer rates are low since a lot of time is wasted in seeks* 

      *尽量转化为顺序访问模式* 

    * I/O operations per second (IOPS ，每秒I/O操作数)

      * 衡量磁盘访问速度
      * Number of random block reads that a disk can support per second
        50 to 200 IOPS on current generation magnetic disks

  * Mean time to failure (MTTF，平均故障时间)

    * 衡量磁盘可靠性
    * the average time the disk is expected to run continuously without any failure

* 磁盘块访问的优化

  * Buffering 缓存: in-memory buffer to cache disk blocks

  * Read-ahead(Prefetch): Read extra blocks from a track in anticipation that they will be requested soon

  * **Disk-arm-scheduling** algorithms re-order block requests so that disk arm movement is minimized 

  * File organization：将碎片化的文件重新整理
    Allocate blocks of a file in as contiguous a manner as possible
    Allocation in units of extents(盘区）

  * Nonvolatile write buffers （非易失性写缓存）

    speed up disk writes by writing blocks to a non-volatile RAM buffer immediately

  * Log disk（日志磁盘）

    a disk devoted to writing a sequential log of block updates
    Used exactly like nonvolatile RAM

* Flash Storage

  * NAND flash
    * Page can only be written once
      Must be erased to allow rewrite
  * SSD(Solid State Disks) 
    * ![image-20230607024602936](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230607024602936.png)
    * SSD比磁盘快百倍，磁盘能耗高（机械运动）更新为即席写入
  * Flash storage 中的地址映射漂移，已达成磨损均衡（wear leveling)
  * ![image-20230607024919201](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230607024919201.png)
  * 对于大数据，热数据（常访问）放在SSD，冷数据放在磁盘里

* NVM，又称Storage Class Memory

  * ![image-20230607025337181](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230607025337181.png)
  * Persistence可以看出是否易失
  * NVM和SSD与硬盘不同，用字节寻址

* 随堂测试：

  * Which physical storage media is non-volatile?

    多选题 (1 分) 

     A.cache

     B.main memory

     C.flash memory

     D.magnetic disk

     E.SSD(State Solid Disk)

     F.magnetic tapes

     G.optical disk

    正确答案: C D E F G

  * Which physical storage medias belong to the secondary storage? 

    多选题 (1 分)

     A.cache

     B.main memory 

     C.flash memory

     D.SSD(Solid State Disk)

     E.magnetic disk

     F.magnetic tapes

     G.optical disk

    正确答案: C D E

  * Which term represents the time that the disk controller takes to reposition the disk arm over the correct track.

    单选题 (1 分)

     A.access time

     B.seek time

     C.rotational latency

     D.data-transfer rate 

    正确答案: B

  * What is the right approach to  optimizing  data access of disks?

    多选题 (1 分)

     A.Buffering

     B.Read-ahead

     C.defragment the file system

     D.Non-volatile write buffers

     E.Log disk

    正确答案: A B C D E

  * MTTF means    1   (注意：每个单词首字母大写).

    填空题 (1 分) (请按题目中的空缺顺序依次填写答案)

    正确答案: Mean Time To Failure

  * IOPS  means     1   (注意：每个单词首字母大写).

    填空题 (1 分) (请按题目中的空缺顺序依次填写答案)

    正确答案: I/O Operations Per Second

## 数据存储结构

* 数据库文件存在磁盘里，文件由记录(record)组成，record由各个字段(field)组成
* 定长记录(Fixed-Length Record)，可以计算每个block可以放多少记录
  * 存record i：若长n byte，从n*(i-1) byte开始
  * 删除：不移动 record，记为空记录
    * 空记录设指针指下一个空的record
    * 头部加上header指向第一条空记录
* 不定长记录(Variable-Length Record)
  * 原因：有不定长字符串，有空字段
  * 方法：不定长的全放后面，用(offset,length)记录位置和长度
  * ![image-20230607031402403](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230607031402403.png)
  * Null bitmap：有几个属性就有几位，0表示非空，1表示空
  * ![image-20230607032222398](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230607032222398.png)
  * 插入：指针+长度存记录位置，在free space从后往前插入
  * 删除：相对地址，block_num + index

* Record组织规则：
  * 堆：
    * ![image-20230607033306769](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230607033306769.png)
    * 维护空闲块的map，记录空闲程度：7即7/8的空闲
  * 顺序 Sequential
    * 插入：插到中间会导致后面的记录全体后移，因此直接放在最后，通过指针串联
      * 每个一段时间按顺序重整（克服碎片化）
  * B+树
  * 哈希
* 存放方式：
  * 按行存放
  * 按列存放：cache命中率高
* 缓存管理 Buffer manager
  * 缓存替换：
    * LRU策略（Least Recently Used）最近最少用到
    * ![image-20230607035017615](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230607035017615.png)
    * 在for循环等场景，LRU可能是一种坏策略
  * 若访问的block不在缓存，读出到缓冲区
  * 访问请求时，钉在(pin)缓冲区，请求为读时加共享锁，写时加exclusive lock

* 随堂测试：

  * What is contained in the header of slotted page? 

    多选题 (1 分)

     A.number of record entries

     B.end location of free space in the block

     C.location of each record

     D.size of each record

     E.primary key of each record

    正确答案: A B C D

  * What kind file organization is suitable for applications that require sequential processing of the entire file? 

    单选题 (1 分)

     A.heap file organization

     B.sequential file organization

     C.multitable clustering file organization

     D.hash file organization

    正确答案: B

  * Which statement is incorrect?

    多选题 (1 分)

     A.For heap file organization, records can be placed anywhere in the file where there is free space.

     B.Database system seeks to minimize the number of block transfers between the disk and memory. 

     C.If the needed block is not in the buffer, the buffer manager will replace some other block, if required, to make space for the new block.

     D.LRU is the most suitable replacement strategy for buffer manager in any cases.

    正确答案: D

  * For the buffer manager, there are following assumptions:

    • There are 4 buffer pages.

    • Initially the buffer is empty occupied.

    • The data access sequence is 1,2,3,4,5,4,3,2,1,3,5

    According to the LRU replacement strategy, there are    1    times replacements occurred,  and the data item    2    is the least recently used after completing the above data access sequence.

    填空题 (1 分) (请按题目中的空缺顺序依次填写答案)

    正确答案:

    1：3

    2：2

## 索引Indexing

* Form：search key - pointer

* Query type

  * Point query: records with a specified value in the attribute

  * Range query: records with an attribute value falling in a specified range of values.

* Primary index 主索引

  * ![image-20230610160436673](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230610160436673.png)
  * candidate key唯一情况下用起来方便

* Secondary Indices

  * ![image-20230610160508100](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230610160508100.png)
  * 不唯一，中间的指针指向多个目标
  * 

* Dense index：Index record appears for every search-key value in the file. 

  * ![image-20230610160725335](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230610160725335.png)

* Sparse index：contains index records for only some search-key values.

  * ![image-20230610160742907](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230610160742907.png)
  * ![image-20230610160938171](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230610160938171.png)

* Multilevel Index（多级索引）

  * 索引的索引
  * ![image-20230610161015946](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230610161015946.png)

* B+ Tree Index

  * 每个节点都和block大小一样
  * ![image-20230610161325306](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230610161325306.png)
  * 叶子结点就是末级索引，之间用指针相连，使连续
  * 高度：$ log_{n}(k)<= height <=log_{n/2}(k/2)+1 $，向上取整（根节点最小两叉）
  * 大小：最大：半满，最小：全满
  * 和ADS不同：每个节点容量相等，非叶子和叶子一样（ADS里非叶子最多阶数-1）
    * 也就是说中间结点的分叉数比叶子结点值数多1
  * 作用：叉数多，层数少，减少seek&block transfer次数

* 估计 height & size

  * person( pid char(18) primary key,  

    ​			name char(8), 

    ​			age smallint,
    ​             address char(40)); 

    Block size : 4K
    1000000 persons

  * Records per block =  4096/(18+8+2+40) =60.235=60

    * record 大小根据各个属性类型算

  * blocks for storing 1M persons= 1000000/60 =16667

    * 计算block数

  * B+ tree n(fan-out)  = (4096-4)/(18+4) +1 = 187

    * B+树一个节点就是一个block，存放M个值和M+1个指针

      即使是叶子结点，也多出一个指向下一个叶子的指针

      指针比值多一个，所以先-4，后+1

    * 一个索引项=索引值+指针(假设4byte)=18+4

    * 最大187叉，最少 n/2 = 94叉

    * 能索引多少值

      * 2 levels:  min=2`*`93 = 186            max= 187'`*`186 = 34,782

      * 3 levels:  min=2`*`94`*`93 = 17484        max=187`*`187`*`186 = 6,504,234

      * 4 levels:  min=2`*`94`*`94`*`93 = 1,643,496

        ​			   max=187`*`187`*`187`*`186 = 1,216,291,758

    * 易得这个B+树为3层

  * size：

    * 最小（全满）100000/186+100000/186/187+1
    * 最大（半满）100000/93+100000/93/94+1

* Bottom-up B+ Tree Build

  * ![image-20230610171021418](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230610171021418.png)
  * fanout = 4，则阶数为3
  * 先排序，按序分块，然后向上构建
  * 构建上图B+树 cost：1 seek + 9 block transfer
  * 插入大量值/合并树可以直接把叶子merge并排序，然后重建
  * ![image-20230610171558671](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230610171558671.png)
  * 原树的叶子读取：1 seek+6 block transfer

* Indexing in Main Memory

  * Random access in memory 
    * Much cheaper than on disk/flash, but still expensive compared to cache read
    * Binary search for a key value within a large B+-tree node results in many **cache misses**
    * Data structures that make best use of cache preferable – **cache conscious**
  * Cache miss
    * HD以block为单位读到buffer，buffer以64byte(例)为单位读到cache，大节点就会读不全，查找索引值过程中读取的cache只有小部分有用，没找到->产生miss
    * 降低miss：
      * 小节点：B+ trees with small nodes that fit in cache line are preferable to reduce cache misses
      * 指针和search key分开排
      * 建立一个“路标”（一棵小树）
  * Key idea:  
    * use large node size to optimize disk access, 
    * but structure data within a node using a tree with small node size, instead of using an array, to optimize cache access.

* LSM tree(Log Structured Merge) 写优化的树结构

  * ![image-20230610175401820](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230610175401820.png)
  * Benefits of LSM approach
    Inserts are done using only sequential I/O operations 随机写->顺序写
    Leaves are full, avoiding space wastage
    Reduced number of I/O operations per record inserted as compared to normal B+-tree (up to some size)
  * Drawback of LSM approach
    Queries have to search multiple trees
    Entire content of each level copied multiple times

* LSM-Stepped Merge Index

  * ![image-20230610175540871](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230610175540871.png)
  * 内存满了直接写到下一层来，disk中这一层满了再merge写到下一层
  * 删除：插入删除标记
  * 更新：删除+插入

* Buffer Tree

  * ![image-20230619143817724](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230619143817724.png)

* 随堂测试

  * 1.Indexing mechanisms are used to speed up access  to desired data.

    判断题 (1 分)

     A.Yes

     B.No

    正确答案: A

  * 2.Range query returns records with an attribute value falling in a specified range of values.

    判断题 (1 分)

     A.Yes

     B.No

    正确答案: A

  * 3.Secondary index is an index whose search key specifies an order same as the sequential order of the file. 

    判断题 (1 分)

     A.Yes

     B.NO

    正确答案: B

  * 4.In an dense index, index record appears for every search-key value in the file. 

     判断题 (1 分)

     A.Yes

     B.No

    正确答案: A

  * 5.In a B+-tree , all paths from root to leaf are of the same length.

     判断题 (1 分)

     A.Yes

     B.No

    正确答案: A

  * 6.If the root of a B+-tree is not a leaf, it has at least 2 children.

     判断题 (1 分)

     A.Yes 

     B.No

    正确答案: A

  * 7.In databases, a node of a B+-tree is generally the same size as a disk block.

     判断题 (1 分)

     A.Yes

     B.No

    正确答案: A

  * 8.The leaf nodes of a B+-tree file organization store records, instead of pointers to records.

     判断题 (1 分)

     A.Yes

     B.No

    正确答案: A

  * 9.Benefits of LSM approach:

     多选题 (1 分)

     A.Inserts are done using only sequential I/O operations

     B.Leave nodes are full, avoiding space wastage

     C.Reduced number of I/O operations per record inserted as compared to normal B+-tree.

     D.Queries have to search multiple trees

     E.Entire content of each level copied multiple times

    正确答案: A B C

  * 10.Bitmap indices are useful for queries on multiple attributes,not particularly useful for single attribute queries.

    判断题 (1 分)

     A.Yes

     B. No

    正确答案: A

## 查询处理Query Processing

* Basic Steps in Query Processing

  * Parsing and translation
    translate the query into its internal form.  This is then translated into relational algebra.
    Parser checks syntax, verifies relations
  * Optimization
    Amongst all equivalent evaluation plans choose the one with lowest cost. 
  * Evaluation
    The query-execution engine takes a query-evaluation plan, executes that plan, and returns the answers to the query.
  * <img src="C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230612001751736.png" alt="image-20230612001751736" style="zoom:33%;" />
  * ![image-20230612003553870](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230612003553870.png)
  * 选择运算尽量先做（往下推）

* 衡量Query

  * $ t_s $：number of seek

  * $ t_t $：number of block transfer(read & write)

  * Cost for b block transfers plus S seeks

    b *  $ t_t $ + S * $ t_s $

  * ![image-20230612004605830](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230612004605830.png)

  * ![image-20230612004618669](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230612004618669.png)

  * ![image-20230612004920316](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230612004920316.png)

* 对select的条件进行排序：外部排序

  * ![image-20230618161811420](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230618161811420.png)
  * ![image-20230618161824886](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230618161824886.png)
  * 性能：
  * ![image-20230618161847075](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230618161847075.png)
  * $ (b_r/M) $ 为归并段数，$ log_{M-1}(b_r/M) $ 为轮次，2br为每次的传输消耗，最后一次+br，如果要写回磁盘就+2br。
  * ![image-20230618163335699](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230618163335699.png)
  * 外部排序（External Merge Sort） 中，给一个段run分配bb 块（而不是1块）作为缓冲，可以减少每轮合并（merge）的seek次数，但也可能增加merge的轮数。对于确定的关系大小br 和确定的内存块数M，理论上应该有一个最佳的bb取值，使得算法代价最小。
  * ![image-20230618163544585](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230618163544585.png)
  * ![image-20230618164207925](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230618164207925.png)

* Join Operation

  * Nested-loop join
    * 两重循环
    * 代价：
      * nr * bs + br   block transfers
      * nr + br  seeks
      * nr是记录数，block中含有多个记录

  * Block nested-loop join
    * ![image-20230618164914151](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230618164914151.png)
    * 代价：
      * Worst case estimate:  br * bs + br  block transfers + 2 * br  seeks
        Each block in the inner relation s is read once for each block in the outer relation
      * Best case: br + bs block transfers + 2 seeks.（内存足够大，每个表只要进入内存一次）
      * 小关系作为外关系更好

    * ![image-20230618165335108](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230618165335108.png)
    * 内存有M块的情况：留1块作为output的缓存，外关系给M-2块，内关系反正每次要seek，只给1块。

  * Indexed nested-loop join
    * ![image-20230618170934436](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230618170934436.png)
    * 多块就是br/(M-2)
    * 外关系小(nr小)的时候选这种方法

  * Merge-join
    * 两个关系已经有序
    * ![image-20230618205150053](C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230618205150053.png)

  * Hash-join
  * <img src="C:\Users\86133\AppData\Roaming\Typora\typora-user-images\image-20230619142752872.png" alt="image-20230619142752872" style="zoom: 67%;" />
