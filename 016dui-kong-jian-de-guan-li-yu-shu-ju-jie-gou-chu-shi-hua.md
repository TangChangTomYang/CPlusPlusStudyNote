#### 堆空间的管理 与 数据结构的初始化


<br>
#### 一、堆空间的分配/ 回收
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
#### 二、 堆空间的初始化





<br>
##### 方式1: &nbsp;  malloc & memset  /free

使用**malloc(size_t __size)** 分配堆空间, 使用**memset(void *p, int value , size_t len)** 初始化堆空间

<br>**API  功能说明:**
```
int *p = (int *)malloc(4); // 分配4字节的堆空间
memset(p,0,4); //从p开始的4个字节堆空间,每个字节都使用 0 来初始化
```

<br> **示例说明:**
```
// malloc 方式 堆空间初识化(手动初始化)
void test (){
    int *p = (int *)malloc(4); //分配4字节的堆空间
    // 从p地址开始的4个字节,每个字节都设置为0
    memset(p , 0, 4);  
    
// 这样也可以初始化
//    size_t size = sizeof(p); // 获取堆空间的长度
//    memset(p, 0, size);
    cout << *p << endl;
 
    free(p); // malloc 必须和free 成对出现
}
```

<br>
<br>
##### 方式二: &nbsp; new/ delete 或者 new[]/ delete[]

**new** 的功能和 ***malloc** 的功能差不多, 只是 **new**的功能更强大, 在C++ 中尽量使用**new** 

<br>
**示例说明:**
```

// 堆空间 单个元素 和 数组的初始化
void test2(){
    // 这种就是没有初识化的
    int *p = new int ;
    // 初始化为 0
    int *p1 = new int() ;
    // 初始化为5
    int *p2 = new int(5) ;
    
    // 初始化一个连续的空间(数组, 3个int), 未被初始化
    int *p3 = new int[3] ;
    // 初始化一个连续的空间(数组, 3个int), 初始化 每个元素初识化为0
    int *p4 = new int[3]() ;
    //初始化一个连续的空间(数组, 3个int), 数组中的元素使用{} 里的内容(当前为:0,0,0) 初始化
    int *p5 = new int[3]{} ; // 注意: {} 只能用在数组的右边,是用来初始化数组的
    //初始化一个连续的空间(数组, 3个int), 数组中的元素使用{} 里的内容(当前为:5,0,0 ) 初始化
    int *p6 = new int[3]{5} ;// 注意: {} 只能用在数组的右边,是用来初始化数组的
    
    
    cout << *p << endl;
    cout << *p1 << endl;
    cout << *p2 << endl;
    cout << p3[0] << p3[1] << p3[2]  << endl;
    cout << p4[0] << p4[1] << p4[2]  << endl;
    cout << p5[0] << p5[1] << p5[2]  << endl;
    cout << p6[0] << p6[1] << p6[2]  << endl;
   
   
    
    /** 结论:
    1. 以后凡是要在堆空间申请一段内存除了使用 new 关键字分配外, 最好在类型右边加上 (), 这样被新分配的堆空间就被初始化了
    2. 如果要在堆空间分配一个数组, 那么在类型的右边可以使用小括号() 来初始化, 也可以使用大括号{}来精细初始胡
     */
}

```

**注意:**
1> malloc 和 new 都只是 分配堆空间, 不会初始化.
2> 使用malloc 分配的堆空间,一般配合 memset 来初始化, 使用free 来回收内存
3> 使用 new 分配的空间一般配合小括号() 来初始化, 用 delete 来回收.
4> 使用 new[] 分配的堆空间数组 配合小括号()或者大括号{} 来初始化, 使用 delete[] 来回收.
5> 注意在初始化时, 大括号{} 只能放在数组旁边.



<br>
#### 三、memset 函数

memset 函数一将较大的数据结构(比如对象/ 数组)内存清零的比较快的方法.

```
Person  *pson;
pson.m_id = 1;
pson.m_age = 20
pson.m_height = 100;
memset(&pson,0,sizeof(pson));


Person pson2[] = {{1,202,100},{1,202,100},{1,202,100}};
memset(&pson2, 0 , sizeof(pson22));
```









<br>
#### 三、memset 函数


