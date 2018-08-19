#### 分布式系统

##### CAP 原理

> 分布式领域[CAP理论](http://www.hollischuang.com/archives/666)告诉我们，任何一个分布式系统都无法同时满足Consistency(一致性),Availability(可用性), Partition tolerance(分区容错性) 这三个基本需求。最多只能满足其中两项。
>
> 一致性：更新操作成功并返回客户端完成后，所有节点在同一时间的数据完全一致。 `all nodes see the same data at the same time `
>
> 可用性：即服务一直可用，而且是正常响应时间。每一个非故障的节点必须对每一个请求作出响应。 `Reads and writes always succeed `
>
> 分区容错性：即分布式系统在遇到某节点或网络分区故障的时候，仍然能够对外提供满足一致性和可用性的服务。 `the system continues to operate despite arbitrary message loss or failure of part of the system `
>
> CAP 的证明：在两个节点之间网络断开的时候 ，当发生相同数据读写时。由于数据还没有进行同步，应用程序没办法立即给用户返回最新的数据，怎么办呢？有二种选择，第一，牺牲数据一致性，响应旧的数据给用户；第二，牺牲可用性，阻塞等待，直到网络连接恢复，数据更新操作完成之后，再给用户响应最新的数据。这个过程，证明了要满足分区容错性的分布式系统，只能在一致性和可用性两者中，选择其中一个。  
>
> [Link](http://www.hollischuang.com/archives/666)

##### 一致性

> 我们所说的分布式一致性问题通常指的是**数据一致性**问题。在分布式系统中，数据一致性往往指的是由于**数据的复制**，**不同数据节点**中的数据内容是否**完整并且相同**。一个系统如果想保证数据一致性很有**可能影响其性能**。因为并发的写请求需要在前一个写请求结束之后才能进行 **(排队)** 。
>
> >  一致性模型：
> >
> > - 强一致性：当更新操作完成之后，任何多个后续进程或者线程的访问都会返回最新的更新过的值。
> > - 弱一致性：系统并不保证后续进程或者线程的访问都会返回最新的更新过的值。
> > - 最终一致性：弱一致性的特定形式。系统保证在没有后续更新的前提下，系统最终返回上一次更新操作的值。
> >
> >  [Link](http://www.hollischuang.com/archives/663)

##### 分布式一致性协议/算法

> **分布式事务**是指会涉及到操作多个数据库的事务。分布式事务处理的关键是必须有一种方法可以知道事务在任何地方所做的所有动作，提交或回滚事务的决定必须产生统一的结果（全部提交或全部回滚）。
>
> > - **二阶段提交（2PC）**：参与者将操作成败通知协调者，再由协调者根据所有参与者的反馈情报决定各参与者是否要提交操作还是中止操作。所谓的两个阶段是指：第一阶段：**准备阶段(投票阶段)**和第二阶段：**提交阶段（执行阶段）**。四次握手。
> >
> >   缺点：1、**同步阻塞问题**；2、**单点故障导致阻塞**。由于协调者的重要性，一旦协调者发生故障。参与者会一直阻塞下去；3、**数据不一致**。协调者故障，只向部分节点发送 commit 命令；
> >
> > - **三阶段提交（3PC）**：引入超时机制之外，3PC 把 2PC 的准备阶段再次一分为二，这样三阶段提交就有 CanCommit、PreCommit、DoCommit 三个阶段。六次握手
> >
> >   ```
> >   在doCommit阶段，如果参与者无法及时接收到来自协调者的doCommit或者rebort请求时，会在等待超时之后，会继续进行事务的提交。
> >   ```
> >
> >   相对于2PC，3PC主要解决的单点故障问题，并减少阻塞。但是这种机制也会导致数据一致性问题。
> >
> >  [Link](http://www.hollischuang.com/archives/681)
> >
> > - **Paxos 算法**：主要解决的问题就是如何保证分布式系统中各个节点都能执行一个相同的操作序列。Paxos算法的目标就是按照少数服从多数的方式，最终达成一致意见。 
> >
> >   1、在整个提议和投票过程中，主要的角色就是“提议者”（向“接受者”提出提议）和“接受者”（收到“提议者”的提议后，向“提议者”表达自己的意见）。
> >
> >   2、整个算法的大致过程为：
> >   第一阶段：因为存在多个“提议者”， 要先明确哪个“提议者”是意见领袖有权提出提议，未来，“接受者”们就主要处理这个“提议者”的提议了**（这样，也可以在提出提议时就尽量让意见统一，谋求尽早形成多数派）。**
> >   第二阶段：由上阶段选出的意见领袖提出提议，“接受者”反馈意见。如果多数“接受者”接受了一个提议，那么提议就通过了。（“提议者”在贿选的时候，发现“接受者”已经接受过前面意见领袖的提议了，即便“提议者”贿选成功，也会默默的把自己的提议改为前面意见领袖的提议。）
> >
> >   [Link1](https://www.zhihu.com/question/19787937/answer/107750652) [Link2](http://www.hollischuang.com/archives/693) [Link3](https://zh.wikipedia.org/wiki/Paxos%E7%AE%97%E6%B3%95) [Link4](https://coolshell.cn/articles/10910.html)

#### 操作系统

##### 分页与虚拟内存

- 内存访问更为安全
- 共享内存更为简单
- 由于每个进程会有一套虚拟内存地址，那么每个进程都会有一个分页表。 

[Link](https://mp.weixin.qq.com/s/1Cj4swUbw23VoxAI4XvNdQ)

##### 同步与异步

> 所谓同步，就是在发出一个**调用**时，在没有得到结果之前，该*调用*就不返回。但是一旦调用返回，就得到返回值了。换句话说，就是由*调用者*主动等待这个**调用**的结果。
>
> >  而异步则是相反，**调用在发出之后**，这个调用就直接返回了，所以没有返回结果。换句话说，当一个异步过程调用发出后，调用者不会立刻得到结果。而是在调用发出后，被调用者通过状态、通知来通知调用者，或通过**回调函数**处理这个调用。
> >
> >  [Link](https://www.zhihu.com/question/19732473/answer/20851256)

##### 阻塞与非阻塞

> 阻塞和非阻塞关注的是**程序在等待调用结果**（消息，返回值）时的状态。
>
> >  阻塞调用是指调用结果返回之前，当前线程会被挂起。调用线程只有在得到结果之后才会返回。
> >  非阻塞调用指在不能立刻得到结果之前，该调用不会阻塞当前线程（不会被挂起）。
> >
> >  [Link](https://www.zhihu.com/question/19732473/answer/20851256)

##### buffer 与 cache 的区别

> Cache：高速缓存，是位于CPU与主内存间的一种容量较小但速度很高的存储器。
>
> >  Buffer：缓冲区，一个用于存储速度不同步的设备或优先级不同的设备之间传输数据的区域。通过缓冲区，可以使进程之间的相互等待变少，从而使从速度慢的设备读入数据时，速度快的设备的操作进程不发生间断。
> >
> >  [Link](http://blog.sina.com.cn/s/blog_93dc666c0101cb35.html)

##### 进程间通信

> - 管道/匿名管道 (pipe)；命名管道 (FIFO)
>
> >    半双工，单向，具有亲缘关系，内核缓冲区，无格式字节流，存在于内存中；无需具有亲缘关系，存在于文件系统中，内容存放在内存中。
> >
>  - 信号 (Signal)
> >
> >   信号是软件层次上对中断机制的一种模拟，是一种异步通信方式。
> >
> >   - 硬件来源：用户按键输入`Ctrl+C`退出、硬件异常如无效的存储访问等。
> >   - 软件终止：终止进程信号、其他进程调用kill函数、软件异常产生信号。
> >
>  - 消息队列 (Message)
> >
> >   消息队列是消息的链表，具有特定的格式，可随机查询，无需等待写入
> >
>  - 共享内存 (share memory)
> >
> >   使得多个进程可以可以直接读写同一块内存空间，是最快的可用 IPC 形式。需要依靠某种同步机制（如信号量）来达到进程间的同步及互斥。
> >
>  - 信号量 (semaphore)
> >
> >   信号量是一个计数器，用于多进程对共享数据的访问，信号量的意图在于进程间同步。信号量值的测试及减 1 操作应当是原子操作。
> >
> >   互斥量用于线程的互斥，信号量用于线程的同步。
> >
>  - 套接字 (socket)
> >
> >   客户/ 服务器（即要进行通信的进程）系统的开发工作既可以在本地单机上进行，也可以跨网络进行。
> >
> >   套接字是支持 TCP/IP 的网络通信的基本操作单元。
> >
> >   套接字的特性由3个属性确定，它们分别是：域(AF_INET, AF_UNIX) 、端口号、协议类型。
> >
> 
>  [Link](https://www.jianshu.com/p/c1015f5ffa74) [Demo](https://songlee24.github.io/2015/04/21/linux-IPC/)

##### 信号量与互斥量的区别

> 互斥量用于线程的互斥，信号量用于线程的同步。
>
> >  **互斥：**是指某一资源同时只允许一个访问者对其进行访问，具有唯一性和排它性。但互斥无法限制访问者对资源的访问顺序，即访问是无序的。
> >
> >  **同步：**是指在互斥的基础上（大多数情况），通过其它机制实现访问者对资源的有序访问。
> >
> >  信号量可以实现多个同类资源的多线程互斥和同步。互斥量的加锁和解锁必须由同一线程分别对应使用，信号量可以由一个线程释放，另一个线程得到。
> >
> >  [Link](https://www.jianshu.com/p/c1015f5ffa74)

##### 进程与线程的区别

> - 一个程序至少有一个进程,一个进程至少有一个线程；
>
> > - 进程是系统进行资源分配和调度的一个独立单位，线程是CPU调度和分派的基本单位，它是比进程更小的能独立运行的基本单位。
> > - 进程在执行过程中拥有独立的内存单元，而多个线程共享内存，从而极大地提高了程序的运行效率；
> > - 一个进程崩溃后，在保护模式下不会对其它进程产生影响，一个线程死掉就等于整个进程死掉，所以多进程的程序要比多线程的程序健壮，但在进程切换时，耗费资源较大，效率要差一些。
> >
> > [Link](http://www.cnblogs.com/lmule/archive/2010/08/18/1802774.html)

> 分点回答
>
> > - 拥有资源：进程是资源分配的基本单位，但是线程不拥有资源，线程可以访问隶属进程的资源。
> > - 调度：线程是独立调度的基本单位，在同一进程中，线程的切换不会引起进程切换，从一个进程内的线程切换到另一个进程中的线程时，会引起进程切换。
> > - 系统开销：由于创建或撤销进程时，系统都要为之分配或回收资源，如内存空间、I/O 设备等，所付出的开销远大于创建或撤销线程时的开销。类似地，在进行进程切换时，涉及当前执行进程 CPU 环境的保存及新调度进程 CPU 环境的设置，而线程切换时只需保存和设置少量寄存器内容，开销很小。
> > - 通信方面：进程间通信 (IPC) 需要进程同步和互斥手段的辅助，以保证数据的一致性。而线程间可以通过直接读/写同一进程中的数据段（如全局变量）来进行通信。
> >   [Link](https://github.com/CyC2018/Interview-Notebook/blob/master/notes/%E8%AE%A1%E7%AE%97%E6%9C%BA%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F.md#3-%E5%8C%BA%E5%88%AB)

##### fork

> 如果进程需要启动另一个程序的可执行文件，它需要先Fork来创建一个自身的副本。然后由该副本即“[子进程](https://zh.wikipedia.org/wiki/%E5%AD%90%E8%BF%9B%E7%A8%8B)”调用[exec](https://zh.wikipedia.org/w/index.php?title=Exec&action=edit&redlink=1)系统调用，用其他程序覆盖自身：停止执行自己之前的程序并执行其他程序。

- fork 之后，子进程的下一条语句与父进程的下一条语句一样。
- 通过检查 fork 返回值来判断是子进程还是父进程。
  - 在父进程中，fork返回新创建子进程的进程ID；
  - 在子进程中，fork返回0；
  - 如果出现错误，fork返回一个负值；

##### 线程池的实现

  多线程进程：每个线程执行的都是进程代码的某个片段啊。

- 当线程池的线程刚创建时，让他们进入阻塞状态：等待某个任务的到来。 如果任务来了，那就好办，唤醒其中一个线程，让它拿到任务去执行即可。

- BlockingQueue：一个线程调用它的take()方法取数据时， 如果这个Queue中没有数据，该线程会阻塞；同样，一个线程调用它的put方法放数据时，如果Queue满了， 也会阻塞。

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

##### 进程调度算法

不同环境的调度算法目标不同，因此需要针对不同环境来讨论调度算法。 

- 批处理系统，批处理系统没有太多的用户操作 ，在该系统中，调度算法目标是保证吞吐量和周转时间 。

  非抢占式：先来先服务 FCFS；短作业优先 SJF；

  抢占式：最短剩余时间有限 SRTN。

- 交互式系统：交互式系统有大量的用户交互操作，在该系统中调度算法的目标是快速地进行响应。 

  时间片轮转 + FCFS；优先级调度；多级反馈队列；

- 实时系统

  要求一个请求在一个确定时间内得到响应。 

##### 进程同步

- 经典同步问题
  - 生产者-消费者问题：使用一个缓冲区来保存物品 ，因为缓冲区属于临界资源，因此需要使用一个互斥量 mutex 来控制对缓冲区的互斥访问。 使用互斥量 + 信号量的方法实现。也可用管程实现。
  - 读者-写者问题：允许多个进程同时对数据进行读操作，但是不允许读和写以及写和写操作同时发生。 使用两个互斥量对读写进行控制。
  - 哲学家进餐问题：死锁。
    - 只有在两个邻居都没有进餐的情况下才允许进餐。
    - 必须同时拿起左右两根筷子；
- 同步方法
  - 信号量：是一个整型变量 。可以对其执行 down 和 up 操作，需要被设计成原语，不可分割，通常的做法是在执行这些操作的时候屏蔽中断 。信号量的取值只能为 0 或者 1，那么就成为了 互斥量（Mutex）。
  - 管程： 管程可以看做一个软件模块，它是将共享的变量和对于这些共享变量的操作封装起来，形成一个具有一定接口的功能模块，进程可以调用管程来实现进程级别的并发控制。进程只能互斥得使用管程，即当一个进程使用管程时，另一个进程必须等待。当一个进程使用完管程后，它必须释放管程并唤醒等待管程的某一个进程。

##### 内存管理

- 虚拟内存

  操作系统将内存抽象成地址空间 ，每个程序拥有自己的地址空间，这个地址空间被分割成多个块，每一块称为一页。这些页被映射到物理内存，但不需要映射到连续的物理内存，也不需要所有页都必须在物理内存中。 

- 分页系统地址映射

  - 内存管理单元（MMU）：管理着地址空间和物理内存的转换。
  - 页表（Page table）：页（地址空间）和页框（物理内存空间）的映射表。

- 页面置换算法

  - 最佳 Optimal

    所选择的被换出的页面将是最长时间内不再被访问，通常可以保证获得最低的缺页率。 

  - 先进先出 FIFO

    所选择换出的页面是最先进入的页面。该算法会将那些经常被访问的页面也被换出，从而使缺页率升高。

  - 第二次机会算法

    第二次机会算法就是寻找一个最近的时钟间隔以来没有被访问过的页面。 

  - 时钟 Clock

    第二次机会算法的循环队列模式，不再从队列头开始查找，而是从当前指针指向开始查找。

  - 最近未使用 Not Recently Used

    系统为毎一页面设置了两个状态位。 当页面被访问 (读或写) 时设置 R 位; 当页面 (即修改页面) 被写入时设置 M 位。 NRU 算法随机地从状态位编号最小的非空类中挑选一个页面淘汰之。 

  - 最近最久未使用 Least Recently Used

- 分段

  程序的地址空间划分成多个拥有独立地址空间的段，每个段上的地址空间划分成大小相同的页。这样既拥有分段系统的共享和保护，又拥有分页系统的虚拟内存功能。 

  段页式：为了进行地址转换，系统为每个作业建立一个段表，并且要为该作业段表中的每一个段建立一个页表。 

[Link](https://github.com/CyC2018/Interview-Notebook/blob/master/notes/%E8%AE%A1%E7%AE%97%E6%9C%BA%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F.md#%E5%9B%9B%E5%86%85%E5%AD%98%E7%AE%A1%E7%90%86)

##### 磁盘调度算法

读写一个磁盘块的时间的影响因素有：

- 旋转时间（主轴旋转磁盘，使得磁头移动到适当的扇区上）
- 寻道时间（制动手臂移动，使得磁头移动到适当的磁道上）
- 实际的数据传输时间

其中，寻道时间最长，因此磁盘调度的主要目标是使磁盘的平均寻道时间最短。

先来先服务 FCFS；最短寻道时间有限 SSTF；电梯算法 SCAN。

[Link](https://github.com/CyC2018/Interview-Notebook/blob/master/notes/%E8%AE%A1%E7%AE%97%E6%9C%BA%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F.md#%E7%A3%81%E7%9B%98%E8%B0%83%E5%BA%A6%E7%AE%97%E6%B3%95)

##### 死锁

- 必要条件

  - 互斥，占有和等待，不可抢占，环路等待。

- 鸵鸟策略

  因为解决死锁问题的代价很高 ，因此大多数操作系统，包括 Unix，Linux 和 Windows，处理死锁问题的办法仅仅是忽略它。 

- 死锁预防

  在程序运行之前预防发生死锁。 破坏死锁的四个条件中的一个或几个条件，来预防发生死锁。 [Link](https://github.com/CyC2018/Interview-Notebook/blob/master/notes/%E8%AE%A1%E7%AE%97%E6%9C%BA%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F.md#3-%E6%AD%BB%E9%94%81%E9%A2%84%E9%98%B2)

- 死锁避免

  在程序运行时避免发生死锁。 

  - 安全状态

    存在某种调度次序能够使得每一个进程运行完毕，则称该状态是安全的。 

  - 单个资源的银行家算法

    算法要做的是判断对请求的满足是否会进入不安全状态，如果是，就拒绝请求；否则予以分配。（与多个资源的死锁检测类似）

  - 多个资源的银行家算法

    [算法](https://github.com/CyC2018/Interview-Notebook/blob/master/notes/%E8%AE%A1%E7%AE%97%E6%9C%BA%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F.md#4-%E6%AD%BB%E9%94%81%E9%81%BF%E5%85%8D)

- 死锁检测与死锁恢复

  - 每种类型一个资源的死锁检测 

    通过检测有向图是否存在环来实现 。

  - 每种类型多个资源的死锁检测

    与多个资源的银行家算法类似

  - 死锁恢复

    - 利用抢占恢复， 利用回滚恢复，通过杀死进程恢复

#### Linux

##### free

- 查看系统中的内存使用情况

##### 查看进程内存使用

`ps aux | grep name` 得到进程 ID

- `cat /proc/id/status`  查看占用大小
- top -p id 查看

##### 进入 root 

`sudo su`

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

`touch:修改文件的访问和修改时间`

  [Link](http://blog.csdn.net/ljianhui/article/details/11100625)

##### shell 统计文件中单词出现的次数

  `wc -c 统计字节数，-l 统计行数，-w 统计字数，-m 统计字符数 `

  `grep cout hello.cpp | wc -l # 统计出现 cout 的行数`

  `grep -o cout hello.cpp | wc -l # 统计出现 cout 的次数`

##### 查看某个端口是否被占用

```bash
$ sudo lsof -i # 查看端口占用情况
$ sudo lsof -i:21 # 查看 21 号端口是否被占用
$ netstat -apn | grep 21 
```

##### 找出出现次数最多的前三个 ip 及次数

`sort ip.txt | uniq -c | sort -rn | head -n 3`

- sort 按 ASCII 码排序 -n 依照数值大小排序 -r 反向
- uniq -c 统计相邻的不重复项

##### umask

> umask 是设置系统创建文件时的默认权限**补码**，默认权限是 666 ，umask设为 244 ，则创建文件的权限为 422 .

##### 查找可执行文件

- `whereis` ：用于定位可执行文件、源代码文件、帮助文件在文件系统中的位置。 

    ```shell
    $ whereis test
    -b   # 定位可执行文件。
    -m   # 定位帮助文件。
    -s   # 定位源代码文件。
    -u   # 搜索默认路径下除可执行文件、源代码文件、帮助文件以外的其它文件。
    ```

- `locate` ：事先建立系统内所有档案名称及路径的数据库，查询时只需查询这个数据库，因此查询速度比 `find` 快，但查找不是实时的，而是以数据库的更新为准。

  ```shell
  $ sudo updatedb  # 更新数据库
  $ locate /etc/sh # 查找etc目录下所有以sh开头的文件
  -n # 限制显示个数
  -i # 忽略大小写
  -r # 正则查询 ^file 以file开头 file$ 以file结尾
  ```

- `which` ：在PATH变量指定的路径中，搜索某个系统命令的位置，并且返回第一个搜索结果。 

    ```shell
    $ which which
    ```

- `type` ：判断一个名字当前是否是alias、keyword、function、builtin、file或者什么都不是。

    ```shell
    $ type ls # 输出 "ls 是 `ls --color=auto' 的别名"
    $ type -t ls # 输出 "alias"
    $ type -a kill # 显示所有可能
    $ type -p gedit # 显示命令可执行路径
    ```

- `find` ：在目录结构中搜索文件，并执行指定的操作。 由于find具有强大的功能，所以它的选项也很多 。

    ```shell
    $ find pathname -options [-print -exec -ok ...]
    $ find -atime 2 # 超找48小时内访问过的文件 
    $ find . -name "*.log" # 在当前目录查找 以.log结尾的文件。 ". "代表当前目录 
    $ find /opt/soft/test/ -perm 777 # 查找/opt/soft/test/目录下,权限为777的文件
    $ find . -type f -name "*.log" # 查找当目录，以.log结尾的普通文件 
    $ find . -type d | sort # 查找当前所有目录并排序
    $ find . -size +1000c -print # 查找当前目录大于1K的文件
    ```


##### shell 信号

- 挂起，运行

```shell
$ ctrl+z : # 停止进程并放入后台，SIGSTP 信号
$ ctrl+c ：# 终止进程 SIGINT
$ ctrl+d : # 输入 EOF
$ ./game.e 1 & # & 放在启动参数后面表示设置此进程为后台进程
$ jobs # 显示当前暂停进程
$ bg %n # 使第 n 个任务在后台运行
$ fg %n # 使第 n 个任务在前台运行
```

- kill

```shell
$ kill -l # 列出所有信号
$ kill -l CONT # 打印出信号对应的序号
$ # HUP 1 终端断线 / INT 2 中断（ctrl+c）/ QUIT 3 退出（ctrl+\）/ TERM 15 终止（默认）/ KILL 9 强制终止 / CONT 18 继续（fg/bg）/ STOP 19 暂停（ctrl+z）
$ kill -9 $(ps -ef | grep user)
$ kill -u user # 杀死指定用户所有进程
```

##### 守护进程

> ["守护进程"](http://baike.baidu.com/view/53123.htm)（daemon）就是一直在后台运行的进程（daemon）。类似Windows服务 ，并且不会因Shell退出而退出 。

创建守护进程方法：

1. 改成后台任务，利用 `&` 或者 `ctrl-z + bg`  ；按 `ctrl-d` 退出当前 session （shell），保留后台任务继续运行。
2. 改成后台任务；使用 `disown` 命令；可以将指定任务从"后台任务"列表（`jobs`命令的返回结果）之中移除。一个"后台任务"只要不在这个列表之中，session 就肯定不会向它发出`SIGHUP`信号。 
3. 读写 I/O ，发现不存在会报错终止执行。需要对后台任务的标准 I/O 进行重定向。 `node server.js > stdout.txt 2> stderr.txt < /dev/null &`
4. `nohup node server.js &`；nohup 做了三件事：阻止`SIGHUP`信号发到这个进程；关闭标准输入。该进程不再能够接收任何输入，即使运行在前台；重定向标准输出和标准错误到文件`nohup.out`。
5. 使用终端复用器：`Screen` 和 `Tmux` ；可以在当前 session 里面，新建另一个 session 。

后台任务特点：

1. 继承当前 session （对话）的标准输出（stdout）和标准错误（stderr）。因此，后台任务的所有输出依然会同步地在命令行下显示。
2. 不再继承当前 session 的标准输入（stdin）。你无法向这个任务输入指令了。如果它试图读取标准输入，就会暂停执行（halt）。

session 退出流程：

1. 用户准备退出 session
2. 系统向该 session 发出`SIGHUP`信号
3. session 将`SIGHUP`信号发给所有子进程；（一般不会发送给后台任务，因此不会随着 session 一起退出。）
4. 子进程收到`SIGHUP`信号后，自动退出

[Link](http://www.ruanyifeng.com/blog/2016/02/linux-daemon.html)

##### select / poll / epoll

[Link](https://blog.csdn.net/lixungogogo/article/details/52226501)

### C++ 并发编程

#### 第一章 并发

##### 1.1 并发方式

- 多进程并发

> 缺点：进程间通信设置复杂，速度慢（因为操作系统的保护措施）；进程有固定开销，需要启动时间，需要资源来管理进程。
>
> 优点：操作系统的安全保护以及更高级别的通信机制，可以更容易编写安全的并发代码；进程可以通过远程连接，实现多台机器的多进程。

- 多线程并发

> 优点：进程中的所有线程共享地址空间，全局变量仍是全局，指针、对象的引用或者数据可以在线程之间传递。而进程间共享内存难以建立和管理，同一数据的内存地址在不同的进程中是不相同的。
>
> 缺点：需要保证数据的一致性。

##### 1.2 为何使用并发

- 分离关注点

> 将相关的代码与无关的代码分离，更容易理解和测试，例如将 DVD 播放程序的播放程序与用户响应程序分离。这种情况下，线程划分不再基于 CPU，而是基于功能的设计。

- 性能

> 并行。两种方式利用并发提高性能：
>
> 1. 任务并行：将单个任务分成几个部分，并行运行，降低总运行时间，任务间可能存在依赖。又称易并行
> 2. 数据并行：每个线程在不同的数据部分上执行相同的操作。

- 何时不用并发

> 1. 任务运行快，比启动线程快。
> 2. 线程是有限资源，运行太多的线程会耗尽进程的可用内存或地址空间。如 4GB 的地址空间，每个线程都有 1MB 的堆栈，那么 4096 个线程会用尽所有空间。可以用线程池来限制线程的数量。
> 3. 线程越多，需要做越多的上下文切换。

##### 1.3 C++ 中的并发和多线程

- 第二章：管理线程；第三章：保护共享数据；第四章：线程间同步；第五章：低级原子操作

##### 1.4 开始入门

- hello world

  ```c++
  #include <iostream>
  #include <thread>  //①
  void hello()  //②
  {
    std::cout << "Hello Concurrent World\n";
  }
  int main()
  {
    std::thread t(hello);  //③
    t.join();  //④
  }
  ```

#### 第二章 线程管理

内容：启动线程；等待线程接收或放在后台运行；传递参数；转移线程所有权；确定线程数以及识别特殊线程。

##### 2.1 基础

**2.1.1 启动线程**

- 在为一个线程创建了一个 `std::thread` 对象后，需要等待这个线程结束。

- 启动线程

  ```c++
  std::thread my_thread(f); // f 可以是普通函数，或者有函数调用符类型的实例
  ```

  若传入的是实例，则会被复制到新线程的存储空间中，执行和调用都在线程的内存空间中进行。**需注意**：如果传递一个临时变量，而不是一个命名的变量，编译器会将其解析为函数声明。1 和 2 可以解决该问题。

  ```c++
  std::thread my_thread(background_task()); // 相当于声明函数。
  std::thread my_thread((background_task()));  // 1
  std::thread my_thread{background_task()};    // 2
  ```

  传入 lambda 表达式

  ```c++
  std::thread my_thread([]{
    do_something();
    do_something_else();
  });
  ```

- 注意

> 1. 启动线程后要明确等待线程结束（join）还是让其自主运行（detach）。如果 thread **销毁**之前还未绝对，thread 的析构函数会调用 terminate 函数终止程序。
> 2. 如果不等待进程，必须保证线程可访问数据的有效性。例如当线程还没结束，函数已经退出，局部变量的指针和引用就无效。可以将对象复制到线程中（注意指针和引用）

**2.1.2 等待线程完成**

- join() 简单粗暴的等待线程完成。并清理线程相关的存储部分。因此一个线程只能 join 一次。

**2.1.3 异常等待线程完成**

- 在有异常的情况下 join 。在 join 前出现异常，join 不会被调用到。有两种办法，用 try/catch 和 RAII 方法。

  ```c++
  // try catch
  struct func; // 定义在清单2.1中
  void f()
  {
    int some_local_state=0;
    func my_func(some_local_state);
    std::thread t(my_func);
    try
    {
      do_something_in_current_thread();
    }
    catch(...)
    {
      t.join();  // 1 保证不管有没有异常都会调用 t.join()
      throw;
    }
    t.join();  // 2
  }
  // RAII 在析构函数中使用 join()
  class thread_guard
  {
    std::thread& t;
  public:
    explicit thread_guard(std::thread& t_):
      t(t_)
    {}
    ~thread_guard()
    {
      if(t.joinable()) // 1
      {
        t.join();      // 2
      }
    }
    thread_guard(thread_guard const&)=delete;   // 3
    thread_guard& operator=(thread_guard const&)=delete;
  };
  
  struct func; // 定义在清单2.1中
  
  void f()
  {
    int some_local_state=0;
    func my_func(some_local_state);
    std::thread t(my_func);
    thread_guard g(t);
    do_something_in_current_thread(); // 即使异常 thread_guard 的析构也会被调用
  }    // 4
  ```

**2.1.4 后台运行线程**

- detach() 让线程在后台运行。不用等待该线程结束。C++ 运行库会负责资源回收。分离线程又称为守护线程。

##### 2.2 传递参数

- 可以传递默认参数以及字符串字面值。若传递动态变量，尽量提前进行转换。

- thread 会将参数复制到其独立内存中，就无法试图通过引用保存更改结果。可以使用 `std::ref` 将参数转换成引用。

-  传递一个成员函数作为线程函数，并提供一个合适的对象指针作为第一个参数。

- 移动传递参数，如 unique_ptr ：当原变量是一个临时变量是，自动进行移动操作，但当原对象是一个命名变量，就需要使用 `std::move()` 显示移动。

- 转移执行线程的所有权：thread 可移动不可复制，与 unique_ptr 类似。

  ```c++
  // 传递常量
  void f(int i, std::string const& s);
  std::thread t(f, 3, "hello");
  // 传递引用
  std::thread t(update_data_for_widget,w,std::ref(data));
  // 调用成员函数
  X my_x;
  std::thread t(&X::do_lengthy_work,&my_x); // 1
  // 移动
  void process_big_object(std::unique_ptr<big_object>);
  std::unique_ptr<big_object> p(new big_object);
  std::thread t(process_big_object,std::move(p));
  ```

##### 2.3 转移线程所有权

- 移动

  ```c++
  void some_function();
  void some_other_function();
  std::thread t1(some_function);            // 1
  std::thread t2=std::move(t1);            // 2
  t1=std::thread(some_other_function);    // 3 临时变量将会隐式调用移动操作
  std::thread t3;                            // 4
  t3=std::move(t2);                        // 5
  t1=std::move(t3);                        // 6 赋值操作将使程序崩溃，调用 std::terminate() 
  ```

- thread 在函数间转移

  ```c++
  std::thread f()
  {
    void some_function();
    return std::thread(some_function);
  }
  
  std::thread g()
  {
    void some_other_function(int);
    std::thread t(some_other_function,42);
    return t; // 编译器自动执行移动操作
  }
  
  void f(std::thread t);
  std::thread t(some_function);
  f(std::move(t));
  ```

- 创建 thread_guard 类管理 thead

  ```c++
  class scoped_thread
  {
    std::thread t;
  public:
    explicit scoped_thread(std::thread t_):                 // 1
      t(std::move(t_))
    {
      if(!t.joinable())                                     // 2
        throw std::logic_error(“No thread”);
    }
    ~scoped_thread()
    {
      t.join();                                            // 3
    }
    scoped_thread(scoped_thread const&)=delete;
    scoped_thread& operator=(scoped_thread const&)=delete;
  };
  
  struct func; // 定义在清单2.1中
  
  void f()
  {
    int some_local_state;
    scoped_thread t(std::thread(func(some_local_state)));    // 4
    do_something_in_current_thread();
  }                                                        // 5
  ```

- 用 vector 存 thread

  ```c++
  void do_work(unsigned id);
  
  void f()
  {
    std::vector<std::thread> threads;
    for(unsigned i=0; i < 20; ++i)
    {
      threads.push_back(std::thread(do_work,i)); // 产生线程
    } 
    std::for_each(threads.begin(),threads.end(),
                    std::mem_fn(&std::thread::join)); // 对每个线程调用join()
  }
  ```

##### 2.4 运行时决定线程数量

- `std::thread::hardware_concurrency()` 可以返回一个程序中能并行的线程数量。
- 实现并行版的 accumulate

##### 2.5 识别线程

- 线程标识符类型 `std::thread::id` 可以通过 thread 对象的 get_id() 直接获取。也可以在当前对象中调用 `std::this_thread::get_id()` 获得。

#### 第三章 线程间共享数据

内容：共享数据带来的问题；使用互斥量保护数据；数据保护的替代方案

##### 3.1 共享数据带来的问题

- 共享数据修改所导致的。
- 不变量：如双链表中的两个指针就是不变量，为了删除节点，其两边节点的指针都要更新，当一边更新完成，不变量就被破坏了，两边都更新完成，不变量就稳定了。

**3.1.1 条件竞争**

- 恶性条件竞争通常发生于完成对多于一个的数据块的修改时。

**3.1.2 避免恶性条件竞争**

- 对数据结果采用保护机制确保只有进行修改的线程才能看到不变量被破坏时的中间状态。

##### 3.2 使用互斥量保护共享数据

**3.2.1 使用互斥量**

- 实例化 `std::mutex` 创建互斥量，调用 lock() 上锁，调用 unlock() 解锁。C++ 标准库提供一个 RAII 语法的模板类 `std::lock_guard()` ，在构造的时候已锁的互斥量，并在析构的时候进行解锁。

  ```c++
  #include <list>
  #include <mutex>
  #include <algorithm>
  
  std::list<int> some_list;    // 1
  std::mutex some_mutex;    // 2
  
  void add_to_list(int new_value)
  {
    std::lock_guard<std::mutex> guard(some_mutex);    // 3
    some_list.push_back(new_value);
  }
  ```

- 大多数情况下，互斥量会与保护的数据放在同一个类中，并把对数据操作的函数作为成员函数。但当成员函数返回的时保护数据的指针或引用时，会破坏对数据的保护。

**3.2.2 精心组织代码来保护数据**

- 切勿将受保护数据的指针或引用传递到互斥锁作用域之外，无论是函数返回值，还是存储在外部可见内存，亦或是以参数的形式传递到用户提供的函数中去。 

**3.2.3 发现接口内在的条件竞争**

- 如双链表的例子中，删除一个节点，需要确保对三个节点的并发访问。可以使用互斥量来保护整个链表。

- 多个接口一起作用：如一个栈，`empty()` 返回时是正确的，但在调用 `top()` 时，可能其他线程对栈做了其他操作，致使栈为空。`top()` 和 `pop()` 也会有竞争。

  ```c++
  stack<int> s;
  if (! s.empty()){    // 1
    int const value = s.top();    // 2
    s.pop();    // 3
    do_something(value);
  }
  ```

- `stack<vector<int>>` 当系统负荷较大，pop() 弹出，`vector<int>` 分配异常，导致数据丢失，所以将 pop() 分为 top() 和 pop() 两步。但这造成了竞争。

  ```c++
  // 线程安全的堆栈，简化接口，只留 pop 和 push 以及 empty，pop 空抛出异常。
  #include <exception>
  #include <memory>
  #include <mutex>
  #include <stack>
  
  struct empty_stack: std::exception
  {
    const char* what() const throw() {
      return "empty stack!";
    };
  };
  
  template<typename T>
  class threadsafe_stack
  {
  private:
    std::stack<T> data;
    mutable std::mutex m;
  
  public:
    threadsafe_stack()
      : data(std::stack<T>()){}
  
    threadsafe_stack(const threadsafe_stack& other)
    {
      std::lock_guard<std::mutex> lock(other.m);
      data = other.data; // 1 在构造函数体中的执行拷贝
    }
  
    threadsafe_stack& operator=(const threadsafe_stack&) = delete;
  
    void push(T new_value)
    {
      std::lock_guard<std::mutex> lock(m);
      data.push(new_value);
    }
  
    std::shared_ptr<T> pop()
    {
      std::lock_guard<std::mutex> lock(m);
      if(data.empty()) throw empty_stack(); // 在调用pop前，检查栈是否为空
  
      std::shared_ptr<T> const res(std::make_shared<T>(data.top())); // 在修改堆栈前，分配出返回值
      data.pop();
      return res;
    }
  
    void pop(T& value)
    {
      std::lock_guard<std::mutex> lock(m);
      if(data.empty()) throw empty_stack();
  
      value=data.top();
      data.pop();
    }
  
    bool empty() const
    {
      std::lock_guard<std::mutex> lock(m);
      return data.empty();
    }
  };
  ```

- 细粒度锁能带来更好的性能，但会有更多的竞争。同时一个给定的操作需要两个或两个以上的互斥量时，可能会出现死锁。

**3.2.4 死锁：问题描述及解决方案**

- 避免死锁的一般建议，就是让两个互斥量总以相同的顺序上锁：总在互斥量B之前锁住互斥量A，就永远不会死锁。 

- 不是万能：多个互斥量琐多个实例，实例要交换，先锁第一个参数再锁第二个参数，当两个线程以不同的参数顺序交换两个相同的实例时，会发生死锁。

- `std::lock()` 可以一次性锁多个互斥量，并且没有死锁风险。用 `lock_guard` 保证释放锁。

  ```c++
  // 这里的std::lock()需要包含<mutex>头文件
  class some_big_object;
  void swap(some_big_object& lhs,some_big_object& rhs);
  class X
  {
  private:
    some_big_object some_detail;
    std::mutex m;
  public:
    X(some_big_object const& sd):some_detail(sd){}
  
    friend void swap(X& lhs, X& rhs)
    {
      if(&lhs==&rhs)
        return;
      std::lock(lhs.m,rhs.m); // 1
      std::lock_guard<std::mutex> lock_a(lhs.m,std::adopt_lock); // 2
      std::lock_guard<std::mutex> lock_b(rhs.m,std::adopt_lock); // 3
      swap(lhs.some_detail,rhs.some_detail);
    }
  };
  ```

**3.2.5 避免死锁的指导** 

- 避免嵌套锁
- 避免再持有锁时调用用户提供的代码
- 使用固定顺序获取锁
- 使用锁的层次结构
- 超越锁的延申拓展：死锁也会发生再任何同步事件中。

**3.2.6 std::unique_lock 灵活的锁**

同 `std::lock_guard()` ，但有更多的可配置项。

**3.2.7 不同域中互斥量所有权的传递**

`std::unique_lock` 可移动

**3.2.8 锁的粒度**

##### 3.3 保护共享数据的替代措施

**3.3.1保护数据的初始化过程**

- 延迟初始化。在并发环境中，会使线程序列化。采用双重锁模式，会出现条件竞争。
- 可以通过 `std::once_flag` 和 `std::call_once` 来处理这种情况。

**3.3.2 保护很少更新的数据**

- 如 DNS 缓存表。读取/写入都使用互斥锁会降低并发性。可以采用读写锁
- `boost::shared_mutex` 通过 `boost::shared_lock()` 可以进行共享锁，通过 `std::lock_guard` 可以进行独享锁。

**3.3.3 嵌套锁**

- 同一个线程多次对 `std::mutex` 再次上锁会出错。`std::rucursive__mutex` 能实现多次上锁。
- 嵌套锁一般用在可并发访问的类上。如一个成员函数调用另一个成员函数。也可以将其提取为一个私有函数。

#### 第四章 同步并发操作

##### 4.1 等待一个事件或其他条件

有三种等待方式：

1. 不断检查任务是否完成的标准（互斥量）。会降低性能。

2. 休眠一段时间检查一次。休眠时长无法估计。

   `std::this_thread::sleep_for(std::chrono::milliseconds(100));  // 2 休眠100ms`

3. 通过线程触发等待事件的机制。称为条件变量

**4.1.1 等待条件达成**

C++标准库对条件变量有两套实现：`std::condition_variable`和`std::condition_variable_any`。这两个实现都包含在`<condition_variable>`头文件的声明中。 `std::condition_variable_any` 较灵活但性能差，一般用第一个。两者都需要与一个互斥量一起才能工作(互斥量是为了同步)。

```c++
std::mutex mut;
std::queue<data_chunk> data_queue;  // 1
std::condition_variable data_cond;

void data_preparation_thread()
{
  while(more_data_to_prepare())
  {
    data_chunk const data=prepare_data();
    std::lock_guard<std::mutex> lk(mut);
    data_queue.push(data);  // 2
    data_cond.notify_one();  // 3
  }
}

void data_processing_thread()
{
  while(true)
  {
    std::unique_lock<std::mutex> lk(mut);  // 4 使用 unique_lock
    data_cond.wait(
         lk,[]{return !data_queue.empty();});  // 5 不断获得互斥量并查询，直到查询为 true 才返回，为 false 会暂时释放互斥量，为 true 返回后持续占用互斥量
    data_chunk data=data_queue.front();
    data_queue.pop();
    lk.unlock();  // 6 释放互斥量
    process(data);
    if(is_last_chunk(data))
      break;
  }
}
```

**4.1.2 使用条件变量构建线程安全队列**

##### 4.2 使用期望等待一次性事件



#### 其他

##### 进程的创建过程

1. 一个新进程总是通过一个进程的复制来创建的，子进程拥有相同的环境，只是进程 ID 不一样。这个过程称为 forking（分叉）
2. forking 之后，子进程的地址空间被新进程的数据覆盖，这是通过 exec 系统调用完成的。
3. fork-exec 机制只改变的待执行的代码，而环境保持不变，包括输入和输出设备的配置，环境变量和优先级。
4. Linux 的第一个进程 init（进程 ID 为 1）也是通过这种方法在 boot 阶段生成的，也叫 bootstrapping（引导） 阶段。
5. 在一些情况下，即使进程不是由 init 生成的，也可能变为 init 的父进程：变为守护进程。
6. 子进程结束，但没有被父进程 wait 处理，会变为僵尸进程。

[Link](https://www.linuxtopia.org/online_books/introduction_to_linux/linux_Process_creation.html)

##### 僵尸进程

1. 僵尸进程指的是，子进程退出后，父进程还未调用 wait ，使得在进程表中还保存着子进程的实体。该实体用于父进程查看子进程的退出状态。父进程通过 wait 系统调用查看退出状态，并释放该实体。
2. 父进程可以通过忽略 SIGCHLD 信号或者通过调用 sigaction 的 SA_NOCLDWAIT flag，这样子进程退出后其实体会立即销毁。
3. 因为僵尸进程只是一个进程表中的实体，因此无法通过调用 kill 进行回收。但可以 kill 它的父进程（或者向父进程发送 SIGCHLD 信号，使其调用 wait），将子进程转交给 init 进程。init 进程会周期性地调用 wait 收割僵尸进程。
4. 过多的僵尸进程会用尽进程号，在 32 位系统中，进程号默认范围为 32767.

[Link](https://unix.stackexchange.com/questions/155012/how-does-linux-handles-zombie-process)