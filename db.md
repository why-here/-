#### 数据库

##### 事务

> 事务指的是满足 ACID 特性的一系列操作，这些操作要么都执行，要么都不执行。可以通过 Commit 提交一个事务，也可以使用 Rollback 进行回滚。MySQL 默认采用自动提交模式。也就是说，如果不显示使用`START TRANSACTION`语句来开始一个事务，那么每个查询都会被当做一个事务自动提交。

##### ACID

> ACID 是 Atomic（原子性）、Consistency（一致性）、Isolation（隔离性）和 Durability（持久性）。
>
> >   原子性：SQL 都成功或都撤销
> >
> >   一致性：不能破坏数据的完整和逻辑。
> >
> >   隔离性：事务查看数据更新时，数据所处的状态要么是另一事务修改它之前的状态，要么是另一事务修改它之后的状态，**事务不会查看到中间状态的数据**。
> >
> >   持久性：事务成功，更新必须永久保存。
> >
> >   数据库管理系统采**用日志来保证事务的原子性、一致性和持久性**。数据库管理系统**采用锁机制来实现事务的隔离性**。
> >
> >   [Link](http://www.cnblogs.com/younes/archive/2010/09/09/1822436.html)

##### 范式与异常

> 函数依赖：
>
> > - 记 A->B 表示 A 函数决定 B，也可以说 B 函数依赖于 A。
> > - 如果 {A1，A2，... ，An} 是关系的一个或多个属性的集合，该集合函数决定了关系的其它所有属性并且是最小的，那么该集合就称为键码。
> > - 对于 W->A，如果能找到 W 的真子集 W'，使得 W'-> A，那么 W->A 就是部分函数依赖，否则就是完全函数依赖；
> >
> >  范式：
> >
> > - 第一范式（1NF）：属性不可分；会存在四个异常
> > - 第二范式（2NF）：每个非主属性完全函数依赖于键码。部分依赖于键码会造成大量冗余数据；
> > - 第三范式（3NF）：非主属性不传递依赖于键码。消除大部分删除异常和插入异常
> > - BC 范式（BCNF）：所有属性不传递依赖于键码。
> >
> >  包含在任何一个键码（可以是多个键码，不一定是主键）中的属性称为主属性。[Link](https://www.zhihu.com/question/24696366/answer/29189700)
> >
> >  异常：
> >
> > - 冗余数据
> > - 修改异常：只修改了部分数据
> > - 删除异常：删除一个信息，那么也会丢失其他信息
> > - 插入异常：想插入一个部分信息无法确定的数据，无法插入
> >
> >  [Link](https://github.com/CyC2018/Interview-Notebook/blob/master/notes/%E6%95%B0%E6%8D%AE%E5%BA%93%E7%B3%BB%E7%BB%9F%E5%8E%9F%E7%90%86.md#%E4%B8%83%E5%85%B3%E7%B3%BB%E6%95%B0%E6%8D%AE%E5%BA%93%E8%AE%BE%E8%AE%A1%E7%90%86%E8%AE%BA)

##### 模式

> **数据模型**：由数据结构、数据操作和完整性三个要素组成。
>
> >  **数据库系统**包含所有与数据库相关的内容，包括数据库、数据库管理系统、应用程序以及数据库管理员和用户，还包括相关的硬件和软件。
> >
> >  **三层模式**：外模式（又称用户模式，是用户和数据库系统的接口），模式（使用特定的数据模式（比如关系模型）来描述数据的逻辑结构，这种逻辑结构包括数据的组成、数据项的名称、类型、取值范围），内模式（又称为存储模式，描述记录的存储方式）
> >
> >  **两层映像**：外模式/模式映像（把外模式的局部逻辑结构和模式的全局逻辑结构联系起来。该映像可以保证数据和应用程序的逻辑独立性），模式/内模式映像（把模式的全局逻辑结构和内模式的物理结构联系起来，该映像可以保证数据和应用程序的物理独立性）。

##### 并发事务隔离/一致性问题

> 在并发环境下，一个事务如果受到另一个事务的影响（破坏了事务的隔离性），那么事务操作就无法满足一致性条件。可能出现以下问题（T1，T2 表示两个事务）：
>
> > - 丢失修改：T1 和 T2 两个事务都对一个数据进行修改，T1 先修改，T2 随后修改，T2 的修改覆盖了 T1 的修改。
> > - 读脏数据：T1 修改一个数据，T2 随后读取这个数据。如果 T1 撤销了这次修改，那么 T2 读取的数据是脏数据。
> > - 不可重复读：T2 读取一个数据，T1 对该数据做了修改（Update 和 Delete）。如果 T2 再次读取这个数据，此时读取的结果和第一次读取的结果不同。
> > - 幻影读：T1 读取某个范围的数据，T2 在这个范围内插入（Insert）新的数据，T1 再次读取这个范围的数据，此时读取的结果可能和第一次读取的结果不同。
> >
> >  [Link](https://github.com/CyC2018/Interview-Notebook/blob/master/notes/%E6%95%B0%E6%8D%AE%E5%BA%93%E7%B3%BB%E7%BB%9F%E5%8E%9F%E7%90%86.md#%E9%97%AE%E9%A2%98)
> >
> >  不可重复读和幻影读的区别：区别在于如何通过锁机制来解决他们产生的问题。通过锁机制克服不可重复读问题，实现可重复读的隔离级别（sql 第一次读取到数据后，就将这些数据加锁，其它事务无法修改这些数据）。但**这种方法却无法锁住 insert 的数据**，所以当事务A先前读取了数据，或者修改了全部数据，事务 B 还是可以 insert 数据提交，这时事务A就会 发现莫名其妙多了一条之前没有的数据，这就是幻读，不能通过行锁来避免。需要 Serializable 隔离级别 ，读用读锁，写用写锁，**读锁和写锁互斥**，这么做可以有效的避免幻读、不可重复读、脏读等问题，但会极大的降低数据库的并发能力。上文说的，是使用悲观锁机制来处理这两种问题，但是MySQL、ORACLE、PostgreSQL等成熟的数据库，出于性能考虑，都是使用了以乐观锁为理论基础的MVCC（多版本并发控制）来避免这两种问题。[Link](https://www.cnblogs.com/itcomputer/articles/5133254.html)

##### 数据库并发事务的隔离功能

> 并发控制可以通过封锁来实现，但是封锁操作需要用户自己控制，相当复杂。数据库管理系统提供了事务的隔离级别，让用户以一种更轻松的方式处理并发一致性问题。
>
> >  SQL 标准描述了四个事务隔离级别（MySQL/InnoDB都提供）
> >
> > - **未提交读（READ UNCOMMITTED）**：事务中的修改，即使没有提交，对其它事务也是可见的；
> > - **提交读（READ COMMITTED）** ：一个事务只能读取已经提交的事务所做的修改。换句话说，一个事务所做的修改在提交之前对其它事务是不可见的。
> > - **可重复读（REPEATABLE READ）** ：保证在同一个事务中多次读取同样数据的结果是一样的。
> > - **可串行化（SERIALIXABLE）** ：强制事务串行执行。
> >
> >  **四个隔离级别的对比** 
> >
> > | 隔离级别 | 脏读 | 不可重复读 | 幻影读 |
> > | :------: | :--: | :--------: | :----: |
> > | 未提交读 | YES  |    YES     |  YES   |
> > |  提交读  |  NO  |    YES     |  YES   |
> > | 可重复读 |  NO  |     NO     |  YES   |
> > | 可串行化 |  NO  |     NO     |   NO   |
> >
> >  [Link](https://github.com/CyC2018/Interview-Notebook/blob/master/notes/%E6%95%B0%E6%8D%AE%E5%BA%93%E7%B3%BB%E7%BB%9F%E5%8E%9F%E7%90%86.md#%E5%9B%9B%E9%9A%94%E7%A6%BB%E7%BA%A7%E5%88%AB)

##### 基本锁功能

> - 粒度：MySQL 中提供了两种封锁粒度：行级锁以及表级锁。锁定的数据量越少，发生锁争用的可能就越小，系统的并发程度就越高。因此封锁粒度越小，系统开销就越大。
>
> > - 锁类型：
> >
> >   - 读写锁：排它锁（Exclusive），简写为 X 锁，又称**写锁**。共享锁（Shared），简写为 S 锁，又称**读锁**。
> >   - 意向锁：意向锁在原来的 X/S 锁之上引入了 IX/IS，IX/IS 都是表锁，用来表示一个事务想要在表中的某个数据行上加 X 锁或 S 锁。任意 IS/IX 锁之间都是兼容的，因为它们只是表示想要对表加锁，而不是真正加锁。
> >
> >   |  -   |  X   |  IX  |  S   |  IS  |
> >   | :--: | :--: | :--: | :--: | :--: |
> >   |  X   |  NO  |  NO  |  NO  |  NO  |
> >   |  IX  |  NO  | YES  |  NO  | YES  |
> >   |  S   |  NO  |  NO  | YES  | YES  |
> >   |  IS  |  NO  |  NO  | YES  | YES  |
> >
> > - 封锁协议
> >
> >   - **一级封锁协议**：解决丢失修改问题，事务 T 要修改数据 A 时必须加 X 锁，直到 T 结束才释放锁。
> >   - **二级封锁协议**：解决读脏数据问题，在一级的基础上，要求读取数据 A 时必须加 S 锁，读取完马上释放 S 锁。
> >   - **三级封锁协议**：解决不可重复读问题，在二级的基础上，要求读取数据 A 时必须加 S 锁，直到事务结束了才能释放 S 锁。
> >
> > - 解锁协议
> >   - 一次加锁：为了预防死锁，一般应用中推荐使用一次封锁法，就是在方法的开始阶段，已经预先知道会用到哪些数据，然后全部锁住，在方法运行之后，再全部解锁。但在数据库中却不适用，因为在事务开始阶段，数据库并不知道会用到哪些数据。
> >   - 两段锁协议：加锁和解锁分为两个阶段进行。事务 T 对数据 A 进行读或者写操作之前，必须先获得对 A 的封锁，并且在释放一个封锁之后，T 不能再获得任何的其它锁。这种方式虽然无法避免死锁，但是两段锁协议可以保证事务的**并发调度是串行化**（各个事务的操作没有交叉，也就没有相互干扰，当然也不会产生并发所引起的。）[Link](https://tech.meituan.com/innodb-lock.html)
> >
> >  [Link](https://github.com/CyC2018/Interview-Notebook/blob/master/notes/%E6%95%B0%E6%8D%AE%E5%BA%93%E7%B3%BB%E7%BB%9F%E5%8E%9F%E7%90%86.md#%E4%B8%89%E5%B0%81%E9%94%81)

##### MVCC（Multi-Version Concurrency Control，多版本并发控制）

> MVCC的实现没有固定的规范，每个数据库都会有不同的实现方式，这里讨论的是InnoDB的MVCC。
>
> >  在InnoDB中，会在每行数据后添加两个额外的隐藏的值来实现MVCC，这两个值一个记录这行数据何时被创建，另外一个记录这行数据何时过期（或者被删除）。 在实际操作中，存储的并不是时间，而是事务的版本号，每开启一个新事务，事务的版本号就会递增。 在可重读Repeatable reads事务隔离级别下：
> >
> > - SELECT时，读取创建版本号<=当前事务版本号，删除版本号为空或>当前事务版本号。
> > - INSERT时，保存当前事务版本号为行的创建版本号
> > - DELETE时，保存当前事务版本号为行的删除版本号
> > - UPDATE时，插入一条新纪录，保存当前事务版本号为行创建版本号，同时保存当前事务版本号到原来删除的行
> >
> >  通过MVCC，虽然每行记录都需要额外的存储空间，更多的行检查工作以及一些额外的维护工作，但可以减少锁的使用，大多数读操作都不用加锁，读数据操作很简单，性能很好，并且也能保证只会读取到符合标准的行，也只锁住必要行。在MySQL的RR（可重复读）级别中，是解决了幻读的读问题的。
> >
> >  在RR级别中，通过MVCC机制，虽然让数据变得可重复读，但我们读到的数据可能是历史数据，是不及时的数据，不是数据库当前的数据！对于这种读取历史数据的方式，我们叫它快照读 (snapshot read)，而读取数据库当前版本数据的方式，叫当前读 (current read)。很显然，在MVCC中：
> >
> > - 快照读：就是select
> >   - select * from table ....;
> > - 当前读：特殊的读操作，插入/更新/删除操作，属于当前读，处理的都是当前的数据，需要加锁。
> >   - select * from table where ? lock in share mode;
> >   - select * from table where ? for update;
> >   - insert;
> >   - update ;
> >   - delete;
> >
> >  事务的隔离级别中虽然只定义了读数据的要求，实际上这也可以说是写数据的要求。为了解决当前读中的幻读问题，MySQL事务使用了Next-Key锁。Next-Key锁是行锁和GAP（间隙锁）的合并。行锁防止别的事务修改或删除，GAP锁防止别的事务新增（锁定一个范围内的索引），行锁和GAP锁结合形成的的Next-Key锁共同解决了RR级别在写数据时的幻读问题。[Link](https://tech.meituan.com/innodb-lock.html)

##### MySQL 日志

> 主要包含：错误日志、查询日志、慢查询日志、事务日志、二进制日志；
>
> > - 在mysql数据库中，错误日志功能是默认开启的。
> > - 默认情况下查询日志是关闭的。由于查询日志会记录用户的所有操作，其中还包含增删查改等信息。
> > - 慢查询日志是用来记录执行时间超过指定时间的查询语句。
> > - 事务日志（InnoDB特有的日志）可以帮助提高事务的效率。使用事务日志，存储引擎在修改表的数据时只需要修改其内存拷贝，再把改修改行为记录到持久在硬盘上的事务日志中，而不用每次都将修改的数据本身持久到磁盘。
> > - 二进制日志也叫作变更日志，主要用于记录修改数据或有可能引起数据改变的mysql语句，并且记录了语句发生时间、执行时长、操作的数据等等。所以说通过二进制日志可以查询mysql数据库中进行了哪些变化。
> >
> >  [Link](http://blog.51cto.com/pangge/1319304)
> >
> >  Undo日志记录某数据被修改前的值，可以用来在事务失败时进行rollback；Redo日志记录某数据块被修改后的值，可以用来恢复未写入data file的已成功事务更新的数据。
> >
> >  [Link](http://www.letiantian.me/2014-06-18-db-undo-redo-checkpoint/)

##### MySQL 索引

> 索引是在存储引擎层实现的，而不是在服务器层实现的，所以不同存储引擎具有不同的索引类型和实现。
>
> >  分类：
> >
> >  - B+ Tree 索引
> >   - MyISAM 实现：使用B+Tree作为索引结构，叶节点的data域存放的是数据记录的地址。
> >   - InnoDB 实现：InnoDB的数据文件本身就是索引文件，所以InnoDB要求表必须有主键；InnoDB的辅助索引data域存储相应记录主键的值而不是地址。
> >
> >  [Link](http://blog.codinglabs.org/articles/theory-of-mysql-index.html)
> >
> >  - 哈希索引： Hash 索引结构的特殊性，其检索效率非常高，索引的检索可以一次定位。
> >
> >   - 由于 Hash 索引比较的是进行 Hash 运算之后的 Hash 值，所以它只能用于等值的过滤，不能用于基于范围的过滤
> >   - Hash 索引无法被用来避免数据的排序操作。
> >   - Hash 索引不能利用部分索引键查询。
> >
> >   [Link](https://blog.csdn.net/oChangWen/article/details/54024063)
> >
> >  - 全文索引：有时候有人叫倒排文档技术。先定义一个词库，然后在文章中查找每个词条(term)出现的频率和位置。这样就相当于对文件建立了一个以词库为目录的索引，这样查找某个词的时候就能很快的定位到该词出现的位置。
> >
> >  **查询性能优化**：
> >
> >  Explain
> >
> >  用来分析 SQL 语句，分析结果中比较重要的字段有：
> >
> >  - select_type : 查询类型，有简单查询、联合查询和子查询
> >  - key : 使用的索引
> >  - rows : 扫描的行数

##### 外键

> 外键的作用：保持数据一致性，完整性，主要目的是控制存储在外键表中的数据。 

> 指定主键关键字： foreign key(列名)
>
> 引用外键关键字： references <外键表名>(外键列名)

例子：

> ```sql
> create table temp(
> id int,
> name char(20),
> foreign key(id) references outTable(id) on delete cascade on update cascade);
> ```
>
> on delete和on update , 可设参数cascade(跟随外键改动), restrict(限制外表中的外键改动),set Null(设空值）,set Default（设默认值）,[默认]no action 
>
> 把 id 列设为 MySQL 外键，参照外表 outTable 的 id 列。当外键的值删除，本表中对应的列删除; 当外键的值改变 本表中对应的列值改变。 

##### SQL

> [Link](https://github.com/CyC2018/Interview-Notebook/blob/master/notes/SQL.md)
>
> > > **过滤**
> > >
> > > 下表显示了 WHERE 子句可用的操作符
> > >
> > > |   操作符    |      说明      |
> > > | :---------: | :------------: |
> > > | `=` `<` `>` | 等于 小于 大于 |
> > > |  `<>` `!=`  |     不等于     |
> > > |  `<=` `!>`  |    小于等于    |
> > > |  `>=` `!<`  |    大于等于    |
> > > |  `BETWEEN`  |  在两个值之间  |
> > > |  `IS NULL`  |   为 NULL 值   |
> > >
> > > 应该注意到，NULL 与 0、空字符串都不同。
> > >
> > > **AND 和 OR** 用于连接多个过滤条件。优先处理 AND，当一个过滤表达式涉及到多个 AND 和 OR 时，可以使用 () 来决定优先级，使得优先级关系更清晰。
> > >
> > > **IN** 操作符用于匹配一组值，其后也可以接一个 SELECT 子句，从而匹配子查询得到的一组值。
> > >
> > > **NOT** 操作符用于否定一个条件。
> > >
> > > **通配符**
> > >
> > > 通配符也是用在过滤语句中，但它只能用于文本字段。
> > >
> > > - **%** 匹配 >=0 个任意字符；
> > > - **_** 匹配 ==1 个任意字符；
> > > - **[ ]** 可以匹配集合内的字符，例如 [ab] 将匹配字符 a 或者 b。用脱字符 ^ 可以对其进行否定，也就是不匹配集合内的字符。
> > >
> > > 使用 Like 来进行通配符匹配。不要滥用通配符，通配符位于开头处匹配会非常慢。
> > >
> > > 

##### NoSQL一览 [Link](https://www.cnblogs.com/vajoy/p/5471308.html)



#### 题解

limit : 限制返回的行数。可以有两个参数，第一个参数为起始行，从 0 开始；第二个参数为返回的总行数。 

执行顺序：from -> join -> on -> where -> group by -> avg,sum,count,max ... -> having -> select -> distinct -> order by -> limit ;

`select a.FirstName, a.Lastname, b.City, b.State from Person a left join Address b on a.PersonId=b.PersonId;` [Link 175 Combine Two Tables](https://leetcode.com/problems/combine-two-tables/description/)

`select (SELECT DISTINCT Salary FROM Employee ORDER BY Salary DESC LIMIT 1 OFFSET 1) as SecondHighestSalary; ` [Link 176 Second Highest Salary](https://leetcode.com/problems/second-highest-salary/description/)

`select Score, (select count(*) from (select distinct Score s from Scores) temp where s>=Score) Rank from Scores order by Score desc;` [Link 178 Rank Scores](https://leetcode.com/problems/rank-scores/description/)

`select distinct l1.Num as ConsecutiveNums from Logs l1, Logs l2, Logs l3 where l1.Num=l2.Num and l2.Num=l3.Num and l2.Id=l1.Id+1 and l3.Id=l2.Id+1;` [Link 180 Consecutive Numbers](https://leetcode.com/problems/consecutive-numbers/description/) 

`select E1.Name as Employee from Employee E1 join Employee E2 on E1.ManagerId=E2.Id and E1.Salary>E2.Salary;` [Link 181 Employees Earning More Than Their Managers](https://leetcode.com/problems/employees-earning-more-than-their-managers/description/)

`select Email from (select Email, count(Email) c from Person group by Email) tmp where c>1; ` [Link 182 Duplicate Emails](https://leetcode.com/problems/duplicate-emails/description/)

`select Name Customers from Customers a left join Orders b on a.Id=b.CustomerId where CustomerId is null;` [Link 183 Customers Who Never Order](https://leetcode.com/problems/customers-who-never-order/description/)

`select d.Name Department, e.Name Employee, Salary from Employee e join Department d on e.DepartmentId=d.Id where (e.DepartmentId, Salary) in (select DepartmentId, max(Salary) from Employee group by DepartmentId);` [Link 184 Department Highest Salary](https://leetcode.com/problems/department-highest-salary/description/)

`select d.Name Department, e1.Name Employee, Salary from Employee e1 join Department d on e1.DepartmentId=d.Id where 3 > (select count(distinct e2.Salary) from Employee e2 where e2.Salary>e1.Salary and e2.DepartmentId=e1.DepartmentId) order by 1,3 desc;` [Link 185 Department Top Three Salaries](https://leetcode.com/problems/department-top-three-salaries/description/)

`delete p1 from Person p1, Person p2 where p1.Email=p2.Email and p1.Id>p2.Id;` [Link 196 Delete Duplicate Emails](https://leetcode.com/problems/delete-duplicate-emails/description/)

`select w1.Id from Weather w1, Weather w2 where datediff(w1.RecordDate, w2.RecordDate)=1 and w1.Temperature>w2.Temperature;` [Link 197 Rising Temperature](https://leetcode.com/problems/rising-temperature/description/)

```sql
SELECT Request_at AS Day , 
ROUND(SUM(Status = 'cancelled_by_driver' OR Status = 'cancelled_by_client') /count(*), 2) 
AS 'Cancellation Rate' 
FROM 
Trips tp, Users us 
WHERE us.Users_id = Client_id AND 
      us.Banned = 'No' AND 
      tp.Request_at >= '2013-10-01' AND tp.Request_at <= '2013-10-03'  
GROUP BY 
      tp.Request_at 
```

[Link 262 Trips and Users](https://leetcode.com/problems/trips-and-users/description/)

`select class from courses group by class having count(distinct student)>=5;` [Link 596 Classes More Than 5 Students](https://leetcode.com/problems/classes-more-than-5-students/description/)

```sql
select distinct s1.* from stadium as s1, stadium as s2, stadium as s3
where
    ((s1.id + 1 = s2.id and s1.id + 2 = s3.id)
    or (s1.id - 1 = s2.id and s1.id + 1 = s3.id)
    or (s1.id - 2 = s2.id and s1.id - 1 = s3.id))
    and s1.people >= 100 and s2.people >= 100 and s3.people >= 100
order by s1.id
```

[Link 601 Human Traffic of Stadium](https://leetcode.com/problems/human-traffic-of-stadium/description/)

`select * from cinema where id%2=1 and description != 'boring' order by rating desc;` [Link 620 Not Boring Movies](https://leetcode.com/problems/not-boring-movies/description/)

```sql
select
if(id < (select count(*) from seat), if(id mod 2=0, id-1, id+1), if(id mod 2=0, id-1, id)) as id, student
from seat
order by id asc;
```

[Link 626 Exchange Seats](https://leetcode.com/problems/exchange-seats/description/)

```sql
UPDATE salary
SET
    sex = CASE sex
        WHEN 'm' THEN 'f'
        ELSE 'm'
    END;
```

[Link 627 Swap Salary](https://leetcode.com/problems/swap-salary/description/)

