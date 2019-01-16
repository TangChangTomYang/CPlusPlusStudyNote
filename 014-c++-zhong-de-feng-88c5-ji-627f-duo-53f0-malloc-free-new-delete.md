分配分配分#### C++ 中的封装/继承/多台/Malloc/free/new/delete



<br>
#### 一、封装


**1、什么是封装? **
封装就是成员变量私有化, 提供公共的 getter 和 setter 给外界去访问成员变量.

```
struct Person {
private:
    int m_age;
    
public:
    void setAge(int age){
        m_ge = age;
        // 也可以这样写(等价的)
//        this -> m_age = age;
    }
    
    int age(){
        return m_age;
        // 也可以这样写(等价的)
//        return this -> m_age;
    }
}

int main(){
    Person pson;
    pson.setAge(10);
    cout << pson.age() << endl;
    
    getchar();
    return 0;
}
```









<br>
#### 二、程序的内存空间(每个程序在运行时都有一个独立的内存空间)

1、程序的内存空间的划分主要分成以下4个部分:

- **代码段(代码区)**<br>用于存放代码

- **数据段(全局区)**<br>用于存放全局变量等

- **栈空间**<br> 每调用一个函数就会给它分配一段连续的栈空间,等函数调用调用完毕后会自动回收这段栈空间 (栈平衡,调用时分配栈空间,调用完毕回收栈空间)

- **堆空间**<br> 需要主动去申请和释放


2、在程序的运行过程中, 为了能够自由的控制内存的生命周期/大小, 会经常用到堆空间.






<br> 
#### 三、堆空间的分配/ 回收
```
(一一对应, 不要写错了)
 malloc --> free
 new --> delete
 new [] --> delete []
 ```
 
**方式一:**
C++ / C 语言中通用的做法 
```
void test (){
    // 向堆空间申请(分配)4字节的空间
    int *p = (int *)malloc(4);
    *p = 20; //给堆空间分配的内存赋值
    cout << *p << endl;
    // 释放 堆空间分配的数据
    free(p);
}
```




<br>
**方式二:**
C++ 特有的做法
```
void test2(){
    int *p = new int ; // 在占空间分配一个 int 的空间\
    
    int *pArr = new int[10]; // 申请10个连续的int 空间
    
    delete p; // 使用完毕, 释放申请的占空间
    
    delete[] pArr; // 在释放时一定要在delete 后加 []
    
}
```

相较malloc/ free , new/ delete 做的事情要多一些

**注意点:**
1> 申请堆空间成功后,会返回那一段内存空间的地址.
2> 申请和释放必须是一对一的关系, 不然可能会存在内存泄露.

现在很对高级语言不需要开发人员去管理内存(比如: java), 屏蔽了很多内存细节,利弊同时存在.
1> 利: 提高开发效率, 避免内存使用不当或泄露
2> 弊: 不利于开发人员了解本质,永远停留在API调用和表层语法,对性能优化无从下手.





<br>
#### 四、 堆空间的初始化

<br>
##### 方式1:   malloc & memset 
使用**malloc(size_t __size)** 分配堆空间, 使用**memset(void *p, int value , size_t len)** 初始化堆空间

<br>
**API  功能说明:**
```
int *p = (int *)malloc(4); // 分配4字节的堆空间
memset(p,0,4); //从p开始的4个字节堆空间,每个字节都使用 0 来初始化
```


