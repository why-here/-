#### C++ 特性

##### 如何确定对象在 heap or stack

- 根据栈和堆的相对位置，局部变量会在栈中生成。

```c++
boolean fromStack(void *ptr) {
  int dummy;
  return ptr > &dummy;
}
```

##### lambda 表达式

```c++
[ capture clause ] (parameters) -> return-type  
{   
   definition of method   
} 
```

- 捕获方式 [&] 按引用捕获所有外部变量；[=] 按值捕获所有外部变量；[a,&b] 指明变量的捕获方式。

##### mutable 关键字

- 修饰类的数据成员，使其在 const 成员函数中也可以被修改

- 修饰 lambda 表达式按值传递，使其可以修改变量值（局部修改）

  ```c++
  int x{0};
  auto f1 = [=]() mutable {x = 42;};  // okay, 创建了一个函数类型的实例
  auto f2 = [=]()         {x = 42;};  // error, 不允许修改按值捕获的外部变量的值
  ```

  [Link](https://liam0205.me/2017/05/25/the-mutable-keyword-in-Cxx/)

##### delete 如何知道大小

在 new[] 返回指针的前一个地址会存储大小信息。

##### 线程

- 线程随着 std::thread 类型实例的创建而创建。

  ```c++
  #include <thread>
  thread t{func};
  t.join();
  $ g++ --std=c++11 -pthread hello_multithread.cpp
  ```

- 有三种创建线程的方式：简单函数、可调用实例的类型和 lambda 表达式。

  ```c++
  void do_some_work();
  std::thread wk_thread{do_some_work};
  ThreadTask task{42};
  std::thread wk_thread{task};
  std::thread wk_thread(ThreadTask());    // 1 函数声明
  std::thread wk_thread{ThreadTask{}};    // 2 线程定义
  std::thread wk_thread{[](){
      do_something();
  }};
  ```

- 线程结束控制：join 或者 detach 。join 主线程阻塞直到该子线程退出。detach 主线程丧失对子线程的控制，交给 C++ 运行时库。因此出现：主线程结束后，子线程仍在运行，可以作为守护线程；主线程结束随即资源销毁，子线程不能引用这些资源。

  ```c++
  if (join_me.joinable())       // 1
      join_me.join();
  if (detach_me.joinable())     // 1
      detach_me.detach();
  ```

- 考虑用 RAII 思想，将线程封装在一个类中，防止资源泄露（避免未处理线程结束状态，导致调用了 terminate() ，终止整个程序）

  ```c++
  struct ThreadGuard {
   private:
      std::thread& t_;
   public:
      explicit ThreadGuard(std::thread& t) : t_(t) {}
      ~ThreadGuard() {
          if (this->t_.joinable())          // 1
              this->t_.join();              // 2
      }
      ThreadGuard  (const ThreadGuard&) = delete;
      ThreadGuard& operator=(const ThreadGuard&) = delete;
  };
  ```

- 向线程传递参数，是将参数**拷贝**进线程类的内部存储空间，而后将参数传递给线程函数。当期望传入一个引用时，要使用`std::ref`进行转换 。应该避免传入可能被销毁的指针或者常量。

- 可以以非静态成员函数作为线程函数，需要传入在线程运行期间不会被销毁的类实例。

  ```c++
  class Foo {
   public:
      void bar(void);
  };
  void demo() {
      Foo baz;
      std::thread temp_t{&Foo::bar, &baz};
      temp_t.join();
      return;
  }
  ```

- 可以通过 move 改变线程的所有权。thread 是可移动但不可复制的。

  ```c++
  thread t1(f1);
  thread t2(move(t1));
  ```

  [Link](https://liam0205.me/2017/05/16/first-step-on-multithread-programming-of-cxx/)

##### 智能指针

- auto_ptr / unique_ptr / shared_ptr / weak_ptr 包含在 <memory> 头文件中。

- **auto_ptr** 

  - auto_ptr 是排他所有者模型，在 C++11 中弃用，由 unique_ptr 代替。

      ```c++
      auto_ptr<A> p1(new A); // p1 points to class A
      p1->show(); // call the show function of A
      p1.get(); // get the address
      auto_ptr<A> p2(p1); // copy constructor called, this makes p1 empty
      ```

  - auto_ptr 的拷贝构造函数以及赋值运算符将被操作对象的指针设为空（假复制），来实现只有一个 auto_ptr 拥有该指针。
  - 由于不能复制（假复制），不能在 STL 的容器中使用，所以被弃用。因为 STL 容器要求元素必须是可复制且可赋值的，并且不会互相影响。[Link](https://stackoverflow.com/questions/111478/why-is-it-wrong-to-use-stdauto-ptr-with-standard-containers)

- **unique_ptr**

  - 明确禁止复制构造以及赋值操作，可以通过 move 来转让指针，更加安全；支持数组。

    ```c++
    unique_ptr<A> p1(new A);
    cout << p1.get() << endl;
    unique_ptr<A> p2 = move(p1);   //  transfers ownership to p2
    
    unique_ptr<A> fun() {
        unique_ptr<A> ptr(new A);
        return ptr;                // can be captured;
    }
    ```

- **shared_ptr**

  - 是引用计数所有权模型，与所有 shared_ptr 副本共同维护指针的引用计数。只有引用计数等于 0 时，所指向的资源才会被释放。

    ```c++
    shared_ptr<A> p1(new A);
    shared_ptr<A> p2(p1);
    p1.get();
    p2.use_count() // 2, Returns the number of shared_ptr objects referring to the same managed object
    p1.reset();
    p2.use_count() // 1
    ```

- **weak_ptr**

  - weak_ptr 是作为 shared_ptr 的拷贝。能够访问 shared_ptr 所指向的内容，但不参与引用计数。可用来打破 shared_ptr 的循环依赖。[循环依赖](https://blog.csdn.net/Xiejingfa/article/details/50772571)

  - 将其中一个 shared_ptr 声明为 weak_ptr ，破除环。使用 weak_ptr 访问时需要检查可用性。

    ```c++
    shared_ptr<A> sp(new A);
    weak_ptr<A> wp(sp);
    if(shared_ptr<A> p = wp.lock()) 
    	...
    wp.expired() // true - unavailable, false - available
    ```

  - weak_ptr 没有重载 operator-> 和 operator * ，因此不可直接通过 weak_ptr 使用对象，一般通过 lock 函数得到 shared_ptr 实例。

  [Link](https://www.geeksforgeeks.org/auto_ptr-unique_ptr-shared_ptr-weak_ptr-2/)

##### 拷贝构造函数 / 赋值运算符

- 拷贝构造函数和赋值运算符的行为比较相似，都是将一个对象的值复制给另一个对象；但是其结果却有些不同，拷贝构造函数使用传入对象的值生成一个新的对象的实例，而赋值运算符是将对象的值复制给一个**已经存在的实例**。 

  ```c++
  Person p;
  Person p1 = p;    // Copy Constructor
  Person p2;
  p2 = p;           // Assign
  f(p2);            // Copy Constructor
  p2 = f1();        // Copy Constructor then Assign
  Person p3 = f1(); // Only call Copy Constructor once, directly construct p3, while not the temp instance
  ```

  [Link](https://www.cnblogs.com/wangguchangqing/p/6141743.html)

##### 编译过程

- 源代码 --编译器--》汇编代码 --汇编器--》目标代码 --链接器--》可执行文件。
- 链接器把多个目标文件合成一个可执行文件，各种符号(变量，函数) 相对地址会改变，需要进行符号重定位。
- 对于动态链接库，其地址不确定。重定位推迟。

[Link](https://blog.csdn.net/shenhuxi_yu/article/details/71437167)

##### c++11 常用特性

- 类型推导 auto
- for 循环迭代
- 两个尖括号，传统 >> 一律被当作右移运算符
- unordered_map/set

##### 迭代器失效问题

[Link](https://www.jb51.net/article/100683.htm)

##### 重写/重载/隐藏

**4.1成员函数被重载的特征**
（1）相同的范围（在同一个类中）； 
（2）函数名字相同； 
（3）参数不同； 
（4）virtual 关键字可有可无。 
**4.2“覆盖”是指派生类函数覆盖基类函数，特征是：**
（1）不同的范围（分别位于派生类与基类）； 
（2）函数名字相同； 
（3）参数相同； 
（4）基类函数必须有virtual 关键字。 
**4.3“隐藏”是指派生类的函数屏蔽了与其同名的基类函数，特征是：**

（1）如果派生类的函数与基类的函数同名，但是参数不同，此时，不论有无virtual关键字，基类的函数将被隐藏（注意别与重载混淆）。 
（2）如果派生类的函数与基类的函数同名，但是参数相同，但是基类函数没有virtual 关键字。此时，基类的函数被隐藏（注意别与覆盖混淆）。

[Link](https://www.cnblogs.com/BeyondAnyTime/archive/2012/06/05/2537451.html)

##### map 与 unordered_map 的区别

> map: #include < map >
>
> unordered_map: #include < unordered_map >
>
> - map： map 内部实现了一个红黑树，该结构具有自动排序的功能，因此 map 内部的所有元素都是**有序的**，map 的很多操作在 $O(logn)$ 的时间复杂度下就可以实现。
> - unordered_map: unordered_map 内部实现了一个哈希表，因此其元素的排列顺序是杂乱的，无序的。
> - 对于那些有顺序要求的问题，用 map 会更高效一些；对于查找问题，unordered_map 会更加高效一些。
> - 使用非内置类型作为 key，要使用 map ，需要重载 operator < ，而要使用 unordered_map 需要重载 operator == 。

##### 连续赋值顺序，从右置左

##### 面向对象的了解

> 面向对象编程注重的是：**1）数据和其行为的打包封装，2）程序的接口和实现的解耦**。[Link](https://coolshell.cn/articles/8745.html)

> 面向对象是相对于面向过程而言的。面向过程语言是一种基于**功能分析**的、以**算法**为中心的程序设计方法；而面向对象是一种基于**结构分析**的、以**数据**为中心的程序设计思想。
>
> >  从面向过程的角度看，类就是一个特殊的数据结构，它就好像是我们C语言中的结构体;从面向对象的角度看，类就是具有相同属性和方法的对象的集合。
> >
> >  面向对象有三大特性：封装、继承、多态。
> >
> > - **封装，**就是指隐藏对象的实现细节，给外界提供公共的方法来访问。
> >
> > - **继承**，子类可以继承父类的公共属性和方法，子类永远没法继承到父类的私有属性和方法。
> > - **多态，**就是同一个实现接口，对不同的实例而执行不同的操作。
> >
> >  [Link](https://my.oschina.net/shaw1688/blog/601142)

##### 多态实现原理

> 在基类的函数前加上virtual关键字，在派生类中重写该函数，运行时将会根据对象的实际类型来调用相应的函数。
>
> >  C++的多态性是通过动态绑定技术来实现的。
> >
> >  [Link](http://blog.csdn.net/tujiaw/article/details/6753498)

> 每一个有虚函数的类（或有虚函数的类的派生类）都有一个虚函数表，该类的任何对象中都放着虚函数表的指针。虚函数表中列出了该类的虚函数地址。
>
> >  多态的函数调用语句被编译成一系列根据基类指针所指向的（或基类引用所引用的）对象中存放的虚函数表的地址，在虚函数表中查找虚函数地址，并调用虚函数的指令。
> >
> >  [Link](https://www.jianshu.com/p/3a404ab34936) [Link](https://blog.csdn.net/lihao21/article/details/50688337)
>
> 虚函数表解析 [Link](https://blog.csdn.net/haoel/article/details/1948051)

##### 类的内存分配

> 基类，若有虚函数，则先是一个虚指针，然后是成员变量；子类，同样有虚指针，父类成员，子类成员。
>
> > 是这样的，当创建一个含有虚函数的父类的对象时，编译器在对象构造时将虚表指针指向父类的虚函数；同样，当创建子类的对象时，编译器在构造函数里将虚表指针（子类只有一个虚表指针，它来自父类）指向子类的虚表（这个虚表里面的虚函数入口地址是子类的）。 
>
> [Link](http://blog.jobbole.com/108785/)

##### C 语言实现多态

  使用函数指针，以及函数指针的字节对齐实现多态，使得将子类指针赋予父类指针，调用函数时能正常调用。

  [Link](http://www.cnblogs.com/wuyudong/p/achieving-polymorphism-in-c.html)

##### 多态

> 多态性的表现，这里用c++来简述，其实OOP应该都差不多。
>
> >  c++的多态分为两种：
> >
> >  1.编译时多态：重载，函数名称相同，但参数类型或参数个数不同的一组函数。在编译期就决好的。
> >
> >  2.运行时多态：重写（也称为覆盖override），也称为覆盖，牵扯到虚函数，简单来说就是虚函数（impure virtual）为我们实现一份默认的操作，我们可以使用这个也可以自己重写（覆盖）虚函数。

##### 右值引用与转移语义

> 右值引用 (Rvalue Referene) 是 C++ 新标准 (C++11, 11 代表 2011 年 ) 中引入的新特性 , 它实现了转移语义 (Move Sementics) 和精确传递 (Perfect Forwarding)。它的主要目的有两个方面：
>
> > 1. 消除两个对象交互时不必要的对象拷贝，节省运算存储资源，提高效率。
> > 2. 能够更简洁明确地定义泛型函数。
> >
> >  在 C++11 之前，右值是不能被引用的，最大限度就是用常量引用绑定一个右值

> - 通俗的左值的定义就是非临时对象，右值是指临时的对象，它们只在当前的语句中有效。
>
> > - 实际上右值是可以被修改的，既然右值可以被修改，那么就可以实现右值引用。
> > - 左值的声明符号为”&”， 为了和左值区分，右值的声明符号为”&&”。

> 右值引用是用来支持转移语义的。转移语义可以将资源 ( 堆，系统对象等 ) 从一个对象转移到另一个对象，这样能够减少不必要的临时对象的创建、拷贝以及销毁，能够大幅度提高 C++ 应用程序的性能。
>
> > - 参数（右值）的符号必须是右值引用符号，即“&&”。
> > - 参数（右值）不可以是常量，因为我们需要修改右值。
> > - 参数（右值）的资源链接和标记必须修改。否则，右值的析构函数就会释放资源。转移到新对象的资源也就无效了。

> 标准库提供了函数 std::move，这个函数以非常简单的方式将左值引用转换为右值引用。
>
> >  `std::move`在提高 swap 函数的的性能上非常有帮助。通过 std::move，一个简单的 swap 函数就避免了 3 次不必要的拷贝操作。

> 精确传递适用于这样的场景：需要将一组参数原封不动的传递给另一个函数。
>
> > - 函数 forward_value 为每一个参数必须重载两种类型，T& 和 const T&，否则，下面四种不同类型参数的调用中就不能同时满足
> > - 右值引用，只需要定义一次，接受一个右值引用的参数，就能够将所有的参数类型原封不动的传递给目标函数。

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

- 结构体中的所有成员其**首地址偏移量**必须为**其数据类型长度的整数倍**，其中第一个成员的首地址偏移量为0 。例如，若第二个成员类型为 int ，则其首地址偏移量必须为 4 的倍数，否则就要“首部填充”；以此类推。

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

##### malloc/free 和 new/delete 的区别

1. malloc/free 是 C/C++ 语言的标准库函数，new/delete 是 C++ 的运算符；

2. new 能自动分配空间大小

3. new/delete 会先调用 operator new/delete 申请/释放内存，然后调用对象的构造函数/析构函数，malloc/free 仅仅分配/释放内存。

4. new 返回对象指针，malloc 返回 void 指针。

5. 内存区域：new操作符从自由存储区（free store）上为对象动态分配内存空间，而malloc函数从堆上动态分配内存。 

   [Link](https://blog.csdn.net/nie19940803/article/details/76358673)

##### 自由存储区和堆的区别

- C++ 内存分布：“在C++中，内存区分为5个区，分别是堆、栈、自由存储区、全局/静态存储区、常量存储区”。 
- 自由存储区和堆的区别：

> “malloc在堆上分配的内存块，使用free释放内存，而new所申请的内存则是在自由存储区上，使用delete来释放。” ；
>
> 堆是操作系统维护的一块内存，而自由存储是C++中通过new与delete动态分配和释放对象的抽象概念。堆与自由存储区并不等价。 
>
> 所有的C++编译器默认使用堆来实现自由存储，也即是缺省的全局运算符new和delete也许会按照malloc和free的方式来被实现。
>
> 但程序员也可以通过重载操作符，改用其他内存来实现自由存储，例如全局变量做的对象池，这时自由存储区就区别于堆了。 

​	[Link](https://www.cnblogs.com/QG-whz/p/5060894.html)

##### 程序内存分布

- 运行时内存分布由代码段(Text)、初始化数据段(data)、未初始化数据段(BSS)、堆(heap)和栈(stack)构成，如果程序使用了内存映射文件（比如共享库、共享文件），那么包含映射段(MM)。 

- 代码段，只读，也存储字符串常量 ，合称只读区。

  `char s[] = "abc"; // 存储在栈中，运行时刻赋值`

  `char *p3 = "123456"; // 字符串常量存储在常量区中`

- 数据段（data）：用于存储初始化的全局变量和Static变量 ，段大小在编译时确定，所以内存的分配属于静态内存分配。 

- BSS 段：通常用来存放程序中未初始化的全局变量和Static，虽未显示初始化，但在程序载入内存执行时，由内核清0，所以未显示初始化则默认为0。BSS段的大小也是在编译时确定，运行时内存的分配属于静态内存分配。 

- 堆：用于保存程序运行时动态申请的内存空间，生命周期是整个程序运行期间，可用 free / delete 回收。

- 栈：用于保存函数的局部变量（但不包括static声明的静态变量，静态变量存放在数据段或BSS段）、参数、返回值、函数返回地址以及调用者环境信息（比如寄存器值）等信息，由系统进行内存的管理，在函数完成执行后，系统自行释放栈区内存，不需要用户管理。 它的地址空间“向下减少” 。

- 映射段：内核将文件内容（动态链接库、共享文件、匿名映射对象）直接映射到内存。 Linux中通过mmap()系统调用

- 内核空间：当进程处于内核态时，执行的内核代码会使用当前进程的内核栈。每个进程都有自己的内核栈。 程序的中断处理程序将使用当前进程的内核栈。这与处于内核态的进程的状态有些类似。 

  [Link](https://blog.csdn.net/k346k346/article/details/45592329)

##### 函数调用过程

- EBP 栈底指针，ESP 指向栈顶，EIP 指令指针

- 第一步：各个参数从右向左逐步要入栈中，然后压人返回地址（压入 EIP 保存现场）

- 第二步：压入 EBP ，保存原栈底地址，将 ESP 赋给 EBP ，存储局部变量，加入 64 B 的间隔区域。

- 第三步：分别将EBX，ESI，EDI压入栈中，属于 main 函数的执行数据，保护现场。EBX，ESI，EDI分别为基址寄存器，源变址寄存器，目的变址寄存器。 

- 第四步：执行函数

- 第五步：执行完毕，从栈顶恢复EBX，ESI，EDI。EBP 赋值 给 ESP 。恢复 main EBP 。

- 第六步：返回值，将保存的 EIP 值恢复，ESP - 参数大小，回到原栈顶

  [Link](https://blog.csdn.net/qq_35583007/article/details/78841904)

  返回值保存在一段临时区域,到下一条语句时,返回值被销毁,所以,如果要继续使用返回值,必须将返回 值赋予其他变量。 不大于32位的（返回值）在eax中，64位的在edx + eax中。再大就传指针了。 

##### printf/cout 执行编译顺序

- printf/cout 从右向左编译，从左向右输出，如 `cout << p << ++p;` 输出两个数值相等。

##### 类变量初始化顺序

- 初始化列表的执行顺序由变量的声明顺序决定。

##### 构造/析构执行顺序

- 先调用父类构造函数，再调用子类构造函数
- 先调用子类析构函数，再调用父类析构函数

##### 什么时候要将析构函数定义为虚函数

- 1.每个析构函数（不加 virtual） 只负责清除自己的成员。 
- 2.可能有基类指针，指向的确是派生类成员的情况。那么当析构一个指向派生类成员的基类指针时，程序就不知道怎么办了。所以要保证运行适当的析构函数，基类中的析构函数必须为虚析构。 
- [Link](https://blog.csdn.net/jiadebin890724/article/details/7951461)

##### 指针和引用的区别

- 1、指针是一个实体，需要分配内存空间。引用只是变量的别名，不需要分配内存空间。
- 2、引用在定义的时候必须进行初始化，并且不能够改变。指针在定义的时候不一定要初始化，并且指向的空间可变。（注：不能有引用的值不能为NULL）
- 3、有多级指针，但是没有多级引用，只能有一级引用。`int **p = a;`
- 4、指针和引用的自增运算结果不一样。（指针是指向下一个空间，引用时引用的变量值加1）
- 5、sizeof 引用得到的是所指向的变量（对象）的大小，而sizeof 指针得到的是指针本身的大小。
- 6、引用访问一个变量是直接访问，而指针访问一个变量是间接访问。

##### 4.1.3 求值顺序

- 优先级规定了运算对象的组合方式，但是没有说明运算对象按照什么顺序求值，如：

  `int i = f1() * f2()` 不知 f1() 和 f2() 哪个先调用

- 只有 && || ?: , 四种运算符规定了求值顺序，都是从左至右。

##### 4.10 逗号运算符

- 从左向右的顺序求职，常用在 for 循环中

  `for(; ; ++ix , ++cnt )`

##### 4.11 类型转换

- `int ival = 3.541 + 3;` 3 会隐式转换为 double，尽可能避免损失精度
- 非 const pointer 可以转换为 const pointer ，反过来不行，尝试去掉 const 属性不行。
- 显示转换：cast-name<type>(expression);
  - static_cast ：一般用于执行会损失精度的转换，避免出现 warning 如 int -> double ，用于告诉编译器不在乎损失精度。不能转 const 类型。
  - const_cast ：只能改变 const ，用于去掉 const 特性，不能改变类型
  - reinterpret_cast ：为位模式提供较低层次上的重新解释。
  - dynamic_cast ：通常用作向下转换【基类到派生类】和平行转换【基类到基类】 ，成功返回指针/引用，负责返回NULL；通过虚表中指示的类型信息进行类型检查。因此必须要有虚函数。[Link](https://blog.csdn.net/lianghui0811/article/details/76487416?locationNum=8&fps=1) 
- 旧式显示转换 c++
  - type(expr) 函数形式
  - (type)expr c 语言风格

##### 6.1.2 函数声明

- 函数的名字也必须在使用之前声明
- 含有函数声明的头文件应该被包含到定义函数的源文件中

##### 6.2 数组参数

- `void print(int (&arr)[10] )` 只能绑定到数组大小为 10 的数组上；可用非类型模板参数，使其适应任意大小的数组
- `int (*matrix)[10]` <==> `int matrix[][10]` // 指向含有 10 个整数的数组的指针
- `int *matrix[10]` // 一维 *int 数组，10 个指针构成的数组
- main 函数的参数是可选的， `int main(int argc, char *argv[])
- 值是如何被返回的：返回的值用于初始化调用点的一个临时变量，该临时变量就是函数调用结果
- NDEBUG 预处理变量，如果定义了 NDEBUG 则 assert 什么也不做

##### 6.7 函数指针

- 函数的类型由它的返回类型和形参类型共同决定
- 函数指针的赋值和调用与变量一样
  - 声明函数 `bool lengthCompare(const string &, const string &);`
  - 声明函数指针 `bool (*pf)(const string &, const string &);`
  - pf = lengthCompare; // 自动转换为指针

##### 7.1 定义抽象数据类型

- 调用成员函数，会用对象地址初始化 this
- this **默认**指向的是非常量类型，因此不能绑定到常量对象上（不能隐式去掉 const 特性），在成员函数后面加上 const 即可 `int isbn() const { ... }`
- 因此，在该函数内不能更改对象的内容，常量对象（引用，指针）都只能调用常量成员函数
- 构造函数：`Sales_data() = default;` 保留默认构造函数
- 在类内部定义的函数将是内联的
- 拷贝：初始化，参数传递
- 赋值：赋值运算符
- override 关键字 ：如果派生类在虚函数声明时使用了override描述符，那么该函数必须重载其基类中的同名函数，否则代码将无法通过编译。 
- delete 关键字 ： C++11 中，可在想要 “禁止使用” 的特殊成员函数声明后加 “= delete”（当然也可以声明为私有函数或者保护函数），而需要保留的加 "= default" 或者不采取操作 
- 返回 *this; 对象本身

##### 7.2 访问控制

- struct 默认 public ， class 默认 private
- 友元 ：类可以允许其他类或函数访问他的非共有成员，在类中增加以 friend 开头的声明。friend class A; 
- 类本身就是一个作用域

##### 7.3 类的其他特性

- 要在 const 函数中修改成员变量，需要为变量增加 mutable 关键字 `mutable size_t access_ctr;`
- 友元影响的是访问权限而非声明

##### 7.5 构造函数

- 构造函数初始化列表不会影响初始化顺序，由定义顺序指定
- Sales_data obj(); 声明了一个函数而非对象，应该去掉括号
- 只允许一步类类型转换
- 将构造函数声明为 explicit（只允许出现在类内部声明中）阻止隐式转换

##### 7.6 静态成员

- 静态成员函数不包含 this 指针，仍然可以使用对象访问静态成员

##### 11 关联容器

- 三维：1. set or map 2. 重复 or 不重复 3. order ？ 
- map 未存在会自动创建并初始化
- set 关键字集合，find() 返回 iterator
- 有序容器的关键字类型必须定义元素的比较方法
- pair <utility> pair<t1, t2> make_pari(v1, v2) 自动推断类型
- map 的迭代器指向 pair 类型 first second
- set 的迭代器是 const 的
- set.insert(), map.insert(pair) 插入存在的元素不会有影响。map insert 返回 pair ，first 为关键字的迭代器，second 为是否已存在，已存在 false 
- 访问元素 find count 
- 删除 erase
- 无序容器使用 hash 以及 == 运算符

##### 12 动态内存

- 智能指针，用来管理动态对象，负责自动释放所指向的对象
- shared_ptr <memory>
- make_shared 模板函数：分配一个对象并初始化，返回此对象的 shared_ptr 
  - make_shared(10, '9');

- shared_ptr 拷贝/赋值 auto p(q); auto p = q;

- 智能指针类能记录有多少个 shared_ptr 指向相同的对象，并能在恰当的时候自动释放对象。

- new 默认情况下是默认初始化。内置类型在局部内不进行默认初始化

- 用 new 的返回值初始化 shared_ptr 

- 智能指针的构造函数是 explicit 的，当将一个 shared_ptr 绑定到一个普通指针时，我们就将内存管理责任交给了这个 shared_ptr 。

- p.unique() 是否是唯一用户；p.reset() 重设指针

- shared_ptr 可以在初始化时指定子集的释放操作

- unique_ptr ：只能有一个 unique_ptr 指向一个给定对象，不支持拷贝，赋值 (可以作为返回值传递) ，通过 p.release() 转移 p.reset(q.release())

- unique_ptr 与动态数组，unique_ptr<int[]> up(new int [10]); up.release() 自动调用 delete []

- shared_ptr 不直接管理动态数组，需指定自己的删除器

- weak_ptr ：时一种不控制所指对象生存周期的智能指针，它指向一个由 shared_ptr 所管理的对象，但不会改变 shared_ptr 的引用计数。因此不能使用 weak_ptr 直接访问对象，而必须调用 lock 判断对象是否还存在。

- allocator 类 ：类型内存分配器，先分配内存但未构造，之后再按需要构造内存

  auto p = allocator<T> a; a.allocate(n); a.deallocate(p, n); a.construct(p, args); a.destory(p); //执行析构

#### Python 特性

[Link](https://github.com/taizilongxu/interview_python)

#### Git

##### 分区

> 分为：工作区，版本库，版本库包含暂存区、分支以及分支指针。
>
> >  第一步是用`git add`把文件添加进去，实际上就是把文件修改添加到暂存区；
> >
> >  第二步是用`git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支。

- fetch 与 pull 的区别

  > - git fetch ：相当于是从远程获取最新版本到本地，不会自动 merge
  > - git pull ：相当于是从远程获取最新版本并 merge 到本地