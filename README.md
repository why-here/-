* [网上资源](#%E7%BD%91%E4%B8%8A%E8%B5%84%E6%BA%90)
* [数据库](#%E6%95%B0%E6%8D%AE%E5%BA%93)
  * [事务](#%E4%BA%8B%E5%8A%A1)
  * [ACID](#acid)
  * [范式与异常](#%E8%8C%83%E5%BC%8F%E4%B8%8E%E5%BC%82%E5%B8%B8)
  * [模式](#%E6%A8%A1%E5%BC%8F)
  * [并发事务隔离/一致性问题](#%E5%B9%B6%E5%8F%91%E4%BA%8B%E5%8A%A1%E9%9A%94%E7%A6%BB%E4%B8%80%E8%87%B4%E6%80%A7%E9%97%AE%E9%A2%98)
  * [数据库并发事务的隔离功能](#%E6%95%B0%E6%8D%AE%E5%BA%93%E5%B9%B6%E5%8F%91%E4%BA%8B%E5%8A%A1%E7%9A%84%E9%9A%94%E7%A6%BB%E5%8A%9F%E8%83%BD)
  * [基本锁功能](#%E5%9F%BA%E6%9C%AC%E9%94%81%E5%8A%9F%E8%83%BD)
  * [MVCC（Multi\-Version Concurrency Control，多版本并发控制）](#mvccmulti-version-concurrency-control%E5%A4%9A%E7%89%88%E6%9C%AC%E5%B9%B6%E5%8F%91%E6%8E%A7%E5%88%B6)
  * [MySQL 日志](#mysql-%E6%97%A5%E5%BF%97)
  * [MySQL 索引](#mysql-%E7%B4%A2%E5%BC%95)
  * [SQL](#sql)
  * [NoSQL一览 <a href="https://www\.cnblogs\.com/vajoy/p/5471308\.html" rel="nofollow">Link</a>](#nosql%E4%B8%80%E8%A7%88-link)
* [分布式系统](#%E5%88%86%E5%B8%83%E5%BC%8F%E7%B3%BB%E7%BB%9F)
  * [一致性](#%E4%B8%80%E8%87%B4%E6%80%A7)
  * [分布式一致性协议/算法](#%E5%88%86%E5%B8%83%E5%BC%8F%E4%B8%80%E8%87%B4%E6%80%A7%E5%8D%8F%E8%AE%AE%E7%AE%97%E6%B3%95)
  * [可用性](#%E5%8F%AF%E7%94%A8%E6%80%A7)
  * [分区容错性](#%E5%88%86%E5%8C%BA%E5%AE%B9%E9%94%99%E6%80%A7)
* [操作系统](#%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F)
  * [同步与异步](#%E5%90%8C%E6%AD%A5%E4%B8%8E%E5%BC%82%E6%AD%A5)
  * [阻塞与非阻塞](#%E9%98%BB%E5%A1%9E%E4%B8%8E%E9%9D%9E%E9%98%BB%E5%A1%9E)
  * [buffer 与 cache 的区别](#buffer-%E4%B8%8E-cache-%E7%9A%84%E5%8C%BA%E5%88%AB)
  * [进程间通信](#%E8%BF%9B%E7%A8%8B%E9%97%B4%E9%80%9A%E4%BF%A1)
  * [信号量与互斥量的区别](#%E4%BF%A1%E5%8F%B7%E9%87%8F%E4%B8%8E%E4%BA%92%E6%96%A5%E9%87%8F%E7%9A%84%E5%8C%BA%E5%88%AB)
  * [进程与线程的区别](#%E8%BF%9B%E7%A8%8B%E4%B8%8E%E7%BA%BF%E7%A8%8B%E7%9A%84%E5%8C%BA%E5%88%AB)
  * [fork](#fork)
  * [线程池的实现](#%E7%BA%BF%E7%A8%8B%E6%B1%A0%E7%9A%84%E5%AE%9E%E7%8E%B0)
  * [线程间通信与同步](#%E7%BA%BF%E7%A8%8B%E9%97%B4%E9%80%9A%E4%BF%A1%E4%B8%8E%E5%90%8C%E6%AD%A5)
  * [多线程实践](#%E5%A4%9A%E7%BA%BF%E7%A8%8B%E5%AE%9E%E8%B7%B5)
* [Linux](#linux)
  * [linux 下查找哪个文件占用空间最大的方法](#linux-%E4%B8%8B%E6%9F%A5%E6%89%BE%E5%93%AA%E4%B8%AA%E6%96%87%E4%BB%B6%E5%8D%A0%E7%94%A8%E7%A9%BA%E9%97%B4%E6%9C%80%E5%A4%A7%E7%9A%84%E6%96%B9%E6%B3%95)
  * [shell 统计文件中单词出现的次数](#shell-%E7%BB%9F%E8%AE%A1%E6%96%87%E4%BB%B6%E4%B8%AD%E5%8D%95%E8%AF%8D%E5%87%BA%E7%8E%B0%E7%9A%84%E6%AC%A1%E6%95%B0)
* [网络编程](#%E7%BD%91%E7%BB%9C%E7%BC%96%E7%A8%8B)
  * [TCP 三次握手四次挥手](#tcp-%E4%B8%89%E6%AC%A1%E6%8F%A1%E6%89%8B%E5%9B%9B%E6%AC%A1%E6%8C%A5%E6%89%8B)
  * [HTTP 连接](#http-%E8%BF%9E%E6%8E%A5)
  * [Socket](#socket)
  * [七/五层模型](#%E4%B8%83%E4%BA%94%E5%B1%82%E6%A8%A1%E5%9E%8B)
* [算法](#%E7%AE%97%E6%B3%95)
  * [求 1\+2\+3\+ \.\.\. \+n，不能使用循环和条件判断。](#%E6%B1%82-123--n%E4%B8%8D%E8%83%BD%E4%BD%BF%E7%94%A8%E5%BE%AA%E7%8E%AF%E5%92%8C%E6%9D%A1%E4%BB%B6%E5%88%A4%E6%96%AD)
  * [<a href="http://blog\.csdn\.net/wenqiang1208/article/details/64152061" rel="nofollow">求二叉树中两个节点的最低公共祖先节点</a>](#%E6%B1%82%E4%BA%8C%E5%8F%89%E6%A0%91%E4%B8%AD%E4%B8%A4%E4%B8%AA%E8%8A%82%E7%82%B9%E7%9A%84%E6%9C%80%E4%BD%8E%E5%85%AC%E5%85%B1%E7%A5%96%E5%85%88%E8%8A%82%E7%82%B9)
  * [两个栈实现队列\+两个队列实现栈](#%E4%B8%A4%E4%B8%AA%E6%A0%88%E5%AE%9E%E7%8E%B0%E9%98%9F%E5%88%97%E4%B8%A4%E4%B8%AA%E9%98%9F%E5%88%97%E5%AE%9E%E7%8E%B0%E6%A0%88)
  * [海量数据处理](#%E6%B5%B7%E9%87%8F%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86)
  * [两个有序数组的中位数](#%E4%B8%A4%E4%B8%AA%E6%9C%89%E5%BA%8F%E6%95%B0%E7%BB%84%E7%9A%84%E4%B8%AD%E4%BD%8D%E6%95%B0)
  * [二叉树基础](#%E4%BA%8C%E5%8F%89%E6%A0%91%E5%9F%BA%E7%A1%80)
  * [排序算法](#%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95)
* [C\+\+ 特性](#c-%E7%89%B9%E6%80%A7)
  * [面向对象的了解](#%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E7%9A%84%E4%BA%86%E8%A7%A3)
  * [多态实现原理](#%E5%A4%9A%E6%80%81%E5%AE%9E%E7%8E%B0%E5%8E%9F%E7%90%86)
  * [C 语言实现多态](#c-%E8%AF%AD%E8%A8%80%E5%AE%9E%E7%8E%B0%E5%A4%9A%E6%80%81)
  * [多态](#%E5%A4%9A%E6%80%81)
  * [右值引用与转移语义](#%E5%8F%B3%E5%80%BC%E5%BC%95%E7%94%A8%E4%B8%8E%E8%BD%AC%E7%A7%BB%E8%AF%AD%E4%B9%89)
  * [std::vector 的容量增长](#stdvector-%E7%9A%84%E5%AE%B9%E9%87%8F%E5%A2%9E%E9%95%BF)
  * [只知道数组名，求数组长度](#%E5%8F%AA%E7%9F%A5%E9%81%93%E6%95%B0%E7%BB%84%E5%90%8D%E6%B1%82%E6%95%B0%E7%BB%84%E9%95%BF%E5%BA%A6)
  * [结构体的位置偏移](#%E7%BB%93%E6%9E%84%E4%BD%93%E7%9A%84%E4%BD%8D%E7%BD%AE%E5%81%8F%E7%A7%BB)
  * [inline 函数](#inline-%E5%87%BD%E6%95%B0)
  * [内存拷贝](#%E5%86%85%E5%AD%98%E6%8B%B7%E8%B4%9D)
  * [静态函数/变量](#%E9%9D%99%E6%80%81%E5%87%BD%E6%95%B0%E5%8F%98%E9%87%8F)
  * [C 可变参数](#c-%E5%8F%AF%E5%8F%98%E5%8F%82%E6%95%B0)
* [Python 特性](#python-%E7%89%B9%E6%80%A7)
* [Git](#git)
  * [分区](#%E5%88%86%E5%8C%BA)



#### 网上资源

- [笔试面试知识整理](https://hit-alibaba.github.io/interview/basic/network/HTTP.html)
- [Interview-Notebook](https://github.com/CyC2018/Interview-Notebook)
- [Python 面试](https://github.com/taizilongxu/interview_python)
- [Linux 工具](http://linuxtools-rst.readthedocs.io/zh_CN/latest/index.html)

#### 数据库

##### 事务

  >  事务指的是满足 ACID 特性的一系列操作，这些操作要么都执行，要么都不执行。可以通过 Commit 提交一个事务，也可以使用 Rollback 进行回滚。MySQL 默认采用自动提交模式。也就是说，如果不显示使用`START TRANSACTION`语句来开始一个事务，那么每个查询都会被当做一个事务自动提交。

##### ACID

  >  ACID 是 Atomic（原子性）、Consistency（一致性）、Isolation（隔离性）和 Durability（持久性）。
  >
  >  原子性：SQL 都成功或都撤销
  >
  >  一致性：不能破坏数据的完整和逻辑。
  >
  >  隔离性：事务查看数据更新时，数据所处的状态要么是另一事务修改它之前的状态，要么是另一事务修改它之后的状态，**事务不会查看到中间状态的数据**。
  >
  >  持久性：事务成功，更新必须永久保存。
  >
  >  数据库管理系统采**用日志来保证事务的原子性、一致性和持久性**。数据库管理系统**采用锁机制来实现事务的隔离性**。
  >
  >  [Link](http://www.cnblogs.com/younes/archive/2010/09/09/1822436.html)

##### 范式与异常

  > 函数依赖：
  >
  > - 记 A->B 表示 A 函数决定 B，也可以说 B 函数依赖于 A。
  > - 如果 {A1，A2，... ，An} 是关系的一个或多个属性的集合，该集合函数决定了关系的其它所有属性并且是最小的，那么该集合就称为键码。
  > - 对于 W->A，如果能找到 W 的真子集 W'，使得 W'-> A，那么 W->A 就是部分函数依赖，否则就是完全函数依赖；
  >
  > 范式：
  >
  > - 第一范式（1NF）：属性不可分；会存在四个异常
  > - 第二范式（2NF）：每个非主属性完全函数依赖于键码。部分依赖于键码会造成大量冗余数据；
  > - 第三范式（3NF）：非主属性不传递依赖于键码。消除大部分删除异常和插入异常
  > - BC 范式（BCNF）：所有属性不传递依赖于键码。
  >
  > 包含在任何一个键码（可以是多个键码，不一定是主键）中的属性称为主属性。[Link](https://www.zhihu.com/question/24696366/answer/29189700)
  >
  > 异常：
  >
  > - 冗余数据
  > - 修改异常：只修改了部分数据
  > - 删除异常：删除一个信息，那么也会丢失其他信息
  > - 插入异常：想插入一个部分信息无法确定的数据，无法插入
  >
  > [Link](https://github.com/CyC2018/Interview-Notebook/blob/master/notes/%E6%95%B0%E6%8D%AE%E5%BA%93%E7%B3%BB%E7%BB%9F%E5%8E%9F%E7%90%86.md#%E4%B8%83%E5%85%B3%E7%B3%BB%E6%95%B0%E6%8D%AE%E5%BA%93%E8%AE%BE%E8%AE%A1%E7%90%86%E8%AE%BA)

##### 模式

  > **数据模型**：由数据结构、数据操作和完整性三个要素组成。
  >
  > **数据库系统**包含所有与数据库相关的内容，包括数据库、数据库管理系统、应用程序以及数据库管理员和用户，还包括相关的硬件和软件。
  >
  > **三层模式**：外模式（又称用户模式，是用户和数据库系统的接口），模式（使用特定的数据模式（比如关系模型）来描述数据的逻辑结构，这种逻辑结构包括数据的组成、数据项的名称、类型、取值范围），内模式（又称为存储模式，描述记录的存储方式）
  >
  > **两层映像**：外模式/模式映像（把外模式的局部逻辑结构和模式的全局逻辑结构联系起来。该映像可以保证数据和应用程序的逻辑独立性），模式/内模式映像（把模式的全局逻辑结构和内模式的物理结构联系起来，该映像可以保证数据和应用程序的物理独立性）。

##### 并发事务隔离/一致性问题

  > 在并发环境下，一个事务如果受到另一个事务的影响（破坏了事务的隔离性），那么事务操作就无法满足一致性条件。可能出现以下问题（T1，T2 表示两个事务）：
  >
  > - 丢失修改：T1 和 T2 两个事务都对一个数据进行修改，T1 先修改，T2 随后修改，T2 的修改覆盖了 T1 的修改。
  > - 读脏数据：T1 修改一个数据，T2 随后读取这个数据。如果 T1 撤销了这次修改，那么 T2 读取的数据是脏数据。
  > - 不可重复读：T2 读取一个数据，T1 对该数据做了修改（Update 和 Delete）。如果 T2 再次读取这个数据，此时读取的结果和第一次读取的结果不同。
  > - 幻影读：T1 读取某个范围的数据，T2 在这个范围内插入（Insert）新的数据，T1 再次读取这个范围的数据，此时读取的结果可能和第一次读取的结果不同。
  >
  > [Link](https://github.com/CyC2018/Interview-Notebook/blob/master/notes/%E6%95%B0%E6%8D%AE%E5%BA%93%E7%B3%BB%E7%BB%9F%E5%8E%9F%E7%90%86.md#%E9%97%AE%E9%A2%98)
  >
  > 不可重复读和幻影读的区别：区别在于如何通过锁机制来解决他们产生的问题。通过锁机制克服不可重复读问题，实现可重复读的隔离级别（sql 第一次读取到数据后，就将这些数据加锁，其它事务无法修改这些数据）。但**这种方法却无法锁住 insert 的数据**，所以当事务A先前读取了数据，或者修改了全部数据，事务 B 还是可以 insert 数据提交，这时事务A就会 发现莫名其妙多了一条之前没有的数据，这就是幻读，不能通过行锁来避免。需要 Serializable 隔离级别 ，读用读锁，写用写锁，**读锁和写锁互斥**，这么做可以有效的避免幻读、不可重复读、脏读等问题，但会极大的降低数据库的并发能力。上文说的，是使用悲观锁机制来处理这两种问题，但是MySQL、ORACLE、PostgreSQL等成熟的数据库，出于性能考虑，都是使用了以乐观锁为理论基础的MVCC（多版本并发控制）来避免这两种问题。[Link](https://www.cnblogs.com/itcomputer/articles/5133254.html)

##### 数据库并发事务的隔离功能

  > 并发控制可以通过封锁来实现，但是封锁操作需要用户自己控制，相当复杂。数据库管理系统提供了事务的隔离级别，让用户以一种更轻松的方式处理并发一致性问题。
  >
  > SQL 标准描述了四个事务隔离级别（MySQL/InnoDB都提供）
  >
  > - **未提交读（READ UNCOMMITTED）**：事务中的修改，即使没有提交，对其它事务也是可见的；
  > - **提交读（READ COMMITTED）** ：一个事务只能读取已经提交的事务所做的修改。换句话说，一个事务所做的修改在提交之前对其它事务是不可见的。
  > - **可重复读（REPEATABLE READ）** ：保证在同一个事务中多次读取同样数据的结果是一样的。
  > - **可串行化（SERIALIXABLE）** ：强制事务串行执行。
  >
  > **四个隔离级别的对比** 
  >
  >| 隔离级别 |  脏读  | 不可重复读 | 幻影读  |
  >| :--: | :--: | :---: | :--: |
  >| 未提交读 | YES  |  YES  | YES  |
  >| 提交读  |  NO  |  YES  | YES  |
  >| 可重复读 |  NO  |  NO   | YES  |
  >| 可串行化 |  NO  |  NO   |  NO  |
  >
  > [Link](https://github.com/CyC2018/Interview-Notebook/blob/master/notes/%E6%95%B0%E6%8D%AE%E5%BA%93%E7%B3%BB%E7%BB%9F%E5%8E%9F%E7%90%86.md#%E5%9B%9B%E9%9A%94%E7%A6%BB%E7%BA%A7%E5%88%AB)

##### 基本锁功能

  > - 粒度：MySQL 中提供了两种封锁粒度：行级锁以及表级锁。锁定的数据量越少，发生锁争用的可能就越小，系统的并发程度就越高。因此封锁粒度越小，系统开销就越大。
  >
  > - 锁类型：
  >
  >   - 读写锁：排它锁（Exclusive），简写为 X 锁，又称**写锁**。共享锁（Shared），简写为 S 锁，又称**读锁**。
  >   - 意向锁：意向锁在原来的 X/S 锁之上引入了 IX/IS，IX/IS 都是表锁，用来表示一个事务想要在表中的某个数据行上加 X 锁或 S 锁。任意 IS/IX 锁之间都是兼容的，因为它们只是表示想要对表加锁，而不是真正加锁。
  >
  >   |  -   |  X   |  IX  |  S   |  IS  |
  >   | :--: | :--: | :--: | :--: | :--: |
  >   |  X   |  NO  |  NO  |  NO  |  NO  |
  >   |  IX  |  NO  | YES  |  NO  | YES  |
  >   |  S   |  NO  |  NO  | YES  | YES  |
  >   |  IS  |  NO  |  NO  | YES  | YES  |
  >
  > - 封锁协议
  >
  >   - **一级封锁协议**：解决丢失修改问题，事务 T 要修改数据 A 时必须加 X 锁，直到 T 结束才释放锁。
  >   - **二级封锁协议**：解决读脏数据问题，在一级的基础上，要求读取数据 A 时必须加 S 锁，读取完马上释放 S 锁。
  >   - **三级封锁协议**：解决不可重复读问题，在二级的基础上，要求读取数据 A 时必须加 S 锁，直到事务结束了才能释放 S 锁。
  >
  >
  > - 解锁协议
  >   - 一次加锁：为了预防死锁，一般应用中推荐使用一次封锁法，就是在方法的开始阶段，已经预先知道会用到哪些数据，然后全部锁住，在方法运行之后，再全部解锁。但在数据库中却不适用，因为在事务开始阶段，数据库并不知道会用到哪些数据。
  >   - 两段锁协议：加锁和解锁分为两个阶段进行。事务 T 对数据 A 进行读或者写操作之前，必须先获得对 A 的封锁，并且在释放一个封锁之后，T 不能再获得任何的其它锁。这种方式虽然无法避免死锁，但是两段锁协议可以保证事务的**并发调度是串行化**（各个事务的操作没有交叉，也就没有相互干扰，当然也不会产生并发所引起的。）[Link](https://tech.meituan.com/innodb-lock.html)
  >
  > [Link](https://github.com/CyC2018/Interview-Notebook/blob/master/notes/%E6%95%B0%E6%8D%AE%E5%BA%93%E7%B3%BB%E7%BB%9F%E5%8E%9F%E7%90%86.md#%E4%B8%89%E5%B0%81%E9%94%81)

##### MVCC（Multi-Version Concurrency Control，多版本并发控制）

  > MVCC的实现没有固定的规范，每个数据库都会有不同的实现方式，这里讨论的是InnoDB的MVCC。
  >
  > 在InnoDB中，会在每行数据后添加两个额外的隐藏的值来实现MVCC，这两个值一个记录这行数据何时被创建，另外一个记录这行数据何时过期（或者被删除）。 在实际操作中，存储的并不是时间，而是事务的版本号，每开启一个新事务，事务的版本号就会递增。 在可重读Repeatable reads事务隔离级别下：
  >
  > - SELECT时，读取创建版本号<=当前事务版本号，删除版本号为空或>当前事务版本号。
  > - INSERT时，保存当前事务版本号为行的创建版本号
  > - DELETE时，保存当前事务版本号为行的删除版本号
  > - UPDATE时，插入一条新纪录，保存当前事务版本号为行创建版本号，同时保存当前事务版本号到原来删除的行
  >
  > 通过MVCC，虽然每行记录都需要额外的存储空间，更多的行检查工作以及一些额外的维护工作，但可以减少锁的使用，大多数读操作都不用加锁，读数据操作很简单，性能很好，并且也能保证只会读取到符合标准的行，也只锁住必要行。在MySQL的RR（可重复读）级别中，是解决了幻读的读问题的。
  >
  > 在RR级别中，通过MVCC机制，虽然让数据变得可重复读，但我们读到的数据可能是历史数据，是不及时的数据，不是数据库当前的数据！对于这种读取历史数据的方式，我们叫它快照读 (snapshot read)，而读取数据库当前版本数据的方式，叫当前读 (current read)。很显然，在MVCC中：
  >
  > - 快照读：就是select
  >   - select * from table ....;
  > - 当前读：特殊的读操作，插入/更新/删除操作，属于当前读，处理的都是当前的数据，需要加锁。
  >   - select * from table where ? lock in share mode;
  >   - select * from table where ? for update;
  >   - insert;
  >   - update ;
  >   - delete;
  >
  > 事务的隔离级别中虽然只定义了读数据的要求，实际上这也可以说是写数据的要求。为了解决当前读中的幻读问题，MySQL事务使用了Next-Key锁。Next-Key锁是行锁和GAP（间隙锁）的合并。行锁防止别的事务修改或删除，GAP锁防止别的事务新增（锁定一个范围内的索引），行锁和GAP锁结合形成的的Next-Key锁共同解决了RR级别在写数据时的幻读问题。[Link](https://tech.meituan.com/innodb-lock.html)

##### MySQL 日志

  > 主要包含：错误日志、查询日志、慢查询日志、事务日志、二进制日志；
  >
  > - 在mysql数据库中，错误日志功能是默认开启的。
  > - 默认情况下查询日志是关闭的。由于查询日志会记录用户的所有操作，其中还包含增删查改等信息。
  > - 慢查询日志是用来记录执行时间超过指定时间的查询语句。
  > - 事务日志（InnoDB特有的日志）可以帮助提高事务的效率。使用事务日志，存储引擎在修改表的数据时只需要修改其内存拷贝，再把改修改行为记录到持久在硬盘上的事务日志中，而不用每次都将修改的数据本身持久到磁盘。
  > - 二进制日志也叫作变更日志，主要用于记录修改数据或有可能引起数据改变的mysql语句，并且记录了语句发生时间、执行时长、操作的数据等等。所以说通过二进制日志可以查询mysql数据库中进行了哪些变化。
  >
  > [Link](http://blog.51cto.com/pangge/1319304)
  >
  > Undo日志记录某数据被修改前的值，可以用来在事务失败时进行rollback；Redo日志记录某数据块被修改后的值，可以用来恢复未写入data file的已成功事务更新的数据。
  >
  > [Link](http://www.letiantian.me/2014-06-18-db-undo-redo-checkpoint/)

##### MySQL 索引

  > 索引是在存储引擎层实现的，而不是在服务器层实现的，所以不同存储引擎具有不同的索引类型和实现。
  >
  > 分类：
  >
  > - B+ Tree 索引
  >   - MyISAM 实现：使用B+Tree作为索引结构，叶节点的data域存放的是数据记录的地址。
  >   - InnoDB 实现：InnoDB的数据文件本身就是索引文件，所以InnoDB要求表必须有主键；InnoDB的辅助索引data域存储相应记录主键的值而不是地址。
  >
  > [Link](http://blog.codinglabs.org/articles/theory-of-mysql-index.html)
  >
  > - 哈希索引： Hash 索引结构的特殊性，其检索效率非常高，索引的检索可以一次定位。
  >
  >   - 由于 Hash 索引比较的是进行 Hash 运算之后的 Hash 值，所以它只能用于等值的过滤，不能用于基于范围的过滤
  >   - Hash 索引无法被用来避免数据的排序操作。
  >   - Hash 索引不能利用部分索引键查询。
  >
  >   [Link](https://blog.csdn.net/oChangWen/article/details/54024063)
  >
  > - 全文索引：有时候有人叫倒排文档技术。先定义一个词库，然后在文章中查找每个词条(term)出现的频率和位置。这样就相当于对文件建立了一个以词库为目录的索引，这样查找某个词的时候就能很快的定位到该词出现的位置。
  >
  > **查询性能优化**：
  >
  > Explain
  >
  > 用来分析 SQL 语句，分析结果中比较重要的字段有：
  >
  > - select_type : 查询类型，有简单查询、联合查询和子查询
  > - key : 使用的索引
  > - rows : 扫描的行数

##### SQL

  >[Link](https://github.com/CyC2018/Interview-Notebook/blob/master/notes/SQL.md)
  >
  > **过滤**
  >
  > 下表显示了 WHERE 子句可用的操作符
  >
  >|     操作符     |    说明    |
  >| :---------: | :------: |
  >| `=` `<` `>` | 等于 小于 大于 |
  >|  `<>` `!=`  |   不等于    |
  >|  `<=` `!>`  |   小于等于   |
  >|  `>=` `!<`  |   大于等于   |
  >|  `BETWEEN`  |  在两个值之间  |
  >|  `IS NULL`  | 为 NULL 值 |
  >
  > 应该注意到，NULL 与 0、空字符串都不同。
  >
  > **AND 和 OR** 用于连接多个过滤条件。优先处理 AND，当一个过滤表达式涉及到多个 AND 和 OR 时，可以使用 () 来决定优先级，使得优先级关系更清晰。
  >
  > **IN** 操作符用于匹配一组值，其后也可以接一个 SELECT 子句，从而匹配子查询得到的一组值。
  >
  > **NOT** 操作符用于否定一个条件。
  >
  > **通配符**
  >
  > 通配符也是用在过滤语句中，但它只能用于文本字段。
  >
  >- **%** 匹配 >=0 个任意字符；
  >- **_** 匹配 ==1 个任意字符；
  >- **[ ]** 可以匹配集合内的字符，例如 [ab] 将匹配字符 a 或者 b。用脱字符 ^ 可以对其进行否定，也就是不匹配集合内的字符。
  >
  > 使用 Like 来进行通配符匹配。不要滥用通配符，通配符位于开头处匹配会非常慢。
  >
  > 

##### NoSQL一览 [Link](https://www.cnblogs.com/vajoy/p/5471308.html)

#### 分布式系统

> 分布式领域[CAP理论](http://www.hollischuang.com/archives/666)告诉我们，任何一个分布式系统都无法同时满足Consistency(一致性),Availability(可用性), Partition tolerance(分区容错性) 这三个基本需求。最多只能满足其中两项。

##### 一致性

  > 我们所说的分布式一致性问题通常指的是**数据一致性**问题。在分布式系统中，数据一致性往往指的是由于**数据的复制**，**不同数据节点**中的数据内容是否**完整并且相同**。一个系统如果想保证数据一致性很有**可能影响其性能**。因为并发的写请求需要在前一个写请求结束之后才能进行 **(排队)** 。
  >
  > 一致性模型：
  >
  > - 强一致性：当更新操作完成之后，任何多个后续进程或者线程的访问都会返回最新的更新过的值。
  > - 弱一致性：系统并不保证后续进程或者线程的访问都会返回最新的更新过的值。
  > - 最终一致性：弱一致性的特定形式。系统保证在没有后续更新的前提下，系统最终返回上一次更新操作的值。
  >
  > [Link](http://www.hollischuang.com/archives/663)

##### 分布式一致性协议/算法

  > **分布式事务**是指会涉及到操作多个数据库的事务。分布式事务处理的关键是必须有一种方法可以知道事务在任何地方所做的所有动作，提交或回滚事务的决定必须产生统一的结果（全部提交或全部回滚）。
  >
  > - **二阶段提交（2PC）**：参与者将操作成败通知协调者，再由协调者根据所有参与者的反馈情报决定各参与者是否要提交操作还是中止操作。所谓的两个阶段是指：第一阶段：**准备阶段(投票阶段)**和第二阶段：**提交阶段（执行阶段）**。
  >
  >   缺点：1、**同步阻塞问题**；2、**单点故障导致阻塞**。由于协调者的重要性，一旦协调者发生故障。参与者会一直阻塞下去；3、**数据不一致**。协调者故障，只向部分节点发送 commit 命令；
  >
  > - **三阶段提交（3PC）**：引入超时机制之外，3PC 把 2PC 的准备阶段再次一分为二，这样三阶段提交就有 CanCommit、PreCommit、DoCommit 三个阶段。
  >
  >   ```
  >   在doCommit阶段，如果参与者无法及时接收到来自协调者的doCommit或者rebort请求时，会在等待超时之后，会继续进行事务的提交。
  >   ```
  >   相对于2PC，3PC主要解决的单点故障问题，并减少阻塞。但是这种机制也会导致数据一致性问题。
  >
  > [Link](http://www.hollischuang.com/archives/681)
  >
  > - **Paxos 算法**：主要解决的问题就是如何保证分布式系统中各个节点都能执行一个相同的操作序列。
  >
  >   1、在整个提议和投票过程中，主要的角色就是“提议者”（向“接受者”提出提议）和“接受者”（收到“提议者”的提议后，向“提议者”表达自己的意见）。
  >
  >   2、整个算法的大致过程为：
  >   第一阶段：明确哪个“提议者”是意见领袖有权提出提议，未来，“接受者”们就主要处理这个“提议者”的提议了**（这样，也可以在提出提议时就尽量让意见统一，谋求尽早形成多数派）。**
  >   第二阶段：由上阶段选出的意见领袖提出提议，“接受者”反馈意见。如果多数“接受者”接受了一个提议，那么提议就通过了。（“提议者”在贿选的时候，发现“接受者”已经接受过前面意见领袖的提议了，即便“提议者”贿选成功，也会默默的把自己的提议改为前面意见领袖的提议。）
  >
  >   [Link1](https://www.zhihu.com/question/19787937/answer/107750652) [Link2](http://www.hollischuang.com/archives/693) [Link3](https://zh.wikipedia.org/wiki/Paxos%E7%AE%97%E6%B3%95) [Link4](https://coolshell.cn/articles/10910.html)

##### 可用性

  > 即服务一直可用，而且是正常响应时间。
  >
  > 好的可用性主要是指系统能够很好的为用户服务，不出现用户操作失败或者访问超时等用户体验不好的情况。

##### 分区容错性

  > 即分布式系统在遇到某节点或网络分区故障的时候，仍然能够对外提供满足一致性和可用性的服务。

  [Link](http://www.hollischuang.com/archives/666)

#### 操作系统

##### 同步与异步

  > 所谓同步，就是在发出一个**调用**时，在没有得到结果之前，该*调用*就不返回。但是一旦调用返回，就得到返回值了。换句话说，就是由*调用者*主动等待这个**调用**的结果。
  >
  > 而异步则是相反，**调用在发出之后**，这个调用就直接返回了，所以没有返回结果。换句话说，当一个异步过程调用发出后，调用者不会立刻得到结果。而是在调用发出后，被调用者通过状态、通知来通知调用者，或通过**回调函数**处理这个调用。
  >
  > [Link](https://www.zhihu.com/question/19732473/answer/20851256)

##### 阻塞与非阻塞

  > 阻塞和非阻塞关注的是**程序在等待调用结果**（消息，返回值）时的状态。
  >
  > 阻塞调用是指调用结果返回之前，当前线程会被挂起。调用线程只有在得到结果之后才会返回。
  > 非阻塞调用指在不能立刻得到结果之前，该调用不会阻塞当前线程（不会被挂起）。
  >
  > [Link](https://www.zhihu.com/question/19732473/answer/20851256)

##### buffer 与 cache 的区别

  > Cache：高速缓存，是位于CPU与主内存间的一种容量较小但速度很高的存储器。
  >
  > Buffer：缓冲区，一个用于存储速度不同步的设备或优先级不同的设备之间传输数据的区域。通过缓冲区，可以使进程之间的相互等待变少，从而使从速度慢的设备读入数据时，速度快的设备的操作进程不发生间断。
  >
  > [Link](http://blog.sina.com.cn/s/blog_93dc666c0101cb35.html)
  >

##### 进程间通信

  > - 管道/匿名管道 (pipe)；命名管道 (FIFO)
  >
  >   半双工，单向，具有亲缘关系，内核缓冲区，无格式字节流，存在于内存中；无需具有亲缘关系，存在于文件系统中，内容存放在内存中。
  >
  > - 信号 (Signal)
  >
  >   信号是软件层次上对中断机制的一种模拟，是一种异步通信方式。
  >
  >   - 硬件来源：用户按键输入`Ctrl+C`退出、硬件异常如无效的存储访问等。
  >   - 软件终止：终止进程信号、其他进程调用kill函数、软件异常产生信号。
  >
  > - 消息队列 (Message)
  >
  >   消息队列是消息的链表，具有特定的格式，可随机查询，无需等待写入
  >
  > - 共享内存 (share memory)
  >
  >   使得多个进程可以可以直接读写同一块内存空间，是最快的可用 IPC 形式。需要依靠某种同步机制（如信号量）来达到进程间的同步及互斥。
  >
  > - 信号量 (semaphore)
  >
  >   信号量是一个计数器，用于多进程对共享数据的访问，信号量的意图在于进程间同步。信号量值的测试及减 1 操作应当是原子操作。
  >
  >   互斥量用于线程的互斥，信号量用于线程的同步。
  >
  > - 套接字 (socket)
  >
  >   客户/ 服务器（即要进行通信的进程）系统的开发工作既可以在本地单机上进行，也可以跨网络进行。
  >
  >   套接字是支持 TCP/IP 的网络通信的基本操作单元。
  >
  >   套接字的特性由3个属性确定，它们分别是：域(AF_INET, AF_UNIX) 、端口号、协议类型。
  >
  > [Link](https://www.jianshu.com/p/c1015f5ffa74) [Demo](https://songlee24.github.io/2015/04/21/linux-IPC/)

##### 信号量与互斥量的区别

  > 互斥量用于线程的互斥，信号量用于线程的同步。
  >
  > **互斥：**是指某一资源同时只允许一个访问者对其进行访问，具有唯一性和排它性。但互斥无法限制访问者对资源的访问顺序，即访问是无序的。
  >
  > **同步：**是指在互斥的基础上（大多数情况），通过其它机制实现访问者对资源的有序访问。
  >
  > 信号量可以实现多个同类资源的多线程互斥和同步。互斥量的加锁和解锁必须由同一线程分别对应使用，信号量可以由一个线程释放，另一个线程得到。
  >
  > [Link](https://www.jianshu.com/p/c1015f5ffa74)

##### 进程与线程的区别

  > - 一个程序至少有一个进程,一个进程至少有一个线程；
  > - 进程是系统进行资源分配和调度的一个独立单位，线程是CPU调度和分派的基本单位，它是比进程更小的能独立运行的基本单位。
  > - 进程在执行过程中拥有独立的内存单元，而多个线程共享内存，从而极大地提高了程序的运行效率；
  > - 一个进程崩溃后，在保护模式下不会对其它进程产生影响，一个线程死掉就等于整个进程死掉，所以多进程的程序要比多线程的程序健壮，但在进程切换时，耗费资源较大，效率要差一些。
  >
  > [Link](http://www.cnblogs.com/lmule/archive/2010/08/18/1802774.html)

##### fork

  > 如果进程需要启动另一个程序的可执行文件，它需要先Fork来创建一个自身的副本。然后由该副本即“[子进程](https://zh.wikipedia.org/wiki/%E5%AD%90%E8%BF%9B%E7%A8%8B)”调用[exec](https://zh.wikipedia.org/w/index.php?title=Exec&action=edit&redlink=1)系统调用，用其他程序覆盖自身：停止执行自己之前的程序并执行其他程序。

  - fork 之后，子进程的下一条语句与父进程的下一条语句一样。
  - 通过检查 fork 返回值来判断是子进程还是父进程。
    - 在父进程中，fork返回新创建子进程的进程ID；
    - 在子进程中，fork返回0；
    - 如果出现错误，fork返回一个负值；

##### 线程池的实现

  多线程进程：每个线程执行的都是进程代码的某个片段啊。

  -  当线程池的线程刚创建时，让他们进入阻塞状态：等待某个任务的到来。 如果任务来了，那就好办，唤醒其中一个线程，让它拿到任务去执行即可。
  -  BlockingQueue：一个线程调用它的take()方法取数据时， 如果这个Queue中没有数据，该线程会阻塞；同样，一个线程调用它的put方法放数据时，如果Queue满了， 也会阻塞。

  [Link](https://mp.weixin.qq.com/s/fzIsN8DrLUj0NbcJiD6xSw) [实现](http://www.cppblog.com/Chosen/archive/2013/10/07/203568.html)

##### 线程间通信与同步

  通信方式：

  - 使用全局变量，全局变量最好声明为 volatile。 volatile 指出 i 是随时可能发生变化的，每次使用它的时候必须从 i的地址中读取，而不是使用已经存在寄存器中的值。[Link](https://www.cnblogs.com/yc_sunniwell/archive/2010/07/14/1777432.html)
  - 使用消息实现通信。
  - 使用事件类实现线程间通信。

  同步方式：

  - 条件变量：利用线程间共享的全局变量进行同步的一种机制。条件变量上的基本操作有：触发条件(当条件变为 true 时)；等待条件，挂起线程直到其他线程触发条件。
  - 信号量（semaphore）：如同进程一样，线程也可以通过信号量来实现通信，虽然是轻量级的。
  - 互斥量（mutex）： 通过锁机制实现线程间的同步。同一时刻只允许一个线程执行一个关键部分的代码。

  [Link](https://www.jianshu.com/p/9218692cb209)

##### 多线程实践

  - lambda 表达式启动线程：`thread t([i]{cout << i << endl;});`
  - 重载了 () 运算符的类 

  [Link](https://www.cnblogs.com/wangguchangqing/p/6134635.html)


#### Linux

##### linux 下查找哪个文件占用空间最大的方法

  使用 du 命令 + sort 命令

  `du : 计算出单个文件或者文件夹的磁盘空间占用.`

  `sort : 对文件行或者标准输出行记录排序后输出.`

  `grep: 该命令常用于分析一行的信息，若当中有我们所需要的信息，就将该行显示出来`

  `ps: 用于将某个时间点的进程运行情况选取下来并输出 `

  `kill: 该命令用于向某个工作（%jobnumber）或者是某个PID（数字）传送一个信号 `

  `file: 该命令用于判断接在file命令后的文件的基本数据`

  `cat: 该命令用于查看文本文件的内容，后接要查看的文件名，通常可用管道与more和less一起使用`

  `chmod: 该命令用于改变文件的权限`

  `time:该命令用于测算一个命令（即程序）的执行时间。它的使用非常简单，就像平时输入命令一样，不过在命令的前面加入一个time即可`

  [Link](http://blog.csdn.net/ljianhui/article/details/11100625)

##### shell 统计文件中单词出现的次数

  `wc -c 统计字节数，-l 统计行数，-w 统计字数，-m 统计字符数 `

  `grep cout hello.cpp | wc -l # 统计出现 cout 的行数`

  `grep -o cout hello.cpp | wc -l # 统计出现 cout 的次数`

#### 网络编程

##### TCP 三次握手四次挥手

  > 三次握手：前两次握手为了彼此间能通信，第三次握手防止服务器一直等待。第一次握手重发的请求可能在挥手后被服务器接收，服务器第二次握手后就处于等待状态。
  >
  > 四次挥手：TCP是全双工模式。都需要告诉彼此没有数据发送并且都需要得到回复。四次挥手TIME_WAIT保持2MSL(最大报文段生存时间)原因，主要是防止最后一个ack丢失。
  >
  > [Link](https://github.com/jawil/blog/issues/14)

##### HTTP 连接

  > **HTTP连接最显著的特点是客户端发送的每次请求都需要服务器回送响应，在请求结束后，会主动释放连接。**从建立连接到关闭连接的过程称为“一次连接”。
  > 1）在HTTP 1.0中，客户端的每次请求都要求建立一次单独的连接，在处理完本次请求后，就自动释放连接。
  >
  > 2）在HTTP 1.1中则可以在一次连接中处理多个请求，并且多个请求可以重叠进行，不需要等待一个请求结束后再发送下一个请求。
  >
  > [Link](https://github.com/jawil/blog/issues/14)

##### Socket

  > **应用层可以和传输层通过Socket接口，区分来自不同应用程序进程或网络连接的通信，实现数据传输的并发服务。**
  >
  > 包含进行网络通信必须的五种信息：连接使用的协议，本地主机的IP地址，本地进程的协议端口，远地主机的IP地址，远地进程的协议端口。
  >
  > 套接字之间的连接过程分为三个步骤：服务器监听，客户端请求，连接确认。
  >
  > [Link](https://github.com/jawil/blog/issues/14) [Confuse](https://www.cnblogs.com/kex1n/p/6501977.html)

##### 七/五层模型

  > 七层：物理层，数据链路层，网络层，传输层，会话层，表示层，应用层；
  >
  > 五层：物理层，链路层，网络层，传输层，应用层。


#### 算法

##### 求 1+2+3+ ... +n，不能使用循环和条件判断。
  - 使用递归+短路特点 `ans && (ans += Sum_Solution(n - 1));`
  - 利用构造函数 `A *a = new A[n];` 每次重新计算时，需要重设值。


##### [求二叉树中两个节点的最低公共祖先节点](http://blog.csdn.net/wenqiang1208/article/details/64152061)

  - 找出2个链表的长度，然后让长的先走两个链表的长度差，然后再一起走，直到找到相同的值（因为2个链表用公共的尾部）

##### 两个栈实现队列+两个队列实现栈

  由结构体互导数据，得到头部或尾部的数据。栈实现队列是，入栈在第一个栈操作，出栈在第二个栈操作。

  [Link](http://blog.csdn.net/sheepmu/article/details/38428205)

##### 海量数据处理

  [Link](https://blog.csdn.net/v_JULY_v/article/details/6279498)

  - **海量日志数据，提取出某日访问百度次数最多的那个IP。** 

    **算法思想：分而治之 + Hash**

    1. IP 地址最多有 2^32 = 4G 种取值情况，所以不能完全加载到内存中处理； 
    2. 可以考虑采用“分而治之”的思想，按照 **IP 地址的 Hash( IP ) % 1024 值**，把海量 IP 日志分别存储到 1024 个小文件中。这样，每个小文件最多包含 4 MB 个 IP 地址； 
    3. 对于每一个小文件，可以构建一个 IP 为 key ，出现次数为 value 的 Hash map，同时记录当前出现次数最多的那个 IP 地址；
    4. 可以得到 1024 个小文件中的出现次数最多的 IP ，再依据常规的排序算法得到总体上出现次数最多的 IP ；

  - **搜索引擎会通过日志文件把用户每次检索使用的所有检索串都记录下来，每个查询串的长度为1-255字节。** **请你统计最热门的10个查询串，要求使用的内存不能超过1G。** 

    1. 先对这批海量数据预处理，在O（N）的时间内用Hash表完成**统计** 
    2. 借助堆这个数据结构，找出 Top K，时间复杂度为 N'logK 

  - **有一个1G大小的一个文件，里面每一行是一个词，词的大小不超过16字节，内存限制大小是1M。返回频数最高的100个词。** 

    1. 采用类似第一个例子的方法，找出每个小文件中 TOP 100 的词汇，然后进行归并，丢弃掉TOP 100 之后的词。

  - **有10个文件，每个文件1G，每个文件的每一行存放的都是用户的query，每个文件的query都可能重复。要求你按照query的频度排序。**

    1.  方案 1 ：与上一个例子相似。
    2.  方案 2 ：query 的总量是有限的，直接用 hash_map 进行统计，然后做排序。

  - **给定a、b两个文件，各存放50亿个url，每个url各占64字节，内存限制是4G，让你找出a、b文件共同的url？** 

    1. 将两个文件分别进行 hash，存储到多个小文件中，那么两个文件中相同的 url 将被存入相同编号的小文件中，只要求出小文件中相同的 url 即可。求小文件中相同的 url，可以将一个文件中的 url 存入 hash_set 中，然后遍历另一个文件，查看是否在 hash_set 中。

  - **在2.5亿个整数中找出不重复的整数，注，内存不足以容纳这2.5亿个整数。** 

    1. 方案 1 ：采用 2-Bitmap（每个数分配 2 bit，00 表示不存在，01 表示出现一次，10 表示多次，11 无意义）进行，共需内存 2^32 * 2 bit=1 GB 内存，然后扫描这 2.5 亿个整数。 
    2. 方案 2 ：也可采用与第 1 题类似的方法，进行划分小文件的方法。然后在小文件中找出不重复的整数，并排序。然后再进行归并，注意去除重复的元素。 

  - **腾讯面试题：给40亿个不重复的unsigned int的整数，没排过序的，然后再给一个数，如何快速判断这个数是否在那40亿个数当中？** 

    1. 方案 1 ：申请512M的内存，一个bit位代表一个unsigned int值。读入40亿个数，设置相应的bit位，读入要查询的数，查看相应bit位是否为1，为1表示存在，为0表示不存在。 
    2. 方案 2 ：将 40 亿个数按最高位为 1 或 0 划分的两个文件中，然后更加待查找的数的最高位来判断在哪个文件中，然后判断次高位。。。时间复杂度位 O(logn)。

  - **怎么在海量数据中找出重复次数最多的一个？** 

    1. 先做hash，然后求模映射为小文件，求出每个小文件中重复次数最多的一个，并记录重复次数。然后找出上一步求出的数据中重复次数最多的一个就是所求 

  - **上千万或上亿数据（有重复），统计其中出现次数最多的钱N个数据。** 

    1. 与第二题类似

  - **一个文本文件，大约有一万行，每行一个词，要求统计出其中最频繁出现的前10个词，请给出思想，给出时间复杂度分析。**

    1.  这题是考虑时间效率。用trie树统计每个词出现的次数，时间复杂度是O(n*le)（le表示单词的平准长度）。然后是找出出现最频繁的前10个词，可以用堆来实现，前面的题中已经讲到了，时间复杂度是O(n*lg10)。所以总的时间复杂度，是O(n*le)与O(n*lg10)中较大的哪一个。 

##### 两个有序数组的中位数

  > 回顾下中位数，对于一个有序数组，如果数组长度是奇数，那么中位数就是中间那个值，如果长度是偶数，就是中间两个数的平均数。

  - 解法 1 O(nlogn) ：将两个数组合并成一个，然后排序，最后根据数组长度选择中位数
  - 解法 2 O(n) ：通过归并排序合并数组，然后根据长度选择中位数
  - 解法 3 O(logn) ：转变成一个寻找第 k 小数的问题。通过对k/2位置数值大小的比较，进行二分查找，逐步排除掉肯定是小于第 k 个数的数，最后找到所求的第k小数。每次都有k一半的元素被删除，所以算法复杂度为log*k*，由于求中位数时k为（m+n）/2，所以算法复杂度为log(m+*n*)。

  [Link](https://blog.csdn.net/yutianzuijin/article/details/11499917)

##### 二叉树基础

  > - 二叉树的第 $i$ 层至多拥有 $2^{i-1}$ 个节点数；
  >
  > - 深度为 $k$ 的二叉树至多总共有 $2^{k+1}-1$ 个节点数（定义根节点所在深度 $k_0 = 0$）；
  >
  > - 对任何一棵非空的二叉树 T ，如果其叶片(终端节点)数为 $n_0$，分支度为 2 的节点数为 $n_2$，则 $n_0 = n_2 + 1$。
  >
  > - 完全二叉树：叶节点只能出现在最下层和次下层，并且最下面一层的结点都集中在该层最左边的若干位置的二叉树。
  >   - 具有 n 个节点的完全二叉树的高度为 $l o g _2 n + 1 $；
  >   - $n_0$是度为 0 的结点总数（即叶子结点数），$n_1$是度为 1 的结点总数，$n_2$是度为 2 的结点总数。
  >   - $n = n_0 + n_1 + n_2$ （其中n为完全二叉树的结点总数）
  >   - $n = 1 + n_1 + 2*n_2$  （除根结点外其他结点都有父结点）
  >   - $n = 2*n_0 + n_1 - 1$  （上面两式相减，$n_1$ 等于 1 或 0）
  >   - n 为偶数，则 $n_0 = n/2$，n 为奇数，则 $n_0 = (n+1)/2$ （可根据完全二叉树的结点总数计算出叶子结点数）
  >
  >   [Link](https://baike.baidu.com/item/%E5%AE%8C%E5%85%A8%E4%BA%8C%E5%8F%89%E6%A0%91)
  >
  > - 顺序存储
  >
  >   - 若是满二叉树就能紧凑排列而不浪费空间；
  >   - 如果某个节点的索引为i，（假设根节点的索引为0）则在它左子节点的索引会是 $2 i + 1 $，以及右子节点会是 $2 i + 2 $；而它的父节点（如果有）索引则为 $\left\lfloor {\frac {i-1}{2}}\right\rfloor $。
  >
  > - 链表存储
  >
  >   - 使用链表能避免顺序存储浪费空间的问题；
  >   - 但是，由于缺乏父链的指引，在找回父节点时需要重新扫描树得知父节点的节点地址。
  >
  > - 将n叉树转换为二叉树
  >
  >   - 一般有序树可映射为二叉树，但反之未必成立。二叉树当且仅当根节点没有右子结点时可转换为 n 叉树。
  >   - n 叉树转换为二叉树的方法：二叉树中结点 x 的左子结点为 n 叉树中结点 x 的左子结点；二叉树中结点 x 的右子结点为 n 叉树中结点 x 的第一个右边的同级结点 y 。
  >
  > [Link](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%8F%89%E6%A0%91)
  >
  > - 二叉搜索树（BST）
  >
  >   - 左子树上所有节点的值均小于它的根节点的值；右子树上所有节点的值均大于它的根节点的值；任意节点的左、右子树也分别为二叉查找树；没有键值相等的节点；
  >   - 优势在于查找、插入的时间复杂度较低。为O(log n)；
  >   - 一个无序序列可以通过构造一棵二叉查找树变成一个有序序列，构造树的过程即为对无序序列进行查找的过程；
  >   - 每次插入的新的结点都是二叉查找树上新的叶子结点，在进行插入操作时，不必移动其它结点，只需改动某个结点的指针；
  >   - 搜索、插入、删除的复杂度等于树高，期望 $O ( log ⁡ n ) $，最坏 $O ( n )$（数列有序，树退化成线性表）。
  >   - 若该组数值经是有序的（从小到大），则建造出来的二叉查找树的所有节点，都没有左子树。
  >
  >   [Link](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%85%83%E6%90%9C%E5%B0%8B%E6%A8%B9)
  >
  > - 平衡树
  >
  >   > 平衡指所有叶子的深度趋于平衡；几乎所有平衡树的操作都基于树旋转操作，通过旋转操作可以使得树趋于平衡；
  >
  >   - AVL 树
  >
  >     > 任何节点的两个子树的高度最大差别为1；
  >     >
  >     > 节点的**平衡因子**是它的左子树的高度减去它的右子树的高度；带有平衡因子1、0或 -1的节点被认为是平衡的。带有平衡因子 -2或2的节点被认为是不平衡的，并需要重新平衡这个树。
  >
  >     - 在左左和右右的情况下，只需要进行一次旋转操作；在左右和右左的情况下，需要进行两次旋转操作。
  >     - 删除：从AVL树中删除，可以通过把要删除的节点向下旋转成一个叶子节点，接着直接移除这个叶子节点来完成。
  >
  >     [Link](https://zh.wikipedia.org/wiki/AVL%E6%A0%91)
  >
  >   - 红黑树
  >
  >     > 基于二叉查找树增加了额外要求：1. 节点是红色或黑色。2. 根是黑色。3. 所有叶子都是黑色（叶子是NIL节点）。4. 每个红色节点必须有两个黑色的子节点。（从每个叶子到根的所有路径上不能有两个连续的红色节点。）5. 从任一节点到其每个叶子的所有简单路径都包含相同数目的黑色节点。
  >     >
  >     > 从根到叶子的最长的可能路径不多于最短的可能路径的两倍长。
  >     >
  >     > 任何不平衡都会在三次旋转之内解决。
  >
  >     - 插入：首先以二叉查找树的方法增加节点并标记它为红色。接着通过颜色调换（color flips）和树旋转来调整。
  >     - 删除：
  >
  >     > 红黑树相对于AVL树来说，牺牲了部分平衡性以换取插入/删除操作时少量的旋转操作，整体来说性能要优于AVL树。
  >
  >     [Link](https://zh.wikipedia.org/wiki/%E7%BA%A2%E9%BB%91%E6%A0%91)
  >
  >   - B 树
  >
  >     > B 树，概括来说是一个一般化的二叉查找树，可以拥有多于 2 个子节点。
  >     >
  >     > B 树减少定位记录时所经历的中间过程，从而加快存取速度。B 树这种数据结构可以用来描述外部存储。这种数据结构常被应用在数据库和文件系统的实现上。
  >
  >     > 在 B 树中，内部（非叶子）节点可以拥有可变数量的子节点（数量范围预先定义好）。
  >     >
  >     > 内部节点可能会被合并或者分离。
  >     >
  >     > 子节点数量的上界和下界依特定的实现而设置。
  >     >
  >     > B 树中每一个内部节点会包含一定数量的键值。通常，键值的数量被选定在 d 和 2d 之间。因数2将保证节点可以被拆分或组合。
  >     >
  >     > 一个 B 树通过约束所有叶子节点在相同深度来保持平衡。
  >
  >     > 在存取节点数据所耗时间远超过处理节点数据所耗时间的情况下，B 树在可选的实现中拥有很多优势，因为存取节点的开销被分摊到里层节点的多次操作上。
  >
  >   [Link](https://zh.wikipedia.org/wiki/%E5%B9%B3%E8%A1%A1%E6%A0%91)

##### 排序算法

  > 1. 稳定性：a 与 b 相等，排序之前 a 在 b 之前，排序之后 a 还在 b 之前。好处：使用部分键值作为指标进行排序后，未作为排序指标的键值的顺序仍旧保持有序，比如用 [112 和 121] 的最高位排序，稳定算法的结果为 [112 121]，不稳定算法结果可能为 [121 112]。[Link](http://qr.ae/TUTLVr)
  >
  > 2. 是否基于比较，时间，空间复杂度，最好，最坏情况。
  >
  > 3. 所有基于比较的排序算法时间复杂度至少为 O(nlogn);
  >
  > 4. **冒泡排序**：逐轮比较邻近的值并交换；
  >
  >    - 优化 1 ：若不发生 swap ，表示已正序；
  >    - 优化 2 ：记录最后一次发生交换的位置，其之后的元素已排好序；
  >    - 优化 3 ：进行双向的循环（鸡尾酒排序），正向最大移到末尾，反向最小移到最前。
  >
  > 5. **插入排序**：每次取一个未排序元素，在已排序的数列中找到合适的位置插入（需要移动元素）。
  >
  >    改进：在插入有序的数列中时，使用二分查找，找到要插入的位置。
  >
  > 6. **希尔排序**：基于插入排序的以下两点性质而提出改进方法的
  >
  >    - 插入排序在对几乎已经排好序的数据操作时， 效率高， 即可以达到线性排序的效率
  >    - 但插入排序一般来说是低效的， 因为插入排序每次只能将数据移动一位
  >
  >    步骤：
  >
  >    - 先取一个正整数 d1(d1 < n)，把全部记录分成 d1 个组，所有距离为 d1的倍数的记录看成一组，然后在各组内进行插入排序
  >    - 然后取 d2(d2 < d1)
  >    - 重复上述分组和排序操作；直到取 di = 1(i >= 1) 位置，即所有记录成为一个组，最后对这个组进行插入排序。一般选 d1 约为 n/2，d2 为 d1 /2， d3 为 d2/2 ，…， di = 1。
  >
  >    [Link](http://bubkoo.com/2014/01/15/sort-algorithm/shell-sort/)
  >
  > 7. **快速排序**：
  >
  >    - 步骤 1 ：从数组中随机取一个值作为标兵
  >    - 步骤 2 ：将数组分为左右两个区间，比标兵大在右，比标兵小在左
  >    - 步骤 3 ：重复步骤 1，2
  >
  >    分区办法：把标兵放在末尾（或取末尾为标兵），循环移动（交换）小于等于标兵的元素到数组左半边，最后将标兵重新交换到指定位置。
  >
  >    应用：使用分区来查找数组中第 K 大的元素，或最大/小的 K 个元素。
  >
  > 8. **选择排序**：首先在数组中找到最大的放到末尾，重复此操作。
  >
  > 9. **归并排序**：递归将数组不断划分为大小为1的数组，然后递归将两个已排好序的数组合并成一个数组。可以使用临时数组用于合并，也可以采用类似插入排序的方法进行合并（将其中一个子数组中的元素依次插入到另一个数组当中）。[Link](http://bubkoo.com/2014/01/15/sort-algorithm/merge-sort/)
  >
  >    归并排序除了可以对数组进行排序，还可以高效的求出数组小和（即单调和）以及数组中的逆序对，详见这篇[博文](http://www.jianshu.com/p/3ab5033074f1)。
  >
  > 10. **堆排序**：将数组看成一颗完全二叉树，递归构造最大堆（堆根节点最大）或最小堆（根节点最小），将剩余的堆继续调整为最大堆。
  >
  > -  操作 1 ：最大堆调整（Max-Heapify）保证下标 i 的结点之后（两层之内）结点都满足最大堆的性质
  > -  操作 2 ：创建最大堆（Build-Max-Heap）将自下而上的调用 Max-Heapify 来改造数组，建立最大堆
  >    - 操作 3 ：堆排序（Heap-Sort）调用Build-Max-Heap将数组改造为最大堆，然后将堆顶和堆底元素交换，之后将底部上升，最后重新调用Max-Heapify 保持最大堆性质。
  >
  >    [Link](http://bubkoo.com/2014/01/14/sort-algorithm/heap-sort/) [Link](https://www.youtube.com/watch?v=MtQL_ll5KhQ)
  >
  > 11. **桶排序**：
  >
  > - 步骤 1 ：假设待排序的一组数统一的分布在一个范围中，并将这一范围划分成几个子范围，也就是桶
  > - 步骤 2 ：将待排序的一组数，分档规入这些子桶，并将桶中的数据进行排序
  >    - 步骤 3 ：将各个桶中的数据有序的合并起来
  >
  > 12. **基数排序**：基数排序法会使用到桶 (Bucket)，顾名思义，通过按照要比较的位（个位、十位、百位…），将要排序的元素分配至 0~9 个桶中，借以达到排序的作用，排序完后用第二位分桶排序，直到遍历所有位。
  >
  > 13. **猴子排序**：是个既不实用又原始的排序算法，其原理等同将一堆卡片抛起，落在桌上后检查卡片是否已整齐排列好，若非就再抛一次。
  >
  > 14. **计数排序**：统计数值出现的次数，然后根据统计结果进行排序。反向填充目标数组，可以确保计数排序的稳定性。
  >
  > - 步骤 1 ：统计数组A中每个值A[i]出现的次数，存入C[A[i]]
  > - 步骤 2 ：从前向后，使数组C中的每个值等于其与前一项相加，这样数组C[A[i]]就变成了代表数组A中小于等于A[i]的元素个数
  >    - 步骤 3 ：反向填充目标数组B：将数组元素A[i]放在数组B的第C[A[i]]个位置（下标为C[A[i]] - 1），每放一个元素就将C[A[i]]递减
  >
  >| 排序方法 |       平均情况        |     最好情况     |       最坏情况        |      辅助空间      | 稳定性  |    备注    |
  >| :--: | :---------------: | :----------: | :---------------: | :------------: | :--: | :------: |
  >| 冒泡排序 |     $O(n^2)$      |    $O(n)$    |     $O(n^2)$      |     $O(1)$     |  稳定  |  n 小时好   |
  >| 选择排序 |     $O(n^2)$      |   $O(n^2)$   |     $O(n^2)$      |     $O(1)$     | 不稳定  |  n 小时好   |
  >| 插入排序 |     $O(n^2)$      |    $O(n)$    |     $O(n^2)$      |     $O(1)$     |  稳定  |   有序的好   |
  >| 希尔排序 | $O(nlogn)到O(n^2)$ | $O(n^{1.3})$ |     $O(n^2)$      |     $O(1)$     | 不稳定  |          |
  >| 堆排序  |    $O(nlogn)$     |  $O(nlogn)$  |    $O(nlogn)$     |     $O(1)$     | 不稳定  |  n 大时好   |
  >| 归并排序 |    $O(nlogn)$     |  $O(nlogn)$  |    $O(nlogn)$     |     $O(n)$     |  稳定  |  n 大时好   |
  >| 快速排序 |    $O(nlogn)$     |  $O(nlogn)$  |     $O(n^2)$      | $O(logn)到O(n)$ | 不稳定  |   n 大时   |
  >| 计数排序 |    $O(n + k)$     |  $O(n + k)$  |    $O(n + k)$     |   $O(n + k)$   |  稳定  | 可与基数排序配合 |
  >| 基数排序 |    $O(n * dn)$    | $O(n * dn)$  |    $O(n * dn)$    |  $O(n * dn)$   |  稳定  |          |
  >| 桶排序  |      $O(n)$       |    $O(n)$    | $O(nlogn)或O(n^2)$ |  $O(n + bn)$   |  稳定  |          |
  >
  > [基于比较](http://www.cnblogs.com/eniac12/p/5329396.html) [不基于比较](http://www.cnblogs.com/eniac12/p/5332117.html)

#### C++ 特性

##### 面向对象的了解

  > 面向对象编程注重的是：**1）数据和其行为的打包封装，2）程序的接口和实现的解耦**。[Link](https://coolshell.cn/articles/8745.html)

  > 面向对象是相对于面向过程而言的。面向过程语言是一种基于**功能分析**的、以**算法**为中心的程序设计方法；而面向对象是一种基于**结构分析**的、以**数据**为中心的程序设计思想。
  >
  > 从面向过程的角度看，类就是一个特殊的数据结构，它就好像是我们C语言中的结构体;从面向对象的角度看，类就是具有相同属性和方法的对象的集合。
  >
  > 面向对象有三大特性：封装、继承、多态。
  >
  > - **封装，**就是指隐藏对象的实现细节，给外界提供公共的方法来访问。
  >
  >
  > - **继承**，子类可以继承父类的公共属性和方法，子类永远没法继承到父类的私有属性和方法。
  > - **多态，**就是同一个实现接口，对不同的实例而执行不同的操作。
  >
  > [Link](https://my.oschina.net/shaw1688/blog/601142)

##### 多态实现原理

  > 在基类的函数前加上virtual关键字，在派生类中重写该函数，运行时将会根据对象的实际类型来调用相应的函数。
  >
  > C++的多态性是通过动态绑定技术来实现的。
  >
  > [Link](http://blog.csdn.net/tujiaw/article/details/6753498)

  > 每一个有虚函数的类（或有虚函数的类的派生类）都有一个虚函数表，该类的任何对象中都放着虚函数表的指针。虚函数表中列出了该类的虚函数地址。
  >
  > 多态的函数调用语句被编译成一系列根据基类指针所指向的（或基类引用所引用的）对象中存放的虚函数表的地址，在虚函数表中查找虚函数地址，并调用虚函数的指令。
  >
  > [Link](https://www.jianshu.com/p/3a404ab34936) [Link](https://blog.csdn.net/lihao21/article/details/50688337)

##### C 语言实现多态

  使用函数指针，以及函数指针的字节对齐实现多态，使得将子类指针赋予父类指针，调用函数时能正常调用。

  [Link](http://www.cnblogs.com/wuyudong/p/achieving-polymorphism-in-c.html)

##### 多态

  > 多态性的表现，这里用c++来简述，其实OOP应该都差不多。
  >
  > c++的多态分为两种：
  >
  > 1.编译时多态：重载，函数名称相同，但参数类型或参数个数不同的一组函数。在编译期就决好的。
  >
  > 2.运行时多态：重写（也称为覆盖override），也称为覆盖，牵扯到虚函数，简单来说就是虚函数（impure virtual）为我们实现一份默认的操作，我们可以使用这个也可以自己重写（覆盖）虚函数。

##### 右值引用与转移语义

  > 右值引用 (Rvalue Referene) 是 C++ 新标准 (C++11, 11 代表 2011 年 ) 中引入的新特性 , 它实现了转移语义 (Move Sementics) 和精确传递 (Perfect Forwarding)。它的主要目的有两个方面：
  >
  > 1. 消除两个对象交互时不必要的对象拷贝，节省运算存储资源，提高效率。
  > 2. 能够更简洁明确地定义泛型函数。
  >
  > 在 C++11 之前，右值是不能被引用的，最大限度就是用常量引用绑定一个右值

  > - 通俗的左值的定义就是非临时对象，右值是指临时的对象，它们只在当前的语句中有效。
  > - 实际上右值是可以被修改的，既然右值可以被修改，那么就可以实现右值引用。
  > - 左值的声明符号为”&”， 为了和左值区分，右值的声明符号为”&&”。

  > 右值引用是用来支持转移语义的。转移语义可以将资源 ( 堆，系统对象等 ) 从一个对象转移到另一个对象，这样能够减少不必要的临时对象的创建、拷贝以及销毁，能够大幅度提高 C++ 应用程序的性能。
  >
  > - 参数（右值）的符号必须是右值引用符号，即“&&”。
  > - 参数（右值）不可以是常量，因为我们需要修改右值。
  > - 参数（右值）的资源链接和标记必须修改。否则，右值的析构函数就会释放资源。转移到新对象的资源也就无效了。

  > 标准库提供了函数 std::move，这个函数以非常简单的方式将左值引用转换为右值引用。
  >
  > `std::move`在提高 swap 函数的的性能上非常有帮助。通过 std::move，一个简单的 swap 函数就避免了 3 次不必要的拷贝操作。

  > 精确传递适用于这样的场景：需要将一组参数原封不动的传递给另一个函数。
  >
  > - 函数 forward_value 为每一个参数必须重载两种类型，T& 和 const T&，否则，下面四种不同类型参数的调用中就不能同时满足
  > - 右值引用，只需要定义一次，接受一个右值引用的参数，就能够将所有的参数类型原封不动的传递给目标函数。

  [Link](https://www.ibm.com/developerworks/cn/aix/library/1307_lisl_c11/index.html)

##### std::vector 的容量增长
  > std::vector在插入新元素时，若遇到已分配容量不足的情况，会自动拓展容量大小，而这个拓展容量的过程为：
  - 开辟另外一块更大的内存空间，该空间大小通常为原空间大小的两倍；
  - 将原内存空间中的数据拷贝到新开辟的内存空间中；
      - 析构原内存空间的数据，释放原内存空间，并调整各种指针指向新内存空间。

  > Windows下的std::vector一般会按原有容量的1.5倍来增长，到了后期内存吃紧的时候或者一次性插入的数据个数多于原有数据的时候会改变策略为增长空间为刚好能容纳原有数据和新增数据。

  > 对于push_*这样的操作，__n为1，一般会小于size()，所以这时候表现出来的就是翻倍增长，假如是一次插入很多个的时候，__n就有可能比size()大了，这时候也打破翻倍增长的规律，改为增长为刚好容纳原有数据和新增数据的容量了。

  [Link](https://lgcagithub.github.io/2016/08/20/cpp-std-vector-grow/)

##### 只知道数组名，求数组长度

  - 在数组的作用域中，使用`sizeof(数组名)/sizeof(数组的一个元素)`
  - `strlen`可以得到字符数组的长度，但遇到`'\0'`就截止，得到结果后应加 1 。
  - 将数组名作为参数传递，将被当作指针类型，因此需要额外的方法来传递长度信息。

  [Link](http://www.cjjjs.com/paper/bcyy/2016317114754540.html)

##### 结构体的位置偏移

  - 结构体中的所有成员其首地址偏移量必须为**其数据类型长度的整数倍**，其中第一个成员的首地址偏移量为0 。例如，若第二个成员类型为 int ，则其首地址偏移量必须为 4 的倍数，否则就要“首部填充”；以此类推。
  - 结构体所占的总字节数即 sizeof() 函数返回的值必须是**最大成员的长度的整数倍**，否则要进行“末尾填充”；
  - 若结构体 A 将结构体 B 作为其成员，则结构体 B 存储的首地址的偏移量必须为 **B 中所含成员数据长度最大值的整数倍**，如若 B 中成员为 int，double，char，则 B 的偏移量要为 8 的整数倍；否则进行“中间填充”。
  - 空类的长度为 1 ;否则 class 和 struct 的数据对齐原则一致。
  - sizeof() 计算时只计算存放在栈中的空间，static 等声明的全局变量存放在静态数据空间，不会计算在内。

  [Link](https://blog.csdn.net/a1154761720/article/details/19816615)

##### inline 函数

  - inline 函数定义和声明通常全部放在头文件中，因为inline函数会在编译阶段被替换为函数代码，不用到 call/return 机制，如果在一个 .c 中定义内联函数，则在其他文件中无法用该函数；
  - 宏在编译前处理（编译预处理阶段），inline 在编译阶段处理；
  - inline 函数和宏的区别在于 inline 函数在替换时会进行类型检查，而且 inline 函数的声明对于编译器而言只是建议性的，编译器会自身优化；
  - 虚函数肯定不会是内联函数，虚函数是在运行时决定调用哪个函数，而内联函数在编译阶段就会被替换为代码块，函数名符号根本就不存在了；
  - 内联函数的主要作用在于节约了资源，消除了一个call/return机制；

  [Link](https://blog.csdn.net/a1154761720/article/details/19816615)

##### 内存拷贝

  void *memcpy(void *dest, const void *src, size_t n);   #include<string.h>

  void *memmove(void *dest, const void *src, size_t n);   #include<string.h>

  - 当源地址位于 dest~dest+n 之内时，直接从头开始复制会更改原数据的部分内容。
  - 当目的地址位于 src~src+n 之内时，直接从头开始复制会覆盖部分原数据，即更改了原数据内容，复制结果也不正确。可以从尾部开始复制，保证复制结果正确，但原数据仍然会被覆盖。
  - memcpy 不考虑内存覆盖，memmove 考虑内存覆盖，会从尾部开始复制。

  [Link](http://jeremybai.github.io/blog/2014/09/05/memcpy)

##### 静态函数/变量

  - 静态成员变量在类中仅仅是声明，没有定义，所以要在类的外面定义，实际上是给静态成员变量分配内存。如果不加定义就会报错，初始化是赋一个初始值，而定义是分配内存。
  - 静态成员函数没有 this 指针，只能访问静态成员（包括静态成员变量和静态成员函数）。
  - 可以使用静态成员变量清楚了解构造与析构函数的调用情况。

  [Link](http://www.runoob.com/cplusplus/cpp-static-members.html)

##### C 可变参数

  函数参数的传递存储在栈中,从右至左压入栈中,压栈过程为递减 

  `int func(int, ... ) {}`

  ```c
  #include <stdarg.h>
  double average(int num,...)
  {
      va_list valist;
      /* 为 num 个参数初始化 valist */
      va_start(valist, num);
      /* 访问所有赋给 valist 的参数 */
      for (i = 0; i < num; i++)
      {
         sum += va_arg(valist, int);
      }
      /* 清理为 valist 保留的内存 */
      va_end(valist);
  }
  ```
  [Link](http://www.runoob.com/cprogramming/c-variable-arguments.html)


#### Python 特性

[Link](https://github.com/taizilongxu/interview_python)

#### Git

##### 分区

  > 分为：工作区，版本库，版本库包含暂存区、分支以及分支指针。
  >
  > 第一步是用`git add`把文件添加进去，实际上就是把文件修改添加到暂存区；
  >
  > 第二步是用`git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支。

