#### 程序的内存分布(结构)

![](/assets/Snip20190225_1.png)

<br>
#### 一、程序的内存空间分布(每个程序在运行时都有一个独立的内存空间)

**1、程序的内存空间的划分主要分成以下4个部分:**

- **代码段(代码区)**<br>用于存放代码

- **数据段(全局区)**<br>用于存放全局变量等

- **栈空间**<br> 每调用一个函数就会给它分配一段连续的栈空间,等函数调用完毕后会自动回收这段栈空间 (栈平衡,调用时分配栈空间,调用完毕回收栈空间)

- **堆空间**<br> 需要主动去申请和释放


**2、在程序的运行过程中, 为了能够自由的控制内存的生命周期/大小, 会经常用到堆空间.** 

- **一般像Objective-C / java 的对象都是存储在堆空间 (堆空间的申请和释放需要程序员实施, 当然现在的编译器帮忙做了很多,程序员做的很少了).**
- **C++ 中的类比较特别,既可以存在于堆空间(需要程序员申请和回收)也可以存在于栈空间(不需要程序员管理)**






